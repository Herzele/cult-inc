# Cult Inc — Backlog

Items are loosely ordered by priority within each section. Move items to CHANGELOG.md when shipped.

Status icons: 📋 Spec (ready to build) · 💡 Idée (not yet specced) · 🚧 In Progress · ✅ Done

> **Numérotation `FEAT-XXX` :** les IDs sont attribués dans l'ordre de création, pas dans l'ordre de lecture du document. C'est pour ça que les phases ne sont pas strictement croissantes (ex. Phase 2 — Divine Entities = FEAT-037→041, ajouté après Phase 4 = FEAT-028→032). Aucun ID n'est manquant entre 001 et 046.

---

## Phase 1 — Core Loop (Prototype)

### Must Have
- [ ] 📋 FEAT-001 Game tick system (configurable tick rate, requestAnimationFrame loop)
- [ ] 📋 FEAT-002 Belief resource — the primary currency
- [ ] 📋 FEAT-003 Click interaction — "Preach" button generates Belief
- [ ] 📋 FEAT-004 First follower — passive Belief generation
- [ ] 📋 FEAT-005 Recruit mechanic — spend Belief to gain Followers
- [ ] 📋 FEAT-006 Follower assignment — idle vs. preaching vs. working
- [ ] 📋 FEAT-007 Zustand game store with actions and selectors
- [ ] 📋 FEAT-008 Persistent save via localStorage (JSON snapshot)
- [ ] 📋 FEAT-009 Offline progress calculation on load
- [ ] 📋 FEAT-010 Basic UI shell — resource bar, action panel, log panel

### Should Have
- [ ] 💡 FEAT-011 Tiered upgrades — unlock multipliers for Belief and Followers
- [ ] 💡 FEAT-012 Heat system — rises with size, triggers events at thresholds
- [ ] 💡 FEAT-013 Simple event system — random narrative pop-ups with choices
- [ ] 💡 FEAT-014 Settings panel — speed, mute, reset

### Nice to Have
- [ ] 💡 FEAT-015 Animated belief counter
- [ ] 💡 FEAT-016 Sound effects (ambient chanting, ding on milestone)
- [ ] 💡 FEAT-017 Dark/light theme toggle

---

## Phase 2 — Prestige & Depth

- [ ] 💡 FEAT-018 First prestige mechanic ("Revelation") — reset resources, gain Doctrine points
- [ ] 💡 FEAT-019 Doctrine tree — permanent passive bonuses
- [ ] 💡 FEAT-020 Rival faction NPC — competes for followers in the same pool
- [ ] 💡 FEAT-021 Secrecy stat — opposes Heat, unlocked via upgrades
- [ ] 💡 FEAT-022 Map view — expand to new regions

---

## Phase 2 — Divine Entities

- [ ] 💡 FEAT-037 Entity detection system — tracks player behavior to determine which entity manifests
- [ ] 💡 FEAT-038 Entity manifestation — chosen entity reveals itself via narrative events
- [ ] 💡 FEAT-039 Entity power system — passive unlocks, active abilities, situational events (positive/negative)
- [ ] 💡 FEAT-040 Entity influence on Heat — each entity pushes toward its preferred cult profile
- [ ] 💡 FEAT-041 4 alignment axes implementation: Malefic / Benevolent / Chaos / Order

---

## Phase 3 — Archetypes & Polish

- [ ] 💡 FEAT-023 Three cult archetypes selectable at game start (Commune, Media Empire, Doomsday Sect)
- [ ] 💡 FEAT-024 Archetype-specific upgrades and event chains
- [ ] 💡 FEAT-025 Narrative log — scrollable history of key events
- [ ] 💡 FEAT-026 Achievements system
- [ ] 💡 FEAT-027 Cloud save (Supabase or similar)
- [ ] 💡 FEAT-042 Cross-entity combinations — multi-deity bonuses unlocked at prestige milestones

---

## Phase 3 — Monetization

- [ ] 💡 FEAT-043 Cosmetic system — follower skins, temple themes, visual styles
- [ ] 💡 FEAT-044 Optional boosters — temporary multipliers, non-blocking
- [ ] 💡 FEAT-045 Founder pack (one-time purchase) — exclusive cosmetics + supporter badge
- [ ] 💡 FEAT-046 `isPremium` flag in game store from day one (even if empty)

---

## Phase 4 — Launch

- [ ] 💡 FEAT-028 Playtesting feedback integration
- [ ] 💡 FEAT-029 Performance audit (no jank at 10k followers)
- [ ] 💡 FEAT-030 Accessibility pass (keyboard nav, contrast)
- [ ] 💡 FEAT-031 SEO / social share metadata
- [ ] 💡 FEAT-032 Analytics (privacy-safe, opt-in)

---

## Icebox (no current priority)

- 💡 FEAT-033 Mobile app wrapper (Capacitor)
- 💡 FEAT-034 Multiplayer / leaderboards
- 💡 FEAT-035 Procedurally generated cult names
- 💡 FEAT-036 Steam release via Electron