# Cult Inc — Architecture

## Overview

Client-only React SPA. No server. State lives in Zustand, persisted to localStorage. All game logic is deterministic TypeScript — no side effects outside the store actions.

---

## Folder Structure

```
src/
  components/       — React UI components (dumb, subscribe to store slices)
  game/
    engine.ts       — tick loop, requestAnimationFrame driver
    formulas.ts     — pure functions: costs, rates, offline calc
    events.ts       — event definitions and trigger conditions
    upgrades.ts     — upgrade definitions
  store/
    index.ts        — root Zustand store
    slices/
      resources.ts  — belief, followers, heat, doctrine
      upgrades.ts   — purchased upgrades, available upgrades
      events.ts     — active events, event history
      meta.ts       — run count, prestige bonuses, settings
  types/
    game.ts         — all shared TypeScript types and interfaces
  test/
    setup.ts        — vitest setup
```

---

## State Architecture (Zustand)

The store is split into slices combined at the root. Each slice owns its state and actions.

```typescript
// Rough shape
interface GameState {
  // Resources
  belief: number
  followers: number
  shelter: number
  heat: number
  doctrine: number

  // Meta
  tickCount: number
  lastSaveTime: number
  runCount: number
  isPremium: boolean // anticipé pour FEAT-046, false par défaut

  // Collections
  upgrades: Record<UpgradeId, UpgradeState>
  activeEvents: GameEvent[]

  // Actions
  tick: (deltaMs: number) => void
  preach: () => void
  recruit: () => void
  purchaseUpgrade: (id: UpgradeId) => void
  save: () => void
  load: () => void
  prestige: () => void
}
```

---

## Tick Loop

The game engine runs a `requestAnimationFrame` loop that fires `store.tick(deltaMs)` each frame. The tick action:

1. Computes resource deltas using `formulas.ts`
2. Applies deltas to state
3. Checks event trigger conditions
4. Autosaves every 30 seconds

**No React state is used for game logic.** Components read from Zustand via selectors. This keeps the tick loop independent of React's render cycle.

---

## Persistence

```typescript
// Save: JSON.stringify the saveable slice of state → localStorage['cult-inc-save']
// Load: parse, validate schema version, apply to store
// Offline: (now - lastSaveTime) * beliefPerSecond, capped at 4 hours
```

Schema versioning: `saveVersion` field in the save object. Migrations run on load when `saveVersion` is behind `CURRENT_SAVE_VERSION`.

**Stratégie de migration :**
- Chaque montée de `CURRENT_SAVE_VERSION` est accompagnée d'une fonction `migrate_v{N-1}_to_v{N}(save) → save'` dans `src/game/migrations.ts`.
- Au load, on applique séquentiellement les migrations de `save.saveVersion` à `CURRENT_SAVE_VERSION`.
- Une migration est **non destructive par défaut** : si un champ disparaît, on le conserve quand même dans le save sérialisé pendant 1 version (deprecation), puis on le retire à la suivante. Cela protège des rollbacks involontaires.
- Si le save est plus récent que `CURRENT_SAVE_VERSION` (joueur revenu d'une beta), on refuse le load et on propose un export JSON brut pour le récupérer manuellement.

---

## Formulas Module

All game math lives in `src/game/formulas.ts` as pure functions with no imports from the store. This makes them trivially testable with Vitest.

```typescript
export function recruitCost(n: number, upgrades: UpgradeState): number
export function beliefPerSecond(state: ResourceState): number
export function heatPerMinute(followers: number, activeEvents: GameEvent[]): number
export function offlineProgress(bps: number, offlineSeconds: number): number
```

---

## Testing Strategy

| Layer | Tool | What |
|-------|------|------|
| Formulas | Vitest | Unit test every formula with edge cases |
| Store actions | Vitest | Integration test tick sequences |
| UI components | Vitest + Testing Library | Render, interact, assert output |
| Full game flows | Playwright | Click through core loop, verify milestone states |

---

## Performance Constraints

- Tick must complete in < 2ms (frame budget is 16ms at 60fps)
- Store state must stay < 10KB serialized (localStorage limit awareness)
- No unbounded arrays — event history capped at 100 entries, log at 200

---

## Decisions & Rationale

| Decision | Rationale |
|----------|-----------|
| Zustand over Redux | Less boilerplate, slice pattern fits incremental games |
| Tailwind v4 | No config file, CSS-first, pairs well with Vite plugin |
| No backend | Reduces complexity for solo dev; localStorage is sufficient for v1 |
| RAF loop over setInterval | More accurate timing, pauses when tab is hidden |
| Formulas as pure functions | Enables fast unit tests without store setup |

---

## Zustand — pattern selector côté composants

Les composants ne lisent **jamais** le store entier — toujours via un selector ciblé pour limiter les re-renders.

```typescript
// ✅ Bon — re-render seulement si belief change
const belief = useGameStore((s) => s.belief)

// ❌ Mauvais — re-render à chaque tick parce que tout l'objet change de référence
const state = useGameStore()

// ✅ Multi-champ : utiliser shallow pour comparer field par field
import { useShallow } from 'zustand/react/shallow'
const { belief, followers } = useGameStore(useShallow((s) => ({
  belief: s.belief,
  followers: s.followers,
})))
```

Règle pratique : si un composant n'a besoin que de N valeurs scalaires, écrire N selectors plutôt qu'un selector objet. Le coût d'écriture est compensé par la simplicité de raisonner sur les re-renders.
