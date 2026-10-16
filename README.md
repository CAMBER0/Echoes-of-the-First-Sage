# Echoes of the Ancient Hero

**A late-game, DLC-sized fan campaign for _The Legend of Zelda: Tears of the Kingdom_.** After the four Regional Phenomena and discovery of the Dragon's Tears map, Link discovers the Archive of Hours beneath the Forgotten Temple. Its Chronolith does not rewrite history: it opens controlled rifts into five sealed trial-sites tied to an incomplete record of the Ancient Hero.

Link earns the restricted **Echo Trace** ability, restores five regional seals in any order, and returns to the temple to enter the Citadel of the Last Hour. The campaign ends with the Hollow Champion, a deliberately original archive-born foe, and the Echo Covenant upgrade.

## Project status

Story and technical pre-production. The first playable milestone is the Chronolith Trial vertical slice.

## Design documents

- [Story bible](docs/story-bible.md) - campaign structure, canon boundaries, regional chapters, and player-facing rewards.
- [Chronolith Trial plan](docs/phase-01-modern-hook.md) - the first safe, testable gameplay milestone.
- [Flag registry](docs/flag-registry.md) - design-state names and save-persistence rules; not yet native game-data keys.
- [M0 research log](docs/m0-research-log.md) - verified data-layout observations and the next map-placement evidence to collect.

## Repository policy

This repository contains original mod source, documentation, build scripts, and release metadata only. It does not include Nintendo game data, game dumps, executable code, encryption keys, or copyrighted assets redistributed from the base game.

## Layout

- docs/ - design notes, quest-state diagrams, flag registry, and installation instructions.
- source/romfs/ - the mod's intended RomFS overlay, organized by game path.
- source/design/ - project-owned implementation specifications, safe to version before binary game files exist.
- scripts/ - repeatable validation and build automation.
- releases/ - release notes and packaging manifests; generated archives remain untracked.

## Development requirements

See [docs/tooling-setup.md](docs/tooling-setup.md) for the approved development toolchain and first-time setup.
