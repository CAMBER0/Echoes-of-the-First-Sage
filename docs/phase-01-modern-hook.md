# Phase 1 — Modern Hook Vertical Slice

## Goal

Build one small, safe playable loop before attempting the custom ancient map:

```text
Forgotten Temple interaction
  -> inspect Chronolith
  -> set mod quest state
  -> fade out
  -> placeholder arrival scene
  -> fade in
  -> player control restored
```

The first test does not need a custom actor model, a full quest log, or a time-transfer effect. It proves that our chosen placement, EventFlow edit, flags, and map transition work together.

## Files we will create later

Do not create these binary game files by hand yet. First identify a vanilla interaction and map cell to clone.

```text
source/romfs/
  Event/Flow/<chosen-vanilla-flow>.bfevfl
  Banc/MainField/<Forgotten-Temple-cell>_Static.bcett.byml.zs
  Pack/Actor/<chosen-chronolith-actor>.pack.zs
```

`<...>` is a deliberate placeholder, not a filename to guess. We will inspect the real file in the personal RomFS dump, copy only that file into the overlay, and then edit it.

## First flag registry

These are design names only. In Event Editor, map each one to a unique mod-owned game-data key after we inspect a native quest that uses compatible types.

| Design key | Type | Meaning |
| --- | --- | --- |
| `Echoes_FirstSage_Started` | bool | Link has activated the Chronolith. |
| `Echoes_FirstSage_HookComplete` | bool | The vertical-slice transfer completed. |
| `Echoes_FirstSage_AnchorRiver` | bool | Reserved for Act II. |
| `Echoes_FirstSage_AnchorTerrace` | bool | Reserved for Act II. |
| `Echoes_FirstSage_AnchorSky` | bool | Reserved for Act II. |
| `Echoes_FirstSage_Complete` | bool | The final archive sequence is complete. |

## Flowchart mockup

This is a structural plan, not a ready-to-import `.bfevfl` file.

```text
Entry: Chronolith_Interact
  |
  +-- Query: Echoes_FirstSage_Started?
  |     |
  |     +-- true  -> Action: display "The Chronolith is quiet."
  |     |
  |     +-- false -> Action: disable player input
  |                 -> Action: camera focus / short text
  |                 -> Action: set Echoes_FirstSage_Started = true
  |                 -> Action: FadeOut
  |                 -> Action: MapTransfer (temporary test destination)
  |                 -> Action: FadeIn
  |                 -> Action: enable player input
  |                 -> Action: set Echoes_FirstSage_HookComplete = true
  |                 -> End
```

## Acceptance test

The milestone is complete only when all of these are true:

1. The Chronolith can be interacted with exactly once.
2. The first interaction reaches the test destination without a softlock.
3. Player input returns after the fade-in.
4. Reloading the save does not restart the opening sequence.
5. The overlay contains only files modified by the project; no base-game data is copied into Git.

## Next concrete action

Use MapEditor to identify the Forgotten Temple map cell and a stable empty placement point. Then we will choose the smallest existing vanilla actor interaction to clone and open its corresponding EventFlow in TOTK Event Editor.
