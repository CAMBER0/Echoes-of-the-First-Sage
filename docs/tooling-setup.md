# Tooling setup

## Purpose

This project uses a **working copy** for edits and a separate, private **reference dump** for comparison. Never edit your only copy of game data, and never add the reference dump to Git.

## Folder convention

Choose locations outside this repository for private data and downloaded apps:

```text
D:\TotK-Private\ReferenceRomFS\   # your personal, legally obtained reference
D:\TotK-Private\WorkRomFS\        # a copied working overlay / staging area
D:\TotK-Tools\                     # downloaded editors
```

The repository's `source\romfs\` directory records only the mod files that will be overlaid at release time.

## Required tools

1. **NX-Editor + TotK plugin** — inspection and editing of supported Nintendo formats.
2. **TkZstd** — decompresses/recompresses TotK `.zs` files.
3. **TOTK Event Editor** — visual editing of EventFlow files (`.bfevfl`).
4. **MrMystery MapEditor** — legacy map-placement workflow. It is archived; use it only with version-pinned backups.
5. **Visual Studio Code** — editing YAML, Markdown, JSON, C#, and PowerShell.
6. **Git** — history, review, releases, and collaboration.

## Installation checklist

- [x] Git installed (`git --version` verified)
- [x] .NET runtime installed (NX-Editor requires .NET 10 x64)
- [ ] NX-Editor launcher installed and TotK plugin enabled
- [ ] TkZstd installed and pointed to a private RomFS directory
- [ ] TOTK Event Editor extracted
- [ ] MapEditor version archived locally with its documentation
- [ ] VS Code installed with C# and YAML extensions
- [ ] GitHub repository created and this local repository pushed

## First safe workflow

1. Back up the original file you intend to study.
2. Decompress a copy when it is a `.zs` file.
3. Inspect the vanilla equivalent in NX-Editor or Event Editor.
4. Create a project-owned copy under `source\romfs\` only after making a deliberate change.
5. Validate the file opens again in the editor before committing.
6. Commit a small, descriptive unit of work.

## GitHub publishing rule

Every public release must include a plain-language installation guide, game version compatibility, checksum/version notes for your release archive, and a statement that it contains no base-game files.
