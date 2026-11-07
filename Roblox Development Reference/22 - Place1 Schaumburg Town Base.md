# Place1 Schaumburg Town Base

This note documents the large editable town foundation created in the separate Roblox Studio project named **Place1** on 2026-11-06.

## Root model

- Studio path: `Workspace.SchaumburgTownBase`
- PrimaryPart: `Workspace.SchaumburgTownBase.11_MapConnectors.TownPivot`
- Style attribute: `TownStyle = SchaumburgInspired`
- Planned map size attribute: `MapSize = 900`
- Audited bounds: approximately `966 × 102.9 × 902` studs
- Audited center: approximately `(-2.5, 35.5, 0)`
- Final contents: `1,285` BaseParts and `202` Models
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
