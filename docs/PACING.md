# Cult Inc — Pacing & Player Journey

Maps the intended emotional arc across a full playthrough, from new player to prestige veteran.

---

## First Session (0–30 min)

**Goal:** Hook the player on the core loop before they close the tab.

| Minute | Expected State | Emotional Beat |
|--------|---------------|----------------|
| 0:00 | Empty game, just a "Preach" button | Curiosity |
| 0:30 | First follower recruited | Delight — someone believes! |
| 2:00 | Passive generation begins | Relief — it works without clicking |
| 5:00 | First upgrade purchased | Power spike |
| 10:00 | Heat hits 25 for the first time | Tension — "am I going too fast?" |
| 15:00 | Heat crackdown or scare | Stakes established |
| 20:00 | Recovery, second upgrade | Strategic thinking begins |
| 30:00 | Prestige milestone visible on horizon | Long-term goal established |

**Key design rule:** The player should never wait more than 90 seconds for something to happen in the first 15 minutes.

---

## Early Game (30 min – 2 hr)

- Follower counts grow into the dozens
- Player experiments with follower assignment ratios
- Heat becomes a constant management concern
- Upgrade tree begins to feel like a real decision tree
- First "oh no I messed up" moment (Heat crackdown, wrong upgrade order)

**Pacing lever:** New content unlocks every ~10–15 minutes of active play.

---

## Mid Game (2–4 hr, first prestige)

- Followers in the hundreds
- Map expansion and rival faction visible
- Doctrine tree visible but empty
- Revelation (prestige) button unlocks
- Player weighs: reset now for bonuses vs. push further?

**Key beat:** First prestige should feel like a satisfying choice, not a forced reset. Communicate clearly what carries over.

---

## Post-Prestige Loop (4+ hr)

- Runs get faster (10x, then 100x on subsequent prestiges)
- Doctrine tree opens up asymmetric playstyles
- Archetype identity solidifies
- Endgame: fill the Doctrine tree, achieve "World Revelation" — a true ending state

---

## Session Length Targets

| Session Type | Length | Content Density | Persona principal |
|-------------|--------|-----------------|-------------------|
| Quick check-in | 2–5 min | Collect offline progress, queue upgrades | The Lurker |
| Casual session | 20–40 min | Manage heat, see events unfold | The Lore Enjoyer |
| Deep session | 2–4 hr | Complete a prestige cycle | The Optimizer |

Les personas sont définis dans `PROJECT.md > Key Personas`.

---

## Negative Feedback Loops (intentional tension)

1. **Heat** — growth causes exposure, exposure limits growth
2. **Recruit cost scaling** — each follower is more expensive
3. **Rival faction** — competes for followers when Heat is high

## Positive Feedback Loops (engine feel)

1. Followers generate Belief → buy more Followers
2. Doctrine bonuses compound across runs
3. Upgrades stack multiplicatively

---

## Do Not Do

- **Do not gate the first follower behind more than 60 seconds of clicking.** Concrètement : si `BASE_PREACH × click_multiplier × 60` ne couvre pas le coût du premier follower, retuner les constantes.
- **Do not make prestige feel like punishment** — always show the net gain. Concrètement : avant de valider une Revelation, l'UI doit montrer le delta `Doctrine actuel + gain estimé` et la liste de ce qui est conservé (cf. `BALANCE.md > Doctrine` et la décision en attente sur le carry-over post-Revelation).
- **Do not introduce Heat events faster than players can read the explanation.** Concrètement : un événement de Heat doit donner au joueur 2–3 ticks de jeu de marge entre l'apparition et l'effet, comme énoncé dans `BALANCE.md > Tuning principles > "Heat events should be readable"`.
- **Do not make the Shelter cap silent.** Quand le bouton Recruit est désactivé par le cap, le tooltip doit le dire (cf. `BALANCE.md > Shelter > Cap mechanism`). Un bouton qui ne réagit pas sans explication est l'archétype du bug perçu.
