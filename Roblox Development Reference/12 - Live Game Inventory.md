# Live Game Inventory

Read-only Studio audit captured **2026-11-04** from **The burg** (`placeId: 93189891893380`). No game objects were changed during the audit.

## Place-level structure

- `Workspace`: 48 top-level objects at audit time.
- `ReplicatedStorage`: 918 descendants.
- `ServerStorage`: 6,992 descendants, including production equipment templates and dated backups.
- `ServerScriptService`: 13 descendants: 8 Scripts, 4 ModuleScripts, and 1 BindableEvent.
- `StarterPlayerScripts`: 18 active LocalScripts.
- `StarterPack`: one `Phone` Tool with 14 descendants.
- `StarterGui`: empty; runtime interfaces are constructed by LocalScripts.
- `Lighting`: Sky, Atmosphere, Bloom, SunRays, and DepthOfField.
- Avatar and handheld animation target: R6.

## Workspace Tools

There are 13 top-level Tools:

| Tool | Bounds in studs | Descendants | Main resource |
|---|---:|---:|---|
| `ACE` | 0.4 × 0.8 × 0.3 | 30 | Oil/Blinker |
| `MXK` | 0.4 × 0.8 × 0.3 | 26 | Oil/Blinker |
| `MuhaMed` | 0.4 × 1.0 × 0.5 | 33 | Oil/Blinker |
| `NOVA` | 0.6 × 0.9 × 0.4 | 85 | Oil/Blinker + visible reservoir |
| `blue razz blast pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `dragon melo pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `dragon melon pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `Fab pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `Green pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `Meta moon pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `Miami Mint pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `Minneapolis Mint pulse` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |
| `test test` | 1.0 × 1.5 × 0.5 | 186 | Battery/Juice |

See [[13 - Live Tool Reference Cards]] for components, colors, scripts, and exact behavior.

## Major locations

| Workspace model | Bounds in studs | Descendants | Purpose |
|---|---:|---:|---|
| `Schaumburg High School` | 695.0 × 63.4 × 972.6 | 20,175 | Complete school campus, rooms, gym, cafeteria, bathrooms, football/stadium systems |
| `MarketSquarePlaza` | 520.0 × 29.5 × 560.0 | 14,961 | Retail plaza with Luxury, Subway, Walgreens, parking and landscaping |
| `BurgDreamWorld` | 201.0 × 67.0 × 201.0 | 1,667 | Dream map, cloud forms, dream bed, exit, XP trader |
| `The Vibe` | 41.4 × 12.5 × 57.3 | 549 | Lounge/store, cashier, food service, restrooms, room-smoke simulation |
| `SchoolFootball` | 188.0 × 71.0 × 388.0 | 9 | Football field boundary and interactive football |

## Houses and neighborhood buildings

| Model | Bounds in studs | Descendants | Interior state |
|---|---:|---:|---|
| `BeigeSplitLevelFillerHouse` | 82.0 × 25.6 × 103.2 | 426 | Organized exterior-only filler |
| `BlueDormerSuburbanHouse` | 71.9 × 26.8 × 86.5 | 213 | Exterior model |
| `GrayGableTownhouse` | 59.7 × 29.4 × 101.0 | 349 | Organized exterior-only filler |
| `RaisedRanchHouse` | 65.0 × 25.9 × 78.5 | 91 | Exterior model |
| `SageOffsetHouse_v2` | 62.5 × 29.3 × 59.2 | 349 | Exterior model |
| `SimpleSuburbanHouse` | 62.0 × 21.0 × 82.6 | 84 | Exterior model |
| `SmallBlockApartment` | 70.0 × 31.9 × 56.5 | 117 | Exterior apartment block |
| `SplitLevelSuburbanHouse` | 71.0 × 27.4 × 84.1 | 84 | Exterior model |
| `TealCraftsmanHouse` | 85.8 × 28.4 × 85.5 | 160 | Exterior model |
| `TimberGable_Exterior_v1` | 58.0 × 33.1 × 47.1 | 751 | Exterior timber-gable build |
| `TwoStorySuburbanHouse` | 76.8 × 31.5 × 89.0 | 109 | Exterior model |
| `WhiteSplitLevelHouse` | 93.8 × 26.9 × 89.5 | 282 | Exterior model with garage polish |
| `test house` | 57.1 × 27.5 × 67.6 | 577 | Finished interior/exterior test build |
| `thehouse` | 55.9 × 59.0 × 69.5 | 221 | Three-floor shell/older house |
| `thetesthouse` | 55.9 × 59.0 × 69.5 | 1,911 | Interactive interior house |
| `besthouse` | 55.9 × 59.0 × 69.5 | 3,026 | Most complete player house; doors, windows, coverings, bedroom PC, wardrobe and sleep interactions |

The two largest house interiors use `1st floor`, `2nd floor`, and `3rd floor` models. `besthouse` has 62 ProximityPrompts; `thetesthouse` has 40.

## Other Workspace objects

- `PhoneModel`: 0.5 × 1.0 × 0.3, with `Base`, `Screen`, `Earpiece`, `Camera`, `CameraLens`, and `CameraLensRing` Parts.
- `npc`: classic six-Part block NPC; its Head contains two additional descendants.
- `penjamin`: folder with `backup MKX` (7 descendants) and `MuhaMed backup` (19 descendants). The MuhaMed copy still contains the older `BatteryDisplayController`.
- `Pulse bars`: folder containing a seven-descendant `purple pulse` Model.
- `RoadConnectors`: folder with connector templates and a `SNAP_GUIDE` StringValue.
- `Baseplate`: 2,048 × 16 × 2,048.
- `SpawnLocation`: 12 × 1 × 12.

## Runtime-created folders and interfaces

Several systems create content only while playing:

- `PulseSmokeEffects` and `MXKSmokeEffects` in Workspace for temporary smoke Parts.
- `PulseHitGui`, `MXKBlinkerGui`, Equipment Bag UI, XP UI, phone UI, title UI, sleep UI, and smoke overlays in `PlayerGui`.
- `PulseHeadRushBlur` and `PulseHeadRushColor` in Lighting.
- Player folders/attributes such as `ToolXP`, `EquipmentBagInventory`, story slot state, and camera/UI settings.
