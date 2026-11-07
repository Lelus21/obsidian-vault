# Place1 Schaumburg Town Base

This note documents the large editable town foundation created in the separate Roblox Studio project named **Place1** on 2026-11-06.

## Root model

- Studio path: `Workspace.SchaumburgTownBase`
- PrimaryPart: `Workspace.SchaumburgTownBase.11_MapConnectors.TownPivot`
- Style attribute: `TownStyle = SchaumburgInspired`
- Planned map size attribute: `MapSize = 900`
- Audited bounds after the polish pass: approximately `966 × 100.1 × 902` studs
- Audited center: approximately `(-2.5, 35.5, 0)`
- Current contents after the Burg-style building rebuild: `3,666` BaseParts and `219` Models
- Structural audit: all parts anchored; no invisible colliders

## Folder organization

1. `01_Roads`
2. `02_SidewalksAndCurbs`
3. `03_BlockFoundations`
4. `04_TownSquare`
5. `05_CommercialDistrict`
6. `06_CivicDistrict`
7. `07_ResidentialDistrict`
8. `08_ParkingAndTransit`
9. `09_Landscaping`
10. `10_StreetFurniture`
11. `11_MapConnectors`

## Road grid

The map uses the established town-road profile from [[05 - Roads Sidewalks and Map Pieces]].

- `SchaumburgBoulevard`: north/south, 44 studs wide, centered at `X = 0`.
- `TownSquareDrive`: east/west, 44 studs wide, centered at `Z = 0`.
- `WestNeighborhoodRoad`: north/south, 32 studs wide, centered at `X = -260`.
- `EastNeighborhoodRoad`: north/south, 32 studs wide, centered at `X = 260`.
- `NorthCommercialRoad`: east/west, 32 studs wide, centered at `Z = 260`.
- `SouthResidentialRoad`: east/west, 32 studs wide, centered at `Z = -260`.
- Sidewalks are segmented around all sixteen blocks and are 5 studs wide.
- Main-road crosswalks, yellow dashed center markings, white edge lines, raised curbs and traffic signals are already installed.

### Expansion connectors

Each invisible marker contains a `RoadSnap` Attachment:

- `NorthTownConnector` at approximately `(0, 0.45, -450)`.
- `SouthTownConnector` at approximately `(0, 0.45, 450)`.
- `WestTownConnector` at approximately `(-450, 0.45, 0)`.
- `EastTownConnector` at approximately `(450, 0.45, 0)`.

New roads should continue the same centerline, elevation and width from these markers.

## Town square

Path: `04_TownSquare.VeteransGatewayTownSquare`

- Large brick civic plaza in the central northeast block.
- `CentralFountain` with lower basin, illuminated water, center column, upper bowl and eight water jets.
- `BrickClockTower` with red-brick shaft, limestone bands, four clock displays and green metal roof.
- `VeteransGateway` with brick piers, teal posts and a segmented arch labeled `SCHAUMBURG TOWN SQUARE`.
- Internal concrete walks, planters, benches, trees, bike racks and warm street lighting.

The invisible SpawnLocation is positioned near the plaza entrance at approximately `(58, 1.1, 58)`. Play mode placed the character safely on the brick plaza.

## Commercial buildings

Every shop is an exterior-only Model with a foundation, four-wall shell, roof, storefront glass, front door, awning and readable sign. They can be replaced individually with interactive interiors later.

- `PulseLuxury`
- `TownCafe`
- `WoodfieldMarket`
- `FreshGrocer`
- `SchaumburgPharmacy`
- `VillageDiner`
- `TechAndGames`
- `FitnessCenter`
- `CommunityBank`
- `FamilySalon`
- `AutoService`
- `BooksAndMore`

Shared parking areas include painted spaces, drive aisles and nearby sidewalks.

## Civic district

- `SchaumburgMunicipalHall`
- `PublicLibrary`
- `FireStation`
- `CommunityClinic`
- `SchaumburgHighSchool`

These are organized exterior shells with glass entries, signs, canopies, parking/aprons and room for future gameplay interiors.

## Residential district

- Ten varied exterior-only suburban houses with garages, driveways, front walks, roof forms, windows, porch lights and coordinated colors.
- `TownCenterApartments`: three-story exterior apartment shell with repeated windows, entry and sign.

