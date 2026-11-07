# Burg Model Transfer Catalog

This catalog was captured from the live **The burg** Studio place (`placeId: 93189891893380`) on 2026-11-06. It is intended to support copying selected Burg buildings into Place1 and preserving recoverable `.rbxm` files in the Obsidian vault.

## Current transfer status

- The burg was connected during this audit.
- Place1 was not connected at the same time, so no cross-place paste was attempted.
- The Studio MCP connection can inspect and edit the DataModel but does not expose a local **Save Selection to File** command.
- Obsidian Markdown cannot reproduce Roblox Instances, CFrames, meshes, scripts or constraints by itself.
- A real model can still be stored in the vault as an attached `.rbxm` or `.rbxmx` file after it is exported from Studio.
- The prepared attachment directory is [[Model Exports/README]].

## Recommended export packages

Export separate packages instead of one enormous file. This keeps Place1 imports manageable and makes dependency problems easier to diagnose.

1. `Burg_InteractiveHouses.rbxm`
   - `Workspace.besthouse`
   - `Workspace.thetesthouse`
   - `Workspace.test house`
2. `Burg_ExteriorHouseCollection.rbxm`
   - All exterior-only houses and `SmallBlockApartment`
3. `Burg_TheVibe.rbxm`
   - `Workspace.The Vibe`
4. `Burg_MarketSquarePlaza.rbxm`
   - `Workspace.MarketSquarePlaza`
5. `Burg_LuxuryOnly.rbxm`
   - `Workspace.MarketSquarePlaza.Buildings.Luxury`
6. `Burg_SchaumburgHighSchool.rbxm`
   - `Workspace.Schaumburg High School`
7. `Burg_TownSquareAndRoads.rbxm`
   - `Workspace.SchaumburgTownSquare`
   - `Workspace.TownSquareNeighborhoodExpansion`
   - Road kit Models
8. `Burg_DreamWorld.rbxm`
   - `Workspace.BurgDreamWorld`

## Major top-level model inventory

Counts are live audit values. Dimensions are approximate bounding-box sizes in studs.

| Model | Parts | Models | Scripts | Prompts | Approx. size | Interior/status |
|---|---:|---:|---:|---:|---|---|
| `Schaumburg High School` | 18,699 | 363 | 16 | 153 | 695 × 63.4 × 972.6 | Complete interactive school, athletics and interiors |
| `MarketSquarePlaza` | 3,300 | 213 | 1 | 10 | 520 × 29.5 × 560 | Interior businesses and complete plaza site |
| `besthouse` | 2,849 | 161 | 5 | 64 | 55.9 × 59 × 69.5 | Most complete interactive player house |
| `thetesthouse` | 1,719 | 121 | 2 | 40 | 55.9 × 59 × 69.5 | Multi-floor interactive house variant |
| `BurgDreamWorld` | 1,105 | 39 | 1 | 1 | 201 × 67 × 201 | Complete dream environment and interior replica |
| `TimberGable_Exterior_v1` | 746 | 5 | 0 | 0 | 58 × 33.1 × 47.1 | Three floor/garage/porch shell; inspect before gameplay use |
| `test house` | 548 | 13 | 1 | 1 | 57.1 × 27.5 × 67.6 | Finished-interior test house with repaired layout folders |
| `The Vibe` | 458 | 27 | 9 | 5 | 41.4 × 12.5 × 57.3 | Complete interactive lounge, kitchen and bathrooms |
| `BeigeSplitLevelFillerHouse` | 416 | 0 | 0 | 0 | 82 × 25.6 × 103.2 | Polished exterior-only split level |
| `SageOffsetHouse_v2` | 344 | 5 | 0 | 0 | 62.5 × 29.3 × 59.2 | Offset suburban shell; inspect interior markers before use |
| `GrayGableTownhouse` | 336 | 0 | 0 | 0 | 59.7 × 29.4 × 101 | Polished exterior-only two-garage townhouse |
| `WhiteSplitLevelHouse` | 268 | 7 | 0 | 0 | 93.8 × 26.9 × 89.5 | Exterior-only split-level house |
| `SchaumburgTownSquare` | 266 | 24 | 0 | 0 | 150 × 59.3 × 141 | Civic plaza, fountain, clock tower and gateway |
| `thehouse` | 212 | 5 | 0 | 0 | 55.9 × 59 × 69.5 | Legacy three-floor house shell; inspect before transfer |
| `BlueDormerSuburbanHouse` | 201 | 6 | 0 | 0 | 71.9 × 26.8 × 86.5 | Exterior-only dormer house |
| `TealCraftsmanHouse` | 154 | 2 | 0 | 0 | 85.8 × 28.4 × 85.5 | Exterior-only craftsman with balcony and bay window |
| `TownSquareNeighborhoodExpansion` | 145 | 9 | 0 | 0 | 193.5 × 11.4 × 148.5 | Roads, sidewalks, parking and transit expansion |
| `SmallBlockApartment` | 114 | 1 | 0 | 0 | 70 × 31.9 × 56.5 | Exterior-only three-story apartment |
| `TwoStorySuburbanHouse` | 105 | 1 | 0 | 0 | 76.8 × 31.5 × 89 | Exterior-only porch/garage house |
| `RaisedRanchHouse` | 87 | 1 | 0 | 0 | 65 × 25.9 × 78.5 | Exterior-only raised ranch |
| `SplitLevelSuburbanHouse` | 81 | 1 | 0 | 0 | 71 × 27.4 × 84.1 | Exterior-only split level |
| `SimpleSuburbanHouse` | 80 | 2 | 0 | 0 | 62 × 21 × 82.6 | Exterior-only ranch/garage house |
| `roadtype1` | 56 | 2 | 0 | 0 | 96 × 1 × 194 | Composite road/intersection sample |
| `FourWayIntersection` | 38 | 0 | 0 | 0 | 96 × 1 × 96 | Standardized four-way road piece |
| `NOVA` | 36 | 0 | 4 | 1 | 0.6 × 0.9 × 0.4 | Interactive handheld Tool model, not a building |
| `RightTurnRoad` | 25 | 0 | 0 | 0 | 68 × 1 × 68 | Standardized right-turn road piece |
| `simple road` copy 1 | 18 | 0 | 0 | 0 | 40 × 1 × 98 | Standardized straight road |
| `simple road` copy 2 | 18 | 0 | 0 | 0 | 40 × 1 × 98 | Standardized straight road |

