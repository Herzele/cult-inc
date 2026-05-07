# Cult Inc — Backlog

Items are loosely ordered by priority within each section. Move items to CHANGELOG.md when shipped.

---

## Phase 1 — Core Loop (Prototype)

### Must Have
- [ ] Game tick system (configurable tick rate, requestAnimationFrame loop)
- [ ] Belief resource — the primary currency
- [ ] Click interaction — "Preach" button generates Belief
- [ ] First follower — passive Belief generation
- [ ] Recruit mechanic — spend Belief to gain Followers
- [ ] Follower assignment — idle vs. preaching vs. working
- [ ] Zustand game store with actions and selectors
- [ ] Persistent save via localStorage (JSON snapshot)
- [ ] Offline progress calculation on load
- [ ] Basic UI shell — resource bar, action panel, log panel

### Should Have
- [ ] Tiered upgrades — unlock multipliers for Belief and Followers
- [ ] Heat system — rises with size, triggers events at thresholds
- [ ] Simple event system — random narrative pop-ups with choices
- [ ] Settings panel — speed, mute, reset

### Nice to Have
- [ ] Animated belief counter
- [ ] Sound effects (ambient chanting, ding on milestone)
- [ ] Dark/light theme toggle

---

## Phase 2 — Prestige & Depth

- [ ] First prestige mechanic ("Revelation") — reset resources, gain Doctrine points
- [ ] Doctrine tree — permanent passive bonuses
- [ ] Rival faction NPC — competes for followers in the same pool
- [ ] Secrecy stat — opposes Heat, unlocked via upgrades
- [ ] Map view — expand to new regions

---

## Phase 3 — Archetypes & Polish

- [ ] Three cult archetypes selectable at game start (Commune, Media Empire, Doomsday Sect)
- [ ] Archetype-specific upgrades and event chains
- [ ] Narrative log — scrollable history of key events
- [ ] Achievements system
- [ ] Cloud save (Supabase or similar)

---

## Phase 4 — Launch

- [ ] Playtesting feedback integration
- [ ] Performance audit (no jank at 10k followers)
- [ ] Accessibility pass (keyboard nav, contrast)
- [ ] SEO / social share metadata
- [ ] Analytics (privacy-safe, opt-in)

---

## Icebox (no current priority)

- Mobile app wrapper (Capacitor)
- Multiplayer / leaderboards
- Procedurally generated cult names
- Steam release via Electron
