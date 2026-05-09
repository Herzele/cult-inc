# Cult Inc — Changelog

Follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format.
Versions use [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

### Added
- Project scaffold: Vite + React + TypeScript + Zustand + Tailwind CSS v4
- Folder structure: `/src`, `/docs`, `/tests`, `/prototypes`, `/agents`
- Design docs: PROJECT.md, BACKLOG.md, BALANCE.md, PACING.md, ARCHITECTURE.md
- Testing setup: Vitest + Playwright configured
- `CLAUDE.md` — instructions projet pour les outils Claude (entrée auto-chargée)
- `docs/AUDIT.md` — audit vivant des incohérences entre docs
- `BALANCE.md` : section "Click Actions" (rôle qualitatif de Preach, Phase 1+)
- `BALANCE.md` : section "Follower States" (idle / preaching / working, défaut `preaching` au recrutement, idle à rôle évolutif post-Revelation)
- `BALANCE.md > Shelter` : sous-section "Cap mechanism" — hard cap explicite Phase 1
- `BALANCE.md > Heat` : sous-section "Composition de heat_per_minute" alignée avec la signature TypeScript de ARCHITECTURE.md

- `PROJECT.md` : Capacitor + ESLint/Husky/lint-staged au tableau Tech Stack ; cross-refs Personas → PACING
- `PACING.md` : colonne "Persona principal" sur Session Length Targets ; "Do Not Do" enrichi (4 items précisés + Shelter cap silencieux)
- `ARCHITECTURE.md` : `isPremium` dans GameState, stratégie de migration `saveVersion`, section "Zustand — pattern selector"
- `BACKLOG.md` : note explicative sur la numérotation `FEAT-XXX` (ordre de création, pas de gap)

### Changed
- `AUDIT.md` : naming `followers` tranché, Believers nettoyé, items §1 résolus marqués ✅
- `AUDIT.md §5` : passe de cleanup terminée — items mécaniques résolus, items design explicitement déférés avec justification

---

<!-- Template for future entries:

## [0.x.0] — YYYY-MM-DD

### Added
- 

### Changed
- 

### Fixed
- 

### Removed
- 

-->
