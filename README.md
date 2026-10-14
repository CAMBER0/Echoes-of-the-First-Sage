# Echoes of the First Sage

**A DLC-sized story expansion for _The Legend of Zelda: Tears of the Kingdom_, in which Link investigates a Zonai energy surge in the Forgotten Temple and crosses a Chronolith into Ancient Hyrule, 10,000 years before the present era.**

There, alongside the Ancient Hero, he must uncover the source of a temporal rupture before returning to a changed modern Hyrule.

## Project status

Pre-production / tooling setup.

## Repository policy

This repository contains original mod source, documentation, build scripts, and release metadata only. It does not include Nintendo game data, game dumps, executable code, encryption keys, or copyrighted assets redistributed from the base game.

## Layout

- `docs/` — design notes, quest-state diagrams, flag registry, and installation instructions.
- `source/romfs/` — the mod's intended RomFS overlay, organized by game path.
- `scripts/` — repeatable validation and build automation.
- `releases/` — release notes and packaging manifests; generated archives remain untracked.

## Development requirements

See [docs/tooling-setup.md](docs/tooling-setup.md) for the approved development toolchain and first-time setup.
