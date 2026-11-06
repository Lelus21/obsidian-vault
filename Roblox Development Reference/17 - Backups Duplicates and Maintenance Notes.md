# Backups, Duplicates, and Maintenance Notes

## Active code versus backups

`ServerStorage` contains dated snapshots and older copies. They are useful for recovery but should not be treated as live code. Observed backup groups include:

- `SchoolPolish_20261023`
- `SchoolBathroomUpgrade_20261023`
- `StallInsideControlsBackup`
- `SchoolSmokeRetuneBackup`
- multiple `FootballBefore...` snapshots
- `WardrobeBeforeFirstPersonFix_20261103`
- `WardrobeBeforeCursorLockFix_20261103`
- `BeforeStorySaves_20261103`
- `BeforeDreamTravel_20261104`
- `DreamBeforeOpenFloor_20261104`

Active production scripts live in ServerScriptService, StarterPlayerScripts, ReplicatedStorage, or the active Workspace models described in [[15 - Live Script and System Register]].

## Deliberate shared-source groups

- All standard Pulse `PickupHandler` scripts are identical.
- All standard Pulse `ScreenUseCounter` scripts are identical.
- Most Pulse `HeldVisualAnimator` scripts are identical; Fab and `test test` share the side-star-pulse extension.
- `besthouse` and `thetesthouse` share the same house door and window controller sources.
- The Vibe entry and both restroom doors share one door-controller source.
- School and The Vibe food factories share the same procedural factory source.

When fixing a shared system, update the source templates and every live copy, or consolidate into a ModuleScript where practical.

## Equipment template drift risk

There are two versions of each bag item:

1. the Workspace world/reference Tool;
2. the production clone under `ServerStorage.EquipmentBagTools`.

Before publishing a change, compare scripts, attributes, sounds, SurfaceGuis, Remotes, WeldConstraints and grip properties. A Workspace-only fix will not automatically reach a Tool granted from the Equipment Bag.

## Naming issues worth cleaning later

- `dragon melo pulse` and `dragon melon pulse` are different live Tools; the first appears to be an unregistered alternate variant.
- `test test` is a finished Pulse implementation with experimental naming.
- `test house`, `thehouse`, `thetesthouse`, and `besthouse` are hard to distinguish outside Studio context.
- Two top-level Models share the name `simple road`.
- Several older houses contain generic `Part` names.
- `penjamin.MuhaMed backup` still uses the old `BatteryDisplayController` naming even though production MuhaMed is oil-only.

Rename only with a reference audit because scripts and catalog entries use exact names.

## Performance attention points

- High school: 20,175 descendants and 18,227 Parts.
- Plaza: 14,961 descendants plus thousands of UI Frames/UICorners on SurfaceGuis.
- ServerStorage: 6,992 descendants from templates and backups.
- `besthouse`: 3,026 descendants.
- Pulse Tools: 186 descendants each, largely from display/constellation UI.

Potential future optimization work:

- Stream or region-load the high school/plaza if the whole map becomes active at once.
- Replace repeated static decorative Parts with meshes only where visual quality is preserved.
- Avoid running inactive location controllers every frame.
- Keep smoke Parts short-lived and use the existing Debris cleanup.
- Archive old backups outside the production place after exporting a safe copy.
- Consider consolidating duplicated Tool scripts into shared modules, while keeping client/server boundaries intact.

## Safe change checklist

1. Confirm whether the target is a Workspace reference, a ServerStorage template, or both.
2. Preserve `Handle`, grip, attachment, RemoteEvent and prompt names expected by scripts.
3. Preserve R6 assumptions unless intentionally adding R15 support.
4. Keep server validation for resources, cooldowns, streaks and XP.
5. Test desktop first-person prompts, mouse lock, touch controls and gamepad actions.
6. Check title/phone/wardrobe camera overrides after changing camera or FOV code.
7. Test room smoke in both The Vibe and school rooms after changing emissions.
8. Test save behavior in a published test place with API Services; Studio XP is intentionally session-only.
9. Verify that temporary UI, IK, BindToRenderStep connections, smoke and effects clean up on unequip, death and destruction.
10. Update this vault after shipping a substantial system change.
