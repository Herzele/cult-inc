# Cult Inc — Balance Manifesto

Design intent document. Describes *why* each mechanic exists and *what it should feel like*, not the exact numbers. All tunable constants live in `src/game/constants.ts`.

---

## Philosophy

Incremental games live or die on their feedback loops. Every resource should feel meaningful at the moment it's introduced, and every mechanic should create a decision — not just a wait.

The core tension in Cult Inc is **growth vs. exposure**. The player always wants more followers, but more followers means more Heat. There is no "safe" path — only tradeoffs.

---

## Resources — design intent

### Belief
The primary currency and the pulse of the game. It should feel abundant early (every click matters, every second ticks forward) and scarce mid-game when upgrade costs escalate. Belief is never "lost" — it's always spent on something, which should feel intentional, not punishing.

### Followers
The engine. Followers transform Belief from a manual grind into a passive machine. Recruiting the first follower is the most important moment in the game — it should feel like a threshold crossed, not a routine purchase. Each subsequent follower should feel slightly harder to justify, with the player always asking "can I afford the Heat?"

### Shelter
A soft governor on growth. Its purpose is to prevent runaway follower stacking and to give upgrades a concrete, spatial meaning. The player should occasionally feel the ceiling — "I need to build before I can recruit."

**Cap mechanism (Phase 1) — hard cap explicite.** Quand `followers === shelterCapacity`, le bouton Recruit est désactivé. Tooltip clair : *"Pas de place. Construis un nouvel abri."* Pas de pénalité progressive, pas de surpeuplement toléré.

Construire un abri est une **action volontaire** avec coût Belief croissant (formule dans `formulas.ts`, valeurs dans `constants.ts`). Le joueur choisit son rythme : agrandir d'abord puis recruter à plein, ou alterner.

*Tension visée :* le rythme `construire → recruter → construire`. Pas de dégradation continue, juste un seuil binaire qui se manifeste comme un prérequis.

*Phase 2 (idée) :* un toggle "Tolérer le surpeuplement" comme upgrade débloquable. Activé, il permettrait de dépasser le cap mais chaque follower au-dessus génèrerait du Heat passif (lien thématique : surpeuplement → suspicion du voisinage). Donnerait au joueur expérimenté un levier d'arbitrage entre Heat et Belief.

### Heat
The primary risk mechanic. Heat should create genuine anxiety, not just a cooldown timer. The player should feel the heat rising before it becomes critical, and recovery should require active decisions, not just waiting. Low Heat = false security. High Heat = exciting danger.

**Composition de `heat_per_minute` :**

```
heat_per_minute = base_heat(followers) + active_event_heat
```

Où :
- `base_heat(followers)` : fonction monotone croissante des followers, à tuner. Définie dans `formulas.ts`, paramétrée par `constants.ts`. La forme initiale (linéaire `followers / 10`) est une hypothèse, pas une décision.
- `active_event_heat` = `sum(event.heat for event in activeEvents)` : chaque événement actif déclare un champ `heat` qui s'additionne. Permet à un événement de répression d'augmenter brusquement le Heat sans modifier la formule de base.

Ceci aligne la formule décrite ici avec la signature TypeScript `heatPerMinute(followers: number, activeEvents: GameEvent[]): number` de `ARCHITECTURE.md`.

### Doctrine
The prestige currency. Earned through the sacrifice of resetting, Doctrine should feel like wisdom accumulated across runs. Each point spent should meaningfully alter the next playthrough — not just speed it up, but change how it feels.

---

## Click Actions

### Preach
Le seul levier d'agence direct du joueur. Doit créer un sentiment de "je fais quelque chose" dès le tout premier clic, avant même que la boucle passive démarre.

*Évolution qualitative attendue :*
- **0–30 sec** : seul moyen de générer du Belief, chaque clic compte.
- **Premier follower → 5 min** : Preach reste utile mais le passif décolle. Le joueur peut commencer à lâcher la souris sans culpabilité.
- **Mid early-game** : Preach devient marginal en valeur absolue, mais reste un levier d'urgence (besoin opportuniste de Belief pour un recrutement, un upgrade qui apparaît juste hors d'atteinte).
- **Late game** : symbolique. Quelques upgrades ou événements peuvent ponctuellement le rendre intéressant à nouveau (multiplicateur ×100 sur un event, "appel divin" de 30 secondes).

