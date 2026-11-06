# Roblox Project Reference — The burg

This folder summarizes both the Roblox Studio work discussed in chat and a read-only audit of the live place. It is the central reference for continuing development of **The burg** (`placeId: 93189891893380`). The live audit was captured on **2026-11-04**.

## Project direction

- Avatar rig: **R6**.
- Visual style: polished, readable Roblox geometry rather than ultra-detailed meshes.
- Props should be optimized, smoothly aligned, and suitable for gameplay.
- Houses used as neighborhood filler should normally be **exterior-only and hollow**.
- Interactive handheld items should be Tools that can be picked up, equipped, animated, and used on desktop and mobile.

## Reference notes

- [[01 - Pulse Bar Models and Visual Design]]
- [[02 - Pulse Bar Interaction and R6 Animation]]
- [[03 - Pulse Sounds Smoke and Head Rush Effects]]
- [[04 - MXK MuhaMed Tamu and Blinker Systems]]
- [[05 - Roads Sidewalks and Map Pieces]]
- [[06 - House Building Standards]]
- [[07 - House and Building Catalog]]
- [[08 - Bugs Fixes and Lessons Learned]]
- [[09 - Currency XP and Game Systems]]
- [[10 - Roblox Script Architecture]]
- [[11 - Reusable Model Prompts and Specifications]]
- [[12 - Live Game Inventory]]
- [[13 - Live Tool Reference Cards]]
- [[14 - Live Buildings Roads and Locations Audit]]
- [[15 - Live Script and System Register]]
- [[16 - Exact Gameplay Values and Data Contracts]]
- [[17 - Backups Duplicates and Maintenance Notes]]
- [[18 - Roblox Development Reflection Log]]
- [[19 - The Burg Game Ideas]]
- [[20 - Roblox Game Development Playbook]]
- [[21 - XP Gain Bar Reference]]

## Which notes to use

- Use notes `01`–`11` for design history, requested behavior, and reusable building standards.
- Use notes `12`–`17` for the current live Studio hierarchy and implementation details.
- If an older design note disagrees with the live audit, treat the live audit as the current implementation and verify it in Studio before changing code.
- Before new Roblox work, review the relevant notes and the reflection log. After verified changes, append a reflection entry so future work can reuse the implementation and lessons.

## Important current systems

Future feature ideas and a first delivery milestone are in [[19 - The Burg Game Ideas]].
Research, Luau examples, asset workflows and release checks are in [[20 - Roblox Game Development Playbook]].

- All Pulse Bars use a completed-hit event, screen counters, R6 holding animation, smoke, sound, and a shared head-rush screen effect.
- Desktop ProximityPrompts are prevented from capturing the first-person mouse.
- MXK and MuhaMed use the Oil display and long-hold Blinker system.
- Roads use standardized dimensions so straight roads, turns, and intersections align.
- The newest filler house is `Workspace.BeigeSplitLevelFillerHouse`.
- `Workspace.GrayGableTownhouse` was rebuilt as a hollow exterior-only model. A prior interior version was backed up in `ServerStorage`.

## Naming rule

Keep models, folders, scripts, RemoteEvents, attachments, and important parts descriptively named. Avoid unnamed Parts and duplicate generic folders. Each finished house should contain organized folders such as:

- `ExteriorShell`
- `Roofs`
- `WindowsAndDoors`
- `ExteriorTrim`
- `ExteriorDetails`
- `Site`

