# Echoes of the Ancient Hero - Flag Registry

## Status

These are **design identifiers**, not confirmed game-data keys. Before adding any flag to a .bfevfl or game-data file, inspect a native quest with the same data type and persistence behavior. Preserve its naming, lifecycle, and reset conventions.

All keys below are intended as persistent booleans unless a later implementation note says otherwise.

## Main progression

| Design key | Set when | Used to |
| --- | --- | --- |
| 'EotAH_PrerequisitesMet' | The prerequisite query passes. | Permit the temple rumor/entrance. |
| 'EotAH_ArchiveDiscovered' | Link finds the sealed stair or Archive of Hours. | Keep the entrance state after reload. |
| 'EotAH_ChronolithTrialStarted' | The first Chronolith scene begins. | Recover safely from a mid-trial save. |
| 'EotAH_Trial_RecallComplete' | The Recall room resolves. | Allow the Ultrahand room to start. |
| 'EotAH_Trial_UltrahandComplete' | The construction route is completed. | Allow the Sentinel room to start. |
| 'EotAH_Trial_SentinelComplete' | The Sentinel is resolved. | Grant the trial completion safely. |
| 'EotAH_ChronolithTrialComplete' | The three tutorial rooms resolve. | Stop replaying the unlock scene. |
| 'EotAH_EchoTraceUnlocked' | The trial completion reward is granted. | Enable registered Echo Trace interactions. |
| 'EotAH_FiveRiftsRevealed' | The trial exit returns control. | Show rift guidance once. |
| 'EotAH_FinalLiftUnlocked' | All five seals are present. | Enable the Citadel entrance. |
| 'EotAH_HollowChampionCleared' | The finale boss resolves. | Gate finale/replay/postgame behavior. |
| 'EotAH_EchoCovenantUnlocked' | The final reward is granted. | Enable the upgraded registered targets. |
| 'EotAH_PostgameUnlocked' | The epilogue finishes. | Enable relic trails, rematches, and time trials. |

## Regional chapter template

Each chapter uses the same state shape. The placeholders below are expanded for Ember, Tide, Verdant, Dune, and Gale.

| Design key pattern | Set when | Used to |
| --- | --- | --- |
| 'EotAH_Rift_<Region>_Discovered' | Link first enters/interacts with that rift. | Intro dialogue and map state. |
| 'EotAH_Rift_<Region>_Checkpoint_<N>' | A safe authored checkpoint is reached. | Restore a re-entry point after defeat/exit. |
| 'EotAH_Rift_<Region>_BossCleared' | The region guardian is resolved. | Prevent boss respawn except through replay. |
| 'EotAH_Seal_<Region>_Acquired' | The seal reward scene finishes. | Check final-lift condition. |
| 'EotAH_Memory_<Region>_Viewed' | The memory scene finishes. | Prevent duplicate story playback. |

Concrete region suffixes:

    Ember     Furnace Heart / Death Mountain
    Tide      Deep Current / Lanayru
    Verdant   Living Canopy / Faron
    Dune      Glass Dunes / Gerudo
    Gale      Storm Choir / Hebra

## Final-dungeon and safety state

| Design key | Set when | Used to |
| --- | --- | --- |
| 'EotAH_CitadelEntered' | The Last-Hour lift transfer finishes. | Initialize finale re-entry behavior. |
| 'EotAH_CitadelCheckpoint_<N>' | A safe final-dungeon checkpoint is reached. | Resume after defeat or voluntary exit. |
| 'EotAH_HollowChampionPhase_<N>' | A stable boss phase boundary is reached. | Restore a supported boss checkpoint only. |
| 'EotAH_Reward_MantleGranted' | Cosmetic reward delivery finishes. | Make reward delivery idempotent. |
| 'EotAH_Reward_MedallionGranted' | Key-item delivery finishes. | Make reward delivery idempotent. |

## Implementation rules

1. Never set a completion flag before the scene, item grant, map transfer, or save-safe checkpoint it represents has completed.
2. Make reward delivery idempotent: reloading after a reward scene must never duplicate an item.
3. Test every flag with a new eligible save, a reload during the relevant sequence, an exit from the relevant rift, and a post-final-boss save.
4. Do not put placeholder names directly into game data. Replace each with a verified native-compatible key only when its source file and behavior have been inspected.