The houses are intentionally filler-ready. They can remain hollow for performance or be replaced one at a time with playable interiors.

## Transit and street details

- Four `TOWN LOOP` glass bus shelters.
- Main-intersection traffic signals.
- Street-name signs at the central and secondary intersections.
- Warm streetlights along both major boulevards.
- Benches, bike racks, planters and approximately 120 landscaping groups.
- Daytime Lighting, Atmosphere and `TownColorGrade` were configured for a warm suburban presentation.

## Continuation rules

- Preserve the root Model and numbered folder structure.
- Snap neighborhood extensions to the four `RoadSnap` Attachments.
- Keep secondary roads at 32 studs and major boulevards at 44 studs.
- Keep sidewalks at 5 studs for this Place1 map.
- Put new buildings into the correct district folder and give each building a descriptive Model name.
- Prefer exterior-only shells until a building needs gameplay.
- Add interiors as separate child Models so the filler exterior can remain reusable.
- Maintain clear sightlines near intersections; do not place trees or signs inside crosswalk corners.

## Full polish pass

The town received a second full visual pass on 2026-11-06 after the original fountain, clock tower, tree scatter and open southern blocks were judged too basic.

### Fountain rebuild

`04_TownSquare.VeteransGatewayTownSquare.CentralFountain` was rebuilt from scratch with correctly oriented circular geometry:

- 50-stud circular plinth and 46-stud lower basin.
- Three coordinated stone/water tiers.
- Eight upper arcing streams and six middle arcing streams.
- Five vertical top jets.
- Eight underwater neon lights with PointLights.
- Flower beds and benches positioned around the fountain without blocking the plaza paths.

### Clock tower rebuild

`04_TownSquare.VeteransGatewayTownSquare.BrickClockTower` now includes:

- Stepped limestone foundation and base.
- Taller brick shaft with dark inset panels and corner pilasters.
- Four stone cornice levels.
- Limestone clock chamber.
- Four separate analog clock faces with hour marks and hands.
- Four-panel copper roof, eave, roof cap, spire and gold finial.

### Filled districts

The previously empty southern-center blocks now contain:

- `SchaumburgPoliceDepartment` with visitor parking.
- `VillageConferenceHotel` with parking and landscaped islands.
- `SchaumburgFuelAndMarket` with store, canopy, pump islands and forecourt.
- Detailed striped parking for the municipal hall, fire station, library and clinic.
- `SchoolAthleticCourt` behind the high school.
- Residential foundation shrubs and mulch beds.

### Tree replacement and safety audit

All original `StreetTree` Models were removed. The replacement system generated `123` layered-canopy `OrnamentalTree` Models from block-edge candidates.

- Every normal tree publishes `ClearanceChecked = true`.
- Candidates within 38 studs of any major intersection were rejected.
- Candidates were rejected if a 12 × 16 × 12-stud clearance volume touched roads, sidewalks, curbs, parking, driveways, building foundations or existing trees.
- Tree trunks are collidable, while canopies are non-colliding.
- A final trunk-overlap audit reported `0` trees intersecting roads, sidewalks, parking, buildings or driveways.

### Final verification

- `2,018` anchored BaseParts and `219` Models.
- `0` unanchored parts.
- `0` invisible colliders.
- Player spawned safely on the town-square brick plaza at approximately `(60.3, 3.7, 62.6)`.
- Aerial, town-square, south-district and west-district play-mode views were inspected.
- No console errors appeared.
- Backup: `ServerStorage.SchaumburgTownBase_BeforePolish_20261106`.

## Burg-style building rebuild

The residential and commercial buildings received a separate all-sides rebuild on 2026-11-06. The exact live Burg models could not be cloned because only Place1 was connected, so the rebuild followed [[06 - House Building Standards]] and [[07 - House and Building Catalog]].

### Houses

All ten filler houses were rebuilt into four varied Burg-suburban styles rather than receiving surface-only decoration.

