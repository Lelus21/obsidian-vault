# House Building Standards

## Default filler-house rule

Unless an interior is explicitly requested, neighborhood houses should be:

- Exterior-only.
- Hollow inside.
- Fully closed from every outside camera angle.
- Free of interior furniture, room walls, stairs, and decorative clutter.
- Optimized for background/filler use.

## Exterior quality checklist

- No random walls or windows floating in the air.
- Windows sit inside wall openings rather than hovering on top of empty space.
- No wall pieces protrude through the roof.
- Gable ends are completely filled.
- Roof valleys and roof-to-wall transitions are sealed.
- Fascia, soffits, gutters, and corner boards align consistently.
- Chimneys intersect roofs cleanly and include a cap.
- Front must read clearly as the front; rear should be simpler.
- Garage must be fully present when shown in the reference.
- Driveway aligns with garage doors.
- Entry path aligns with the front door.
- Keep plants, but remove unnecessary giant grass plates if requested.
- Exterior color palette should be consistent with no accidental mismatched walls.
- Inspect front, rear, left, right, and top views before considering the model complete.

## Model organization

Recommended folders:

- `ExteriorShell`
- `Roofs`
- `WindowsAndDoors`
- `ExteriorTrim`
- `ExteriorDetails`
- `Site`

Recommended attributes:

- `ExteriorOnly = true`
- `ExteriorFinished = true`
- `BuildOrigin`
- Optional style/backup metadata

## Technical rules

- Anchor every building and site part.
- Set decorative parts to `CanCollide = false` when players should not hit them.
- Keep major walls and floors collidable.
- Use `SmoothPlastic`, `Concrete`, `Slate`, `Brick`, `Glass`, `Metal`, `Grass`, and `Ground` intentionally.
- Use consistent wall thickness.
- Use a model PrimaryPart or reliable pivot.
- Avoid excessive tiny pieces on filler houses.
- Back up a detailed version to `ServerStorage` before replacing it with a simplified shell.

## Neighborhood alignment checklist

- Audit actual building footprints before arranging houses; visual spacing from one camera angle is not enough.
- Check house-to-house and house-to-civic/commercial overlaps separately.
- Use the driveway direction to determine the true front of a reused model. Do not rely only on the pivot's reported yaw.
- Make the driveway reach the road or sidewalk edge exactly; add a small matching connector when the remaining gap is intentional.
- Keep a narrow but visible property gap between neighboring roof overhangs, yards and site pieces.
- If two full-size filler houses cannot fit inside a block, scale only the filler shells consistently or move them to a planned neighborhood extension.
- Never hide houses inside a civic, commercial or parking parcel just to fill space.
- New neighborhood extensions should continue the road hierarchy, sidewalks, curbs, lighting and `RoadSnap` connector system.
- Run the overlap audit again after rotating, scaling or moving any house.

## Preferred visual style

- Roblox-readable proportions.
- Polished suburban architecture.
- Moderate blockiness rather than photorealistic mesh complexity.
- Layered roofs with believable overhangs.
- White or coordinated trim around windows and roof edges.
- Simple shrubs and mulch beds rather than dense landscaping.

