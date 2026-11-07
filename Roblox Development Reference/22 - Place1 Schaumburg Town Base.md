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
