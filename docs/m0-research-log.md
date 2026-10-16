# M0 Research Log - Forgotten Temple Entry

## What was verified

The private reference dump contains the expected surface-map placement layout:

    Banc/MainField/<grid>_Static.bcett.byml.zs
    Banc/MainField/<grid>_Dynamic.bcett.byml.zs

It also contains an EventFlow directory and several files whose names reference the Lost Temple. This confirms that the project can base its first edit on real game data without importing the full dump into this repository.

## Candidate references

These are investigation leads only. They have **not** been copied, changed, or selected as the mod's base flow:

- Event/EventFlow/Npc_Wanderer_LostTemple.bfevfl.zs
- Event/EventFlow/Npc_Kakariko005_LostTemple.bfevfl.zs

The correct selection must be made only after opening each candidate in TotK Event Editor and confirming that it has a small, safe inspection or camera/fade pattern to reuse. A story NPC flow is not automatically a good implementation base.

## Next required observation

The exact Forgotten Temple grid and a non-blocking entrance transform still need to be recorded from MapEditor. Record all of the following before editing any map data:

1. MainField grid label, for example 'X-N'.
2. Position X, Y, Z.
3. Rotation X, Y, Z.
4. Whether the actor belongs in the static or dynamic cell.
5. A screenshot or written note showing that the entrance neither blocks existing geometry nor traps the player.

## Approved visual placement

The entrance is approved on the **large blank interior wall above the circular-room ledge**, centered between the two central stone pillars. The intended feature occupies the broad masonry panel rather than an existing arch, doorway, or traversal route.

The placement is in MainField cell **D-2**. The vanilla actor Npc_Wanderer_LostTemple at position (-953.568, 32.945, -2822.111) is a visual reference point only. It is an existing NPC, not a temporary object and not an approved actor template. It must remain unchanged in both the map data and the final mod.

For the first playable build, treat this as a **flush sealed archive door** with a nearby interactable Chronolith element. Do not cut a physical opening through the temple mesh yet. A flush, visibly dormant door lets us validate placement, interaction range, event flow, and save persistence without risking collision holes or broken navigation. The later reveal can swap or animate authored door-state geometry after the baseline loop is stable.

### Placement guardrails

- Keep the lower ledge traversable and leave both adjacent arches unobstructed.
- Position the interaction point at reachable ledge height; never require climbing a decorative wall.
- Keep the door's collision shallow until the future interior transfer is confirmed.
- Place the temporary Chronolith interaction point slightly in front of the wall, never inside static collision.

## Source-control boundary

The reference RomFS remains private and outside this repository. After the target grid and base flow are verified, copy only the edited overlay file or files into source/romfs/ while preserving their exact game-relative paths.

## First visual probe

The first actor to preview, without saving, is CaveObj_RuinZonau_Shutter_B_01. It is a candidate because it is a separate Zonai-ruin shutter actor rather than a vanilla NPC or an already scripted door. Add it as a **Static** actor in D-2, initially at the recorded reference point, then inspect its orientation, scale, and collision visually.

This is a probe only. Do not overwrite Npc_Wanderer_LostTemple, and do not save the D-2 map until the actor is confirmed to fit the wall and a separate interaction method has been chosen.

### Probe result: CaveObj_RuinZonau_Shutter_B_01

The actor was centered successfully at (-953.500, 33.000, -2821.500) with rotation (0.000, -41.000, 0.000) and scale (1.000, 1.000, 1.000). The offset holds the object slightly in front of the wall, which is the desired placement behavior.

The art result is rejected for the final entrance: its vertical green bars read as a conventional gate, not a concealed Chronolith archive seal. Retain the transform as a dimensional reference only. The next uncommitted preview candidate is DgnObj_Zonau_Shutter_A_01.
