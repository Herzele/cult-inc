# Cult Inc — Project Overview

## Concept

Cult Inc is a browser-based incremental idle game where you start as a charismatic nobody and grow your cult from a handful of believers into a globe-spanning spiritual empire. You manage followers, resources, rituals, and rival factions — all while hiding your true power from society.

## Core Fantasy

The player feels the seductive pull of accumulating belief, loyalty, and influence. Every decision is a trade-off between growth and exposure, speed and control.

## Pillars

1. **Accumulation** — Resources compound. Followers beget followers. Rituals unlock rituals.
2. **Secrecy vs. Scale** — The bigger you grow, the harder you are to hide. Heat is the main constraint.
3. **Narrative Momentum** — Each prestige cycle recontextualizes your cult's history and mythology.
4. **Emergent Strategy** — No single optimal path. Player archetypes: isolationist communes, media cults, doomsday sects, wellness empires.

## Divine Entities System

Entities are not chosen by the player — they choose the player based on accumulated actions and playstyle.

**Alignment axes** — every entity sits somewhere on two independent axes:
- Malefic ↔ Benevolent
- Chaos ↔ Order

**Power types:**
- *Passive unlocks* — permanent bonuses while the entity is present
- *Active abilities* — triggered by the player at a cost
- *Situational events* — positive or negative occurrences inflicted on the player by the entity, outside their control

**Heat relationship** — entities have strong opinions about cult size. Some demand a small, devoted flock (low Heat preferred); others require massive public visibility and actively push the player toward high Heat.

**Progression model (inspired by Hades):**
- Each prestige run reveals more of an entity's true nature and motivations
- Lore depth accumulates across runs without locking the player out of exploring other entities
- New entities unlock progressively at prestige milestones

**Phase constraints:**
- Phase 1: no entities (core loop only)
- Phase 2: one entity at a time, full 4-axis roster introduced gradually
- Phase 3: cross-entity combination mechanics unlock with prestige level
- Entity conflict mechanics deferred to a later phase

---

## Tech Stack

| Layer | Choice |
|-------|--------|
| Framework | React 19 + TypeScript |
| Build | Vite 6 |
| State | Zustand |
| Styling | Tailwind CSS v4 |
| Unit Tests | Vitest |
| E2E Tests | Playwright |

## Key Personas

- **The Lurker** — plays passively, returns every few hours to collect
- **The Optimizer** — wants every upgrade timed, reads the balance sheet
- **The Lore Enjoyer** — reads every event text, wants narrative payoff

## Project Goals

- [ ] Playable prototype (core loop) — Phase 1
- [ ] First prestige mechanic — Phase 2
- [ ] Divine entity system (Phase 2) — one entity, 4 axes, passive/active/situational powers
- [ ] Three distinct cult archetypes — Phase 3
- [ ] Multi-entity combinations (Phase 3)
- [ ] Save/load + cloud sync — Phase 3
- [ ] Soft launch / public playtest — Phase 4

## Repository Layout

```
/src          — game source code
/docs         — design documents (this folder)
/tests        — Playwright e2e tests
/prototypes   — throwaway experiments and mechanic sketches
/agents       — Claude Code agent prompts and automation scripts
```
