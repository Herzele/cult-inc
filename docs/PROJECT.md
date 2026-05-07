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
- [ ] Three distinct cult archetypes — Phase 3
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
