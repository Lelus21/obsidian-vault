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

