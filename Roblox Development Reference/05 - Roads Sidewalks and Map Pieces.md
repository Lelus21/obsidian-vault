# Roads, Sidewalks, and Map Pieces

## Requested road kit

- Simple straight road.
- Sidewalk on both sides.
- Four-way intersection connector.
- Left turn.
- Right turn.
- All pieces must snap together cleanly.

## Alignment rules

- Use one shared road width across every piece.
- Match sidewalk height, sidewalk width, curb height, asphalt thickness, and lane-marking positions.
- End faces should lie on a predictable grid increment.
- Pivot each model at a useful snap point, normally the road center or one connector edge.
- Keep straight road endpoints square.
- Curves should enter and leave with the same tangent and width as straight segments.
- Avoid tiny overlaps or visible gaps between curbs.
- Lane markings should continue naturally through connected pieces.
- Keep road and sidewalks anchored.

## Existing map-piece names referenced

- `simple road`
- `FourWayIntersection`
- `RightTurnRoad`
- `roadtype1`

## Recommended connector metadata

Each modular road can contain Attachments such as:

- `NorthConnector`
- `SouthConnector`
- `EastConnector`
- `WestConnector`

Align the CFrame of one connector to the matching connector of the next road piece. This is safer than manually dragging by eye.

## Live town-square neighborhood starter

`Workspace.TownSquareNeighborhoodExpansion` extends `Workspace.SchaumburgTownSquare` into a modular neighborhood starting point.

- Road width: `32` studs.
- Sidewalk width: `4` studs.
- Asphalt thickness: `0.4` studs.
- Sidewalk thickness: `0.5` studs.
- Grid increment: `4` studs.
- Main east-west road: `TownSquareDrive`, spanning approximately `X 559.7` to `X 751.7` at `Z 325.6`.
- South road: `NeighborhoodBoulevard`, spanning approximately `Z 325.6` to `Z 449.6` at `X 655.7`.
- Public parking: ten marked spaces, an accessible space, driveway, wheel stops, sidewalks, and four landscaped islands.
- Supporting street pieces: gateway crosswalk, curbs, edge lines, dashed center lines, stop control, street-name signs, streetlights, bus shelter, bike racks, and neighborhood monument.

### Expansion connector paths

- `Workspace.TownSquareNeighborhoodExpansion.Connectors.WestNeighborhoodConnector` at approximately `(559.7, 0.45, 325.6)`.
- `Workspace.TownSquareNeighborhoodExpansion.Connectors.EastNeighborhoodConnector` at approximately `(751.7, 0.45, 325.6)`.
- `Workspace.TownSquareNeighborhoodExpansion.Connectors.SouthNeighborhoodConnector` at approximately `(655.7, 0.45, 449.6)`.
- Each road connector contains a `RoadSnap` Attachment.
- Six matching sidewalk endpoints contain `SidewalkSnap` Attachments.

New straight roads should continue from these endpoint faces with the same 32-stud asphalt width, 4-stud sidewalks, elevation, center-line position, and connector orientation.

### Sidewalk junction repair

The live expansion was repaired so sidewalks and curbs no longer cross drivable openings:

- The south frontage sidewalk and curb are split into west/east pieces around the `NeighborhoodBoulevard` mouth.
- Boulevard sidewalks and curbs begin after the frontage-road intersection instead of extending into it.
- The west boulevard sidewalk and curb are split around `ParkingDriveway`.
- The north curb has a 20-stud opening aligned to the town-square gateway and crosswalk.
- `StopSign` is upright at Y rotation `180` and faces northbound boulevard traffic.
- `BusStopSign` uses Y rotation `90` and faces the roadway.
- Backup: `ServerStorage.TownSquareNeighborhoodExpansion_BeforeSidewalkFix_192815`.

## Standardized live road kit

The older road pieces were rebuilt to match the Town Square profile instead of the original 24-stud asphalt width.

### Shared profile

- Asphalt width: `32` studs.
- Sidewalk width: `4` studs per side.
- Total outside width: `40` studs.
- Asphalt thickness: `0.4` studs.
- Sidewalk thickness: `0.5` studs.
- Curbs: `0.45` studs wide and `0.65` studs tall.
- White edge-line offset: `14.8` studs from center.
- Every model publishes `RoadWidth = 32`, `SidewalkWidth = 4`, and `TotalWidth = 40` attributes.
- Every piece has a transparent, non-colliding `RoadPivot` PrimaryPart with named road and sidewalk Attachments.

### Piece dimensions

- `simple road`: `98` studs long, `40` studs outside width, with `NorthConnector` and `SouthConnector` at the square end faces.
- `LeftTurnRoad` and `RightTurnRoad`: three `32 × 32` asphalt sections, `68 × 68` overall footprint, six road/sidewalk connectors, matching curbs, and segmented curved center markings.
- `FourWayIntersection`: five `32 × 32` asphalt sections, `96 × 96` footprint, four road connectors and eight sidewalk connectors.

### Standardized live paths

- Both top-level models named `Workspace.simple road`.
- `Workspace.FourWayIntersection`.
- `Workspace.RightTurnRoad`.
- `Workspace.RoadConnectors.LeftTurnRoad`.
- `Workspace.RoadConnectors.FourWayIntersection`.
- `Workspace.roadtype1.simple road`.
- `Workspace.roadtype1.FourWayIntersection`.

`roadtype1` was shifted `12` studs in positive Z to preserve its north straight connection after the four-way footprint grew. Its nested straight was then aligned to the four-way's east connector with a final connector gap of `0.000` studs. The loose `RightTurnRoad` sample was shifted `8` studs in positive Z to prevent a widened-footprint collision.

Backup: `ServerStorage.RoadKitBeforeTownSquareWidth_193618`.

