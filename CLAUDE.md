# Cult Inc — Instructions projet

> Ce fichier est l'entrée des instructions projet. Il est chargé automatiquement par les outils Claude (Cowork, Claude Code). À maintenir vivant — voir la section *Maintenance de ce fichier* en bas.
>
> Dernière mise à jour : 2026-05-09 (passe AUDIT — naming + sections BALANCE + cleanup §5).

---

## Identité

*Cult Inc* est un simulateur de gestion de culte incrémental (idle game) sur le web (et Android via Capacitor). Le joueur recrute des `followers`, développe son culte, gère cinq ressources, et débloque des mécaniques au fil du temps. Univers fictif et satirique assumé.

Le projet sert aussi de **support d'apprentissage à Cyprien** — voir la section *Approche pédagogique*.

## Stack et infra

- **Front** : React 19 + TypeScript strict, Vite 6, Tailwind CSS v4.
- **State** : Zustand par slices (pas de Redux/Saga/RxJS).
- **Tests** : Vitest (unit), Playwright (e2e).
- **Qualité** : ESLint + Husky + lint-staged (`--max-warnings 0`).
- **Repo** : https://github.com/Herzele/cult-inc/ (branche `master`). Local : `E:\Cult`.
- **Cibles** : web navigateur, Android via Capacitor.

## La doc `docs/` est la source de vérité

Avant toute proposition non triviale, lire le doc pertinent et le citer. Cartographie :

- `docs/PROJECT.md` — concept, piliers, personas, système Divine Entities, phases.
- `docs/ARCHITECTURE.md` — structure `src/`, slices Zustand, tick RAF, contraintes perf (tick < 2 ms, save < 10 KB).
- `docs/BALANCE.md` — manifeste d'intention (le *pourquoi* des mécaniques). Les chiffres tunables vont dans `src/game/constants.ts`, pas dans ce doc.
- `docs/PACING.md` — courbe émotionnelle, milestones par session, "do not do".
- `docs/BACKLOG.md` — features `FEAT-XXX` avec statut (📋 specifié / 💡 idée / 🚧 in progress / ✅ done).
- `docs/CHANGELOG.md` — format Keep a Changelog. Toute feature livrée passe de `BACKLOG` à `CHANGELOG [Unreleased]`.
- `docs/AUDIT.md` — audit vivant des incohérences entre docs. À mettre à jour quand on en résout ou en découvre.

## Naming canonique (voir AUDIT.md §1)

Terme officiel pour les adeptes : **`followers`** (jamais "Believers" ni autre variante). Si un doc utilise un autre mot, c'est un bug à corriger, pas une variante à propager.

| Concept | Identifiant canonique |
|---------|----------------------|
| Adeptes | `followers` |
| Ressources | `belief`, `followers`, `shelter`, `heat`, `doctrine` |
| Action principale | `preach` |
| Reset prestige | `revelation` |
| États d'un follower | `idle` \| `preaching` \| `working` |

## Conventions de code

TypeScript strict, pas de `any`. Composants React fonctionnels uniquement. Tailwind v4 pour le style — pas de CSS custom hors `index.css`. État global via Zustand par slices (`resources`, `upgrades`, `events`, `meta`), state local via `useState`. **Toute la logique de jeu vit dans `src/game/` en fonctions pures**, importable sans store — c'est la couche que Vitest teste en priorité. Pas de logique de jeu dans les composants React. La boucle de jeu utilise `requestAnimationFrame`, jamais `setInterval`. Persistance : `localStorage` avec `saveVersion` et migrations dès le début.

## Game design — réflexes attendus

Toujours raisonner en boucles : croissance (positive), Heat (négative), prestige (méta). Pour chaque mécanique proposée, expose son rôle dans une de ces boucles et la tension qu'elle crée. La règle d'or de `PACING.md` : jamais plus de 90 s d'attente sans rien dans les 15 premières minutes. La règle d'or de `BALANCE.md` : tout wait doit avoir une raison (lire, planifier, regarder).

## Tests

Toute formule économique nouvelle = test Vitest avec coût, production, et cas limite. Avant de marquer une feature finie : `npm run lint && npm run test:run` doit passer. Les flows critiques (premier follower, premier prestige) sont couverts par Playwright.

## Workflow attendu pour une feature

1. Vérifier si elle est dans `BACKLOG.md` et son statut.
2. Lire le doc concerné (`BALANCE.md`, `ARCHITECTURE.md`…).
3. Si la feature manque d'une donnée (cas typique : action `preach` pas chiffrée — cf. AUDIT §1), **alerter et proposer de la spécifier d'abord** plutôt que coder à l'aveugle.
4. À la livraison : mettre à jour `CHANGELOG.md [Unreleased]`, déplacer le statut dans `BACKLOG.md`, et marquer l'item résolu dans `AUDIT.md` si applicable.

## Ce qu'il faut éviter

- Références à des religions ou groupes réels.
- Mécaniques de monétisation prédatrices (la monétisation prévue : cosmétiques + boosters non-bloquants + founder pack, cf. FEAT-043 à 046).
- Redux/Saga/RxJS, frameworks de jeu lourds.
- Logique de jeu dans les composants React.
- Propager un naming non canonique trouvé dans un doc.

## Approche pédagogique

Ce projet est un support d'apprentissage pour Cyprien. Chaque nouvelle notion ou opération technique est expliquée brièvement en début de réponse, la première fois qu'elle apparaît. Les notions déjà couvertes ne sont pas ré-expliquées.

### Notions techniques déjà couvertes

- Structure du projet Vite + React + TypeScript (fichiers de config, dossiers `src/`, `node_modules/`)
- Rôle de Zustand comme gestionnaire de state global
- Différence state global (Zustand) vs state local (`useState`)
- Rôle de Vitest (tests unitaires) et Playwright (tests e2e)
- `CLAUDE.md` : fichier de contexte chargé automatiquement par les outils Claude
- `git init`, remote, commit, push, force push
- Capacitor : outil pour packager une app web React/Vite en APK Android

## Priorités immédiates (état au 2026-05-09, source : `AUDIT.md`)

Les bloquants Phase 1 sont levés (naming, Click Actions, Follower States, Shelter cap, composition Heat). Reste à traiter :

1. Spec **rival faction** (FEAT-020) — avant Phase 2.
2. Lister ce qui **carry-over à la Revelation** (Doctrine oui, mais quoi d'autre ?).
3. **Formule de gain de Doctrine** par Revelation.
4. Passe groupée du **cleanup §5 d'AUDIT** (micro-corrections sur tous les fichiers).
5. `GLOSSARY.md` peut attendre le moment où on introduit les premiers termes de game design (events, rituels) qui en auront besoin.

Si une demande d'implémentation touche un de ces points non résolus, le signaler avant de coder.

---

## Maintenance de ce fichier

Mettre à jour `CLAUDE.md` quand :

- Une **notion technique nouvelle** est introduite → ajouter à *Notions techniques déjà couvertes*.
- Le **naming canonique** évolue → mettre à jour le tableau et `AUDIT.md`.
- Un **nouveau document** apparaît dans `docs/` → ajouter à la cartographie.
- Les **priorités immédiates** changent → résoudre des items, en ajouter, mettre à jour la date.
- Une **convention de code** est tranchée différemment → mettre à jour la section concernée.
- Le **stack** change (ajout/retrait de dépendance majeure).

À chaque mise à jour, actualiser la date "Dernière mise à jour" en haut du fichier.
