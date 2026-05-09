# Cult Inc — Audit de la documentation

_Généré le 2026-05-08. Dernière passe : 2026-05-09 (cleanup §5 — items mécaniques résolus sur PROJECT/PACING/ARCHITECTURE/BACKLOG/CHANGELOG, items design explicitement déférés)._

---

## 1. Cohérence inter-documents

### ✅ Nommage des ressources — résolu (2026-05-09)

Identifiant code canonique : **`followers`**. Vérification grep des docs : zéro occurrence de "Believers" en dehors de cet audit, et la "Followers" capitalisée en prose anglaise est de la grammaire normale (début de phrase, nom de concept), pas du naming drift.

Les 3 occurrences résiduelles de "Believers" dans ce document ont été nettoyées dans la même passe.

---

### ✅ Action "Preach" — résolu (2026-05-09)

Section "Click Actions" ajoutée à `BALANCE.md` au niveau manifeste (rôle qualitatif, évolution attendue, décisions design). Conformément à la philosophie de `BALANCE.md`, les valeurs (`BASE_PREACH`, `click_multiplier` initial) vivent dans `src/game/constants.ts` et la formule dans `src/game/formulas.ts` — pas dans le manifeste.

Ce point était mal posé dans la version initiale de l'audit : il demandait une "formule + valeurs initiales" dans BALANCE, ce qui violait la règle *"All tunable constants live in src/game/constants.ts"* énoncée en tête de BALANCE.md.

---

### ✅ Formule `heatPerMinute` — résolu (2026-05-09)

Section "Composition de heat_per_minute" ajoutée dans `BALANCE.md > Heat`. Précise que `active_event_heat = sum(event.heat for event in activeEvents)` et aligne explicitement la formule manifeste avec la signature TypeScript de `ARCHITECTURE.md`.

---

### ✅ FEAT-006 (assignation des followers) — résolu (2026-05-09)

Section "Follower States" ajoutée à `BALANCE.md`. Définit les trois états (`idle`, `preaching`, `working`), leur rôle, et l'état par défaut au recrutement (`preaching`). Décision design notable : `idle` est volontairement passif en Phase 1 et révèle son rôle stratégique post-Revelation.

---

## 2. Complétude — ce qui est mentionné mais pas défini

### 🔴 Doctrine — formule de gain manquante

BALANCE.md liste Doctrine comme ressource prestige mais ne définit pas :
- Combien de Doctrine gagne-t-on par Revelation ?
- Y a-t-il un seuil minimum de followers/Belief pour déclencher une Revelation ?

### 🔴 Rival faction — citée sans spec

PACING.md (mid-game) : _"Map expansion and rival faction visible"_.  
BACKLOG.md FEAT-020 : _"Rival faction NPC — competes for followers in the same pool"_.  
Aucun document ne définit la mécanique : comment compete-t-elle ? À quelle vitesse ? Est-elle affectée par Heat ?

### 🟡 Upgrade "Midnight Sermons" — implémentation ambiguë

BALANCE.md : _"×1.5 Belief during 22:00–04:00 local time"_.  
Quelle heure de référence ? Fuseau local du joueur ? Serveur ? Problèmes potentiels sur Android si le fuseau change.

### ✅ Shelter cap — résolu (2026-05-09)

Sous-section "Cap mechanism (Phase 1)" ajoutée à `BALANCE.md > Shelter`. Décision tranchée : **hard cap explicite** en Phase 1, avec construction volontaire d'abris. Le mode "tolérer le surpeuplement" (cap mou avec malus Heat) est listé comme idée Phase 2.

### 🟡 Prestige — ce qui est conservé après Revelation non défini