- Exterior-only and fully closed.
- Organized child folders: `ExteriorShell`, `Roofs`, `WindowsAndDoors`, `ExteriorTrim`, `ExteriorDetails`, and `Site`.
- Ranch, craftsman and raised/split-level silhouettes.
- Attached garages with framed, paneled garage doors.
- Layered shingle roof sections, fascia, gutters and downspouts.
- Brick foundation skirts, coordinated siding, corner boards and chimneys.
- Framed glass windows, lintels and optional shutters.
- Front doors, handles, porch roofs, columns, masonry column bases and porch lights.
- Aligned driveways, front walks, mulch beds, shrubs and mailboxes.
- Rear patios, service doors, rear lighting and fully trimmed rear windows.
- Attributes: `ExteriorOnly = true`, `ExteriorFinished = true`, and a `BurgSuburban_1` through `BurgSuburban_4` style value.

### Stores

The twelve original simple storefront shells now publish `Style = BurgCommercial` and `ExteriorFinished = true`.

- Stone/brick façade bases, pilasters and caps.
- Raised parapets and roof cornices.
- Storefront mullions, headers and detailed entrance surrounds.
- Alternating fabric awning stripes and finished planters.
- Door handles, rear service doors and service lights.
- Rooftop HVAC units and slats.
- Rear loading pads, bumpers, wall vents, utility boxes/conduit and enclosed dumpsters.
- Business-specific details: Pulse Luxury neon, café/diner tables, market produce crates, and Auto Service bay accents.

### Apartment

`TownCenterApartments` now includes a stone base, front/rear cornices, brick pilasters, stacked balconies with rails and doors, formal entry canopy, columns, steps, downspouts, rooftop units and resident parking.

### Verification

- Backup: `ServerStorage.SchaumburgTownBase_BeforeBuildingUpgrade_20261106`.
- Current root: `3,666` anchored BaseParts and `219` Models.
- `0` unanchored parts and `0` invisible colliders.
- `122` remaining ornamental trees with `0` physical conflicts after removing one tree that touched a new rear patio.
- Front and rear house, store, apartment and full-town Play-mode views inspected.
- Player still spawns safely at approximately `(60.3, 3.7, 62.6)`.
- No console errors.

## Burg-reference hero interior expansion

Place1 received a gameplay-focused reference expansion on 2026-11-07. The work used [[06 - House Building Standards]], [[07 - House and Building Catalog]], [[14 - Live Buildings Roads and Locations Audit]], and [[23 - Burg Model Transfer Catalog]]. The exact Burg place was not connected at the same time, so these are optimized reconstructions rather than direct Instance clones.

### Playable hero buildings

- `05_CommercialDistrict.PulseLuxury` is now a hollow, playable Luxury-inspired retail model. It has a glass-and-purple-brick storefront, readable `PULSE LUXURY` street sign, neon accents, planters, cashier counter, display walls, three product islands, colored Pulse display props, stockroom, staff bathroom, lighting and three prompted sliding doors. Attributes: `PlayableInterior = true`, `ExteriorFinished = true`, `InspiredBy = MarketSquarePlaza Luxury`.
- `05_CommercialDistrict.TheVibePlace1` replaces the former `TownCafe`. It is a playable The Vibe-inspired lounge with a brick/charcoal storefront, readable street sign, red neon line, lounge booths, couches, tables, service counter, kitchen cabinets and appliances, restroom, string lights, patio seating and two prompted doors. Attributes: `PlayableInterior = true`, `ExteriorFinished = true`, `InspiredBy = The Vibe`.
- `07_ResidentialDistrict.NorthMeadow02_Playable` replaces the former exterior-only `NorthMeadow02` filler while preserving the aligned residential lot. It is a fully walkable Burg-style model home with a garage, porch, working front/garage/bathroom doors, ground-floor living/dining/kitchen/powder-room layout, stairs, an upper hall, bedrooms, office, bathroom, furniture, ceiling and porch lighting, finished windows, roof, driveway, walk, shrubs and mailbox. Attributes: `PlayableInterior = true`, `InteriorFinished = true`, `ExteriorFinished = true`.

The three models are indexed through ObjectValues under `12_HeroInteriors`, while remaining physically located in their normal district folders.

### Reusable model library

`ServerStorage.Place1ReusableModels` contains origin-centered copies ready for `Clone()` plus `PivotTo(...)` placement:

