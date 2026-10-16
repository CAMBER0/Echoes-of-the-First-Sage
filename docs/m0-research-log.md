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

For the first playable build, treat this as a **flush sealed archive door** with a nearby interactable Chronolith element. Do not cut a physical opening through the temple mesh yet. A flush, visibly dormant door lets us validate placement, interaction range, event flow, and save persistence without risking collision holes or broken navigation. The later reveal can swap or animate authored door-state geometry after the baseline loop is stable.

### Placement guardrails

- Keep the lower ledge traversable and leave both adjacent arches unobstructed.
- Position the interaction point at reachable ledge height; never require climbing a decorative wall.
- Keep the door's collision shallow until the future interior transfer is confirmed.
- Place the temporary Chronolith interaction point slightly in front of the wall, never inside static collision.

## Source-control boundary

The reference RomFS remains private and outside this repository. After the target grid and base flow are verified, copy only the edited overlay file or files into source/romfs/ while preserving their exact game-relative paths.