## Interactive interior buildings

### `Workspace.besthouse`

- Three floors with stairs, finished rooms, furniture, baseboards and railings.
- Current sections: `1st floor`, `2nd floor`, `3rd floor`, `WindowCoverings`, stair/railing parts and controller scripts.
- `1st floor`: 994 Parts, 70 Models and 21 prompts.
- `2nd floor`: 1,165 Parts, 58 Models and 22 prompts.
- `3rd floor`: 113 Parts, 15 Models and 3 prompts.
- Door, window, blind/curtain and desk-chair interactions.
- Player-bedroom systems include desk seating, wardrobe, sleep bed and computer area.
- Best choice when Place1 needs one fully playable home.

### `Workspace.thetesthouse`

- Same general three-floor shell and circulation as `besthouse`.
- `1st floor`: 890 Parts, 64 Models and 19 prompts.
- `2nd floor`: 694 Parts, 42 Models and 18 prompts.
- `3rd floor`: 113 Parts, 15 Models and 3 prompts.
- Interactive doors and windows, but less player-bedroom polish.

### `Workspace.test house`

- `ExteriorFinish`: 123 Parts and the front-door interaction.
- `FinishedInterior`: 209 Parts across 11 Models.
- `PolishedStructure`: 128 Parts.
- `RoomLayoutRepair`: 88 Parts.
- Useful as a smaller interior reference, but it has a history of layout repairs and should be reviewed before becoming a hero building.

### `Workspace.The Vibe`

- 458 Parts, 27 Models, 9 source containers, 5 prompts and 21 lights.
- Main sections: `Shell`, `Roof`, `ExteriorDetails`, `StringLights`, `Lounge`, `Kitchen`, `Cashier`, `BathroomExtension`, `PreparedFood`, and smoke state.
- `Lounge`: 98 Parts.
- `Kitchen`: 61 Parts and 2 prompts.
- `BathroomExtension`: 65 Parts, 2 scripts and 2 prompts.
- Entry/restroom doors, cashier dialogue, fridge interaction, cooking/serving behavior and room-smoke simulation.
- This model includes several internal modules, but its smoke visuals and some gameplay services also depend on scripts outside the Model.

### `Workspace.Schaumburg High School`

- Largest transfer candidate: 18,699 Parts and a 695 × 63.4 × 972.6-stud footprint.
- `Interior`: 6,898 Parts, 278 Models and 145 prompts.
- `RearAthletics`: 9,764 Parts, 49 Models, 2 scripts and 2 prompts.
- `CampusParkingFinish`: 799 Parts.
- `CampusExteriorLighting`: 567 Parts and one controller.
- Includes classrooms, offices, cafeteria, gym, bathrooms, scanners, athletics, stadium, parking and smoke regions.
- Import separately and place carefully; it is too large to combine casually with another package.

## Market Square Plaza and businesses

### Whole plaza

- Path: `Workspace.MarketSquarePlaza`.
- 3,300 Parts, 213 Models, one internal source container, 10 prompts, 54 lights and 333 GUI containers.
- Size: approximately 520 × 29.5 × 560 studs.
- Sections: `Buildings`, `Parking`, `Landscaping`, and `Site`.