*Décisions design :* Preach n'a ni coût ni cooldown en Phase 1. Sa production est un produit `BASE × click_multiplier` où `click_multiplier` est élevé par les upgrades et plus tard par la Doctrine. Tout chiffrage vit dans `src/game/constants.ts`.

---

## Follower States

Trois états : `idle`, `preaching`, `working`. Au recrutement, un follower arrive **`preaching`** par défaut — sinon le core loop est bloqué dès le premier follower, ce qui contredit la promesse de PACING (*"It works without me"*).

### Preaching
L'état du moteur. Génère du Belief. C'est ce qui fait que le jeu joue tout seul. Doit représenter la majorité écrasante des followers en early-game.

### Working
Débloqué plus tard, vise à différencier les rôles. Un follower `working` est affecté à une tâche ou un bâtiment spécifique (construction d'abri, étude de la Doctrine, garde anti-Heat). Sa contribution dépend de l'affectation. Crée la première vraie décision d'allocation : Belief vs. Shelter vs. Doctrine.

### Idle
Initialement passif : ne produit rien, ne consomme rien. Sa raison d'être est **évolutive et révélée par la Revelation**. Post-prestige, l'idle devient une réserve stratégique (pool pour rituels ponctuels, amortisseur lors d'événements de répression, candidats pour les nouveaux types de tâche débloqués par la Doctrine).

*Conséquence design :* en Phase 1, `idle` peut paraître inutile au joueur — c'est intentionnel. La première Revelation est aussi le moment où le joueur découvre à quoi servait cet état. Un follower assigné `idle` en Phase 1 n'est pas un gâchis, il est une promesse.

---

## Core feedback loops

### The growth loop (positive)
Followers generate Belief → Belief buys more Followers → more Followers generate more Belief.
This loop should feel satisfying and almost hypnotic. The numbers going up is the reward.

### The Heat loop (negative)
More Followers → more Heat → events disrupt growth → player adapts → growth resumes.
This loop should prevent the growth loop from feeling trivial. Without Heat, there's no game.

### The prestige loop (meta)
Enough Belief accumulated → Revelation available → player weighs reset vs. continue → Doctrine earned → next run faster and different.
This loop should feel like a meaningful choice, never like an obligation.

---

## Experience milestones — what the player should feel

These are emotional targets, not timers. The actual numbers that produce these moments live in `src/game/constants.ts` and will be tuned through playtesting.

| Milestone | Target feeling |
|-----------|---------------|
| First click | "Something is happening" |
| First follower recruited | "Someone believes in me" — genuine delight |
| First passive tick | "It works without me" — relief and wonder |
| First upgrade purchased | Power spike — the machine just got better |
| First Heat scare | "I'm growing too fast" — exciting tension |
| First crackdown | Stakes are real — but recovery feels possible |
| First Revelation available | "I could reset... but do I want to?" |
| First prestige completed | "I understand this game now" |

---

## Tuning principles

**Never punish curiosity.** If a player does something natural (recruits fast, clicks a lot, ignores Heat), the game should respond interestingly, not wall them out.

**Every wait should have a reason.** If the player is waiting for Belief to accumulate, there should be something to read, something to plan, or something to watch.

**Upgrades should feel like decisions.** If the optimal upgrade order is obvious, the upgrade tree needs more variation. Players should occasionally regret a choice and want to try differently next time.

**Heat events should be readable.** Never trigger a punishing event without giving the player at least 2–3 game ticks of visible warning. Surprise punishment feels unfair; telegraphed punishment feels earned.

**Prestige must never feel like punishment.** Always show the player exactly what they keep and what they gain before they commit to a Revelation. The net gain should be visible and meaningful.

---

## Known design tensions

- **Donation Box dilemma** — idle play becoming dominant too early removes the active engagement that makes the early game fun. Consider gating behind prestige.
- **Midnight Sermons** — time-of-day mechanics are interesting but can feel unfair to players in different timezones or sleep schedules. Consider making it a toggle or an upgrade that redefines when "midnight" is.
- **Heat decay asymmetry** — very low follower counts may decay Heat too fast, removing tension from the early game. Tune carefully around the first 10 minutes.
