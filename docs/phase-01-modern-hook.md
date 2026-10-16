# Phase 1 - Chronolith Trial Vertical Slice

## Goal

Build one small, safe playable loop before authoring a regional rift or the final dungeon:

    Eligible save
      -> discover Forgotten Temple sealed stair
      -> inspect Archive of Hours
      -> complete three-room Chronolith Trial
      -> unlock Echo Trace
      -> save, reload, and re-enter safely

This milestone proves placement, EventFlow state, map transfer, persistence, and one explicitly registered Echo Trace target. It does **not** require a custom actor model, a complete quest log, a new ability wheel slot, or a full open-world time effect.

## Files we will create after inspection

Do not invent binary filenames. First inspect the personal RomFS dump, identify a compatible vanilla actor/interaction and the real Forgotten Temple map cell, then copy only the required files into the overlay.

    source/romfs/
      Event/Flow/<verified-vanilla-flow>.bfevfl
      Banc/MainField/<verified-temple-cell>_Static.bcett.byml.zs
      Pack/Actor/<verified-chronolith-or-prop>.pack.zs

The angle-bracket labels mean “verify in the private dump first,” never “guess a filename.” The repository receives only the changed overlay files, never the complete RomFS.

## Chosen entrance composition

The sealed Archive of Hours entrance belongs on the large blank masonry panel above the Forgotten Temple's circular-room ledge, centered between the inner pillars. Phase 1 uses a flush sealed door and a small, reachable interaction point in front of it. The player transfers to the trial instance after the Chronolith scene; Phase 1 does not attempt to cut a real hole into the existing temple mesh.

## Vertical-slice state flow

This is a structural mockup for Event Editor, not an importable .bfevfl.

    Entry: ForgottenTemple_ArchiveTrigger
      |
      +-- Query: Q00 prerequisites satisfied?
      |     |
      |     +-- false -> Action: retain normal temple behavior
      |     |
      |     +-- true  -> Query: EotAH_ArchiveDiscovered?
      |                   |
      |                   +-- false -> Action: reveal or enable sealed-stair interaction
      |                   |           -> Action: set EotAH_ArchiveDiscovered = true
      |                   |           -> End
      |                   |
      |                   +-- true  -> Entry: Chronolith_Interact
      |
      +-- Query: EotAH_EchoTraceUnlocked?
            |
            +-- true  -> Action: show repeat / rift guidance
            |
            +-- false -> Action: lock player input
                        -> Action: camera and Archive of Hours text
                        -> Action: set EotAH_ChronolithTrialStarted = true
                        -> Action: FadeOut
                        -> Action: MapTransfer (verified trial instance)
                        -> Action: FadeIn
                        -> Action: restore player input
                        -> Entry: Trial_Room_Recall

    Entry: Trial_Room_Recall
      -> Action: activate one authored target
      -> Query: target restored?
      -> true -> Entry: Trial_Room_Ultrahand

    Entry: Trial_Room_Ultrahand
      -> Query: route completed?
      -> true -> Entry: Trial_Room_Sentinel

    Entry: Trial_Room_Sentinel
      -> Query: sentinel resolved?
      -> true -> Action: set EotAH_EchoTraceUnlocked = true
              -> Action: set EotAH_ChronolithTrialComplete = true
              -> Action: unlock five rift signals
              -> Action: return to verified Archive of Hours arrival point
              -> End

## Test contract

The vertical slice is complete only when all of these are true:

1. An ineligible save cannot start the DLC path or corrupt normal Forgotten Temple behavior.
2. An eligible save discovers the stair and can resume after saving/reloading.
3. The Chronolith transfer fades out and back in without softlocking player input.
4. Each tutorial room persists only its required completion state.
5. Echo Trace affects the one registered target and ignores all nearby unregistered objects.
6. Completing the trial reveals the five rift signals exactly once.
7. The Git overlay contains only changed project files; no full game data, keys, or extracted assets are committed.

## First editor task

In MapEditor, identify and write down the exact Forgotten Temple placement cell and a safe, non-blocking location for the sealed-stair entrance. In Event Editor, locate a small vanilla interaction with a compatible inspection/camera/fade pattern. Only after those two items are verified should we duplicate data into source/romfs/.