### Luxury

- Path: `Workspace.MarketSquarePlaza.Buildings.Luxury`.
- 1,336 Parts, 125 Models, one script and 4 prompts.
- Size: approximately 91 × 22.1 × 85.6 studs.
- Exterior includes brick piers, aluminum mullions, storefront glass, cornice, parapets, rooftop units, louvers and two entry assemblies.
- `Interior` contains the sales floor, displays/stock, employee areas, stockroom and staff bathroom.
- Best single-store transfer candidate for Place1.
- Store purchasing, inventory and worker behavior also rely on external Luxury/Equipment Bag scripts.

### Subway

- 235 Parts, 9 Models and 4 prompts.
- Approximately 71 × 22.1 × 85.6 studs.
- Full storefront shell and an `Interior` Model, entries, rooftop units, louvers and opening-hours signage.

### Walgreens

- 901 Parts, 25 Models and 2 prompts.
- Approximately 111 × 22.1 × 136.9 studs.
- Full `Interior`, storefront, entries, pharmacy fascia, delivery door, bollards and rooftop details.

### Other plaza shells

- `Mobil`: 80 Parts, approximately 146 × 29.5 × 88 studs.
- `Mobil closed service building`: 52 Parts.
- `Dominos closed storefront`: 54 Parts.
- Four numbered closed storefronts: 51 Parts each.
- `West closed pad`: 51 Parts, approximately 121 × 22.1 × 66.6 studs.

## Exterior house collection

The strongest finished exterior-only references are:

- `BeigeSplitLevelFillerHouse`: six organized exterior folders, garage wing, solar array and polished roof/wall transitions.
- `GrayGableTownhouse`: two garages, recessed entry, rear patio, chimney, gutters and complete gables.
- `TealCraftsmanHouse`: balcony, bay window, stone entry panel, attached garage and layered roof closure.
- `BlueDormerSuburbanHouse`: separate front/rear exterior and finish-detail Models.
- `WhiteSplitLevelHouse`: front/rear exterior, garage addition/polish and landscaping.
- `TwoStorySuburbanHouse`: porch railings/columns, attached garage, chimney and multiple second-floor windows.
- `RaisedRanchHouse`: elevated entry, seven steps, railings, lower brick level and garage.
- `SplitLevelSuburbanHouse`: entry connector, garage wing, picture window and separate roof groups.
- `SimpleSuburbanHouse`: compact ranch shell with garage, chimney and exterior upgrade Model.
- `SmallBlockApartment`: two entries, three window levels, brick wings, side/rear elevations and utility boxes.

## Gameplay dependencies that do not travel with a Model

Copying only a Workspace Model preserves its descendants, but not unrelated services elsewhere in the place.

- `besthouse`: also uses Burg wardrobe, sleep, desk-seating and front-end/save systems.
- Luxury: also uses `LuxuryStoreServer`, `LuxuryStoreClient`, Equipment Bag catalogs/templates, currency and XP systems.
- Market Square doors: use `ServerScriptService.MarketSquarePlazaDoors`.
- The Vibe: smoke visuals live in StarterPlayerScripts; server smoke emission and some shared gameplay systems live outside the Model.
- Schaumburg High School: football services/input, basketball input, room-smoke visuals and some school services exist outside the school Model.
- BurgDreamWorld: entry/exit, client transitions and save/state handling live in Burg Dream services outside the Model.
- Door, prompt, inventory, currency, XP and data-save dependencies should be transferred as code packages only after conflict review.

For a visual Place1 map, import the Models first with scripts disabled or removed. Transfer gameplay systems separately after matching ReplicatedStorage, ServerStorage, ServerScriptService and StarterPlayerScripts dependencies.

## Safe transfer order into Place1

1. Back up Place1.
2. Import exterior-only house collection.
3. Import The Vibe and Luxury as visual buildings first.
4. Import one interactive house and test doors/windows before adding another.
5. Import Market Square Plaza only if Place1 has a 520 × 560-stud clear site.
6. Import the high school last into a dedicated 700 × 975-stud zone.
7. Resolve duplicate script, RemoteEvent, catalog and DataStore names before enabling gameplay.
8. Re-run anchored-part, invisible-collider, prompt, script-error and performance audits.

## Exact-model storage in Obsidian

Obsidian can store and link `.rbxm`/`.rbxmx` attachments, but it cannot preview or edit them as Roblox objects. Export files into:

`C:\Users\Daniel\Documents\Obsidian Vault\Roblox Development Reference\Model Exports`

Then link them from this note using ordinary Obsidian file links. Keep this Markdown catalog even after exporting because it records dependencies that the model file itself does not explain.