- `PulseLuxuryInteriorTemplate`
- `TheVibeInteriorTemplate`
- `PlayableBurgHouseTemplate`

Each template records its original Workspace source in `TemplateSource` and publishes `PlaceWithPivotTo = true`. The gameplay interaction code is shared instead of duplicated inside every model.

### Shared door system

`ServerScriptService.Place1HeroDoorController` discovers every BasePart with `InteractiveDoor = true`, connects its `ProximityPrompt`, and slides the door along its local X axis by `DoorSlideDistance`. It changes the prompt between Open and Close, disables the prompt during the tween, and also handles compatible doors added later.

### District identity additions

`13_DistrictIdentity` now contains:

- `SchaumburgWelcomeGateway` at the southern connector.
- `TownDirectoryKiosk` with Town Square, Civic Campus, Retail Row and Neighborhood directions.
- Color-coded Town Center, Retail Row, Civic Campus and Neighborhood wayfinding signs.

The civic green, brick, cream, charcoal and purple palette intentionally connects the new signs to Veterans Gateway Park, the clock tower and the hero stores without blocking roads or crosswalks.

### Safety, backups and verification

- New pre-expansion backup: `ServerStorage.SchaumburgTownBase_BeforeReferenceExpansion_20261106`.
- Earlier backups remain: `SchaumburgTownBase_BeforePolish_20261106` and `SchaumburgTownBase_BeforeBuildingUpgrade_20261106`.
- Final town audit: `4,523` descendants, `225` Models, `3,862` BaseParts, `0` unanchored parts and `8` ProximityPrompts.
- Hero counts: Pulse Luxury `102` parts / `3` prompts; The Vibe `115` parts / `2` prompts; playable house `218` parts / `3` prompts.
- Aerial, retail-front, both retail-interior, house-front and house-interior views were inspected. A roof/ceiling intersection found during inspection was corrected before the reusable house template was refreshed.
- Play mode started successfully, the shared controller was enabled, all prompts remained present, and the Studio console remained clean.

### Continuation rules for hero buildings

- Keep filler buildings exterior-only until they serve gameplay; promote only selected landmarks to hero interiors.
- Store reusable clones in `ServerStorage.Place1ReusableModels`, but keep the live copy in its numbered district folder.
- Use attributes and the shared door controller instead of adding a separate door script to every model.
- Keep product props and furniture optimized from primitive parts so the town remains stable as more interiors are added.
- If exact Burg models are later exported as `.rbxm`, import them into a staging folder first and compare dependencies before replacing these gameplay-ready reconstructions.

## Alignment, gateway and neighborhood expansion pass

Place1 received a map-wide structural correction and original-feature pass on 2026-11-07. The priority was to remove physical overlaps and awkward empty areas before adding more decoration.

### Town-square gateway rebuild

`04_TownSquare.VeteransGatewayTownSquare.VeteransGateway` was rebuilt from scratch.

- The old disconnected arms and stepped arch pieces were removed.
- Two brick-and-limestone plinths now support inset civic-green metal posts.
- Twenty connected arch segments form one continuous curve with no visible gaps.
- A dark green, gold-trimmed signboard reads `SCHAUMBURG TOWN SQUARE` and `VETERANS GATEWAY` on both sides.
- Caps, brackets and finials use the same brick, cream, civic green and muted gold palette as the clock tower and district identity signs.
- Reusable copy: `ServerStorage.Place1ReusableModels.SchaumburgTownGatewayTemplate`.

### Residential alignment correction

The audit found multiple house shells physically overlapping one another and three houses occupying the same parcels as the library, clinic-side commercial area or other buildings. The correction was structural rather than cosmetic.

- Nine exterior-only filler houses were reduced to `0.82` scale so their footprints fit the neighborhood blocks without losing their established style.
- Every home was rotated from its driveway direction, not from an assumed model yaw.
- Driveway edges were aligned directly to the appropriate road edge.
- `NorthMeadow02_Playable` received a short concrete `DrivewayConnector` to close its remaining small sidewalk gap.
- The two northern west-side homes now form a clean east-facing row.
- The two northern east-side homes now form a clean west-facing row.
- Final audits report `0` house-to-house overlaps and `0` residential-to-commercial/civic building overlaps.

