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