PACING.md : _"Communicate clearly what carries over"_.  
Aucun document ne liste ce qui est conservé (Doctrine oui, mais quoi d'autre ? Upgrades ? Shelter ?).

---

## 3. Actionnabilité — ambiguïtés pour l'implémentation

| Problème | Impact |
|----------|--------|
| ~~Nom des ressources non tranché~~ | ✅ Résolu 2026-05-09 — `followers` adopté |
| ~~Action Preach non chiffrée~~ | ✅ Résolu 2026-05-09 — section "Click Actions" dans BALANCE |
| ~~États des followers~~ | ✅ Résolu 2026-05-09 — section "Follower States" dans BALANCE |
| Rival faction sans spec | Non bloquant Phase 1, mais à documenter avant Phase 2 |
| Doctrine gain formula manquante | Non bloquant Phase 1 |
| ~~Shelter cap non explicité~~ | ✅ Résolu 2026-05-09 — hard cap Phase 1, voir BALANCE > Shelter |

---

## 4. Documents manquants

| Document suggéré | Contenu | Priorité |
|-----------------|---------|----------|
| `GLOSSARY.md` | Définitions canoniques : followers, Belief, Shelter, Heat, Doctrine, Revelation, Preaching, Idle, Working | 🟡 Moyenne (plus bloquant depuis que le naming est tranché) |
| `ENTITIES.md` | Spec du système Divine Entities (mentionné en détail dans PROJECT.md mais sans doc dédié) | 🟡 Phase 2 |
| `SAVE-FORMAT.md` | Schéma JSON de sauvegarde, champs requis, stratégie de migration entre versions | 🟡 Avant implémentation persistance |
| `UI.md` | Contraintes visuelles, mobile-first, implications Capacitor/Android, layout cible | 🟡 Avant implémentation UI |
| `EVENTS.md` | Définition des événements (BACKLOG FEAT-013), structure, conditions de déclenchement, textes | 🟡 Phase 1 Should Have |

---

## 5. Améliorations par fichier

### BALANCE.md
- [x] ~~Uniformiser le terme : `followers` partout~~ (résolu 2026-05-09)
- [x] ~~Ajouter section "Click Actions"~~ (résolu 2026-05-09 — manifeste, valeurs dans constants.ts)
- [x] ~~Ajouter section "Follower States"~~ (résolu 2026-05-09)
- [x] ~~Préciser comment `active_event_heat` est calculé~~ (résolu 2026-05-09)
- [x] ~~Définir comment Shelter bloque le recrutement~~ (résolu 2026-05-09 — hard cap Phase 1)
- [ ] **Déféré** — Ajouter formule de gain de Doctrine par Revelation. Décision design ouverte (combien de Doctrine = quelle quantité de Belief sacrifié, quel seuil minimum). À spécifier avant Phase 2.
- [ ] **Déféré** — Préciser le fuseau horaire pour "Midnight Sermons". Le doc reconnaît déjà la tension dans "Known design tensions" et propose un toggle. Décision reportée jusqu'à l'implémentation effective de la mécanique (Phase 2+).

### PACING.md
- [ ] **Déféré** — Section "Mobile & Android" : nécessite une décision UX sur les notifications push, le format des sessions courtes mobile vs. desktop. À traiter avec la passe Capacitor.
- [x] ~~Référencer les 3 personas de PROJECT.md dans Session Length Targets~~ (résolu 2026-05-09 — colonne "Persona principal" ajoutée)
- [x] ~~Développer les "Do Not Do" avec des exemples concrets liés aux formules de BALANCE~~ (résolu 2026-05-09 — 4 items précisés, 1 ajouté sur Shelter)
- [ ] **Déféré** — Préciser comment "prestige milestone visible on horizon" se traduit en UI. Décision UI design, à traiter avec UI.md / les premières maquettes.

### ARCHITECTURE.md
- [ ] **Déféré** — Section "Android / Capacitor" : à écrire quand on s'attaque à FEAT-033 (Icebox actuellement).
- [x] ~~Aligner la signature de `heatPerMinute` avec la formule de BALANCE.md~~ (résolu 2026-05-09 — section "Composition de heat_per_minute" dans BALANCE)
- [x] ~~Documenter la stratégie de migration de sauvegarde~~ (résolu 2026-05-09 — section "Stratégie de migration" dans Persistence)
- [x] ~~Ajouter `isPremium` dans l'interface GameState~~ (résolu 2026-05-09)
- [x] ~~Documenter le pattern selector Zustand recommandé~~ (résolu 2026-05-09 — section "Zustand — pattern selector côté composants")

### PROJECT.md
- [x] ~~Ajouter Capacitor dans le tableau Tech Stack~~ (résolu 2026-05-09 — + ESLint/Husky/lint-staged ajouté)
- [ ] **Déféré** — Référencer ENTITIES.md quand il sera créé (Phase 2).
- [x] ~~Lier les Key Personas à PACING.md~~ (résolu 2026-05-09 — référence croisée vers Session Length Targets)

### BACKLOG.md
- [ ] **Déféré (volume)** — Liens depuis chaque item 📋 vers la section de doc correspondante. Travail de référencement répétitif, à faire en passe groupée quand l'arborescence des docs sera plus stable.
- [x] ~~Ajouter FEAT-006 dans BALANCE avant de le marquer Spec ready~~ (résolu 2026-05-09 via section "Follower States")
- [x] ~~Corriger la numérotation~~ (résolu 2026-05-09 — note d'introduction ajoutée expliquant que les IDs suivent l'ordre de création, pas l'ordre du doc ; aucun ID manquant entre 001 et 046)
- [ ] **Hors scope actuel** — Agents `balance-check` et `pacing-check` n'existent pas (dossier `agents/` vide). À planifier comme initiative à part si on veut automatiser des checks.

### CHANGELOG.md
- [x] ~~Ajouter `CLAUDE.md`~~ (résolu 2026-05-09 dans [Unreleased])
- [ ] **Hors scope actuel** — `agents/balance-check.md`, `agents/pacing-check.md` : ces fichiers n'existent pas encore.
- [ ] **Anticipation** — `src/types/game.ts` et `src/store/gameStore.ts` à ajouter au [Unreleased] quand ils seront effectivement créés.

---

## Verdict global

La documentation est **solide dans son intention** — PROJECT.md et PACING.md montrent une vision claire du jeu. Les problèmes sont principalement dans la **couche d'implémentation** : un développeur qui ouvre ces docs pour coder se retrouve bloqué sur des ambiguïtés évitables (noms de ressources, formule Preach, états followers).

**Priorité immédiate (état au 2026-05-09 après passe §5) :**
1. Spec rival faction (FEAT-020) avant Phase 2.
2. Lister ce qui carry-over à la Revelation (cf. §2 Prestige).
3. Formule de gain de Doctrine par Revelation.

Les bloquants Phase 1 sont levés. Le cleanup §5 a été traité — items mécaniques résolus, items demandant une décision design explicitement déférés avec justification.