### South Village extension

The six houses that could not fit safely in the existing civic blocks now form a real neighborhood under `15_SouthVillageExtension`.

- Six road-facing homes: `SouthVillage01`, `SouthVillage02`, `EastGrove01`, `EastGrove02`, `WestCourt01`, and `EastCourt01`.
- 32-stud `SouthVillageLane`, approximately 320 studs long.
- Full sidewalks, curbs, center dashes and a paved turnaround.
- Eight coordinated streetlights and clearance-checked ornamental trees.
- Readable `SOUTH VILLAGE LN` street sign.
- `SouthVillageExpansionConnector` with a `RoadSnap` Attachment for a future continuation.
- Extension attributes record six houses, 32-stud road width and expansion-ready status.

### Original feature: Schaumburg Weekend Market

`04_TownSquare.VeteransGatewayTownSquare.SchaumburgWeekendMarket` adds useful activity to the previously empty southern plaza corners while preserving both main pedestrian axes.

- Two matching civic-green market pavilions.
- Four counters with numbered `VendorSlot` Attachments for future NPC/store logic.
- Display crates, canopy trim, warm string bulbs and paved pads.
- Separate two-sided `SCHAUMBURG WEEKEND MARKET` event sign.
- Indexed through `14_CommunityFeatures`.
- Reusable copy: `ServerStorage.Place1ReusableModels.WeekendMarketPavilionTemplate`.

### Backup and verification

- Backup: `ServerStorage.SchaumburgTownBase_BeforeAlignmentAndIdentity_20261107` with the complete pre-pass town.
- Final root: `4,728` descendants, `240` Models and `4,007` BaseParts.
- `0` unanchored parts.
- `0` invisible colliders.
- `0` residential overlaps.
- `0` residential-to-civic/commercial overlaps.
- `0` extension tree/road conflicts.
- Player spawned safely at approximately `(57.5, 6.0, 56.5)`.
- Town-square, all four residential corners, the new neighborhood extension and aerial composition were inspected.
- Play mode produced no console errors.

### Reusable library after this pass

`ServerStorage.Place1ReusableModels` now contains:

- `PlayableBurgHouseTemplate`
- `PulseLuxuryInteriorTemplate`
- `TheVibeInteriorTemplate`
- `SchaumburgTownGatewayTemplate`
- `WeekendMarketPavilionTemplate`

## Town Explorer trail — 2026-11-07

The first small gameplay loop in the `test` Place One town is `14_CommunityFeatures.TownExplorerTrail`. Four compact visit markers lead players through the fountain `(120, 84)`, clock tower `(177, 70)`, weekend market `(120, 205)`, and Pulse Luxury `(-195, 112)`. Each marker has a ProximityPrompt, a short range BillboardGui, and a distinct district color. The markers avoid the main walking paths and use anchored parts.

`ServerScriptService.Place1TownExplorerServer` tracks the four visits per player with a bitmask, validates that a living character is within 13 studs, rejects repeat credit, and sets `ExplorerMask`, `ExplorerProgress`, `ExplorerLastStop`, `ExplorerComplete`, and `TownTitle` attributes. Completion gives the `Town Explorer` title attribute for the current server session; it does not award currency or saved XP.

`StarterPlayer.StarterPlayerScripts.Place1TownExplorerClient` creates a compact top-right progress HUD and updates it from the replicated player attributes. The HUD does not capture the mouse or change camera controls.

The change was guided by [[Level Design Principles - Flow Sightlines and Landmarks]] and [[World-Space UI - BillboardGui and SurfaceGui]]: use the existing clock and fountain as landmarks, give players a reason to follow the route, and limit world labels with `MaxDistance`.

Backup: `ServerStorage.SchaumburgTownBase_BeforeExplorerTrail_20261107`.

Playtest verification: all four prompts advanced progress `1 → 2 → 3 → 4`; completion set `ExplorerComplete = true` and `TownTitle = Town Explorer`. The HUD displayed the completed state, and the Studio console was clear. Progress currently resets on joining a new server; persistence and any credit/XP reward need a separate economy integration decision.
