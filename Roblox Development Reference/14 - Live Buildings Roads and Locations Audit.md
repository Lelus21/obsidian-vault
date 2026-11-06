# Live Buildings, Roads, and Locations Audit

## House style references

The polished filler-house pattern is best represented by `BeigeSplitLevelFillerHouse` and `GrayGableTownhouse`. Both are organized around exterior folders rather than an interior:

- `ExteriorShell`
- `ExteriorTrim`
- `Roofs`
- `WindowsAndDoors`
- `Site`
- optional `ExteriorDetails`

Common material language across the neighborhood is SmoothPlastic siding/trim, Metal gutters and hardware, Glass windows, Slate roofs, Concrete driveways, and Grass site pads. Fronts use clear doors, garages, driveways, paths, trim, lights, and restrained landscaping. Backs remain simpler so they do not read like a second front.

## Interactive player houses

### `besthouse`

- 3,026 descendants, including 2,718 Parts, 155 Models, 62 ProximityPrompts, 20 ClickDetectors, 18 PointLights, and 11 Seats.
- Three floors, stairs, baseboards, railings, furniture and a player bedroom.
- Door types include front, room, garage access, garage backyard, tilt garage, patio sliding, and attic hatch.
- Windows can open halfway and expose a separate Crawl Through prompt.
- `WindowCoverings` adds blinds and curtains with individual toggle prompts.
- Bedroom interactions: desk chair, computer, wardrobe, and sleep bed.
- Scripts: `HouseDoorController`, `WindowInteractionController`, `WindowCoveringsController`, and `DeskChairSeating`.

### `thetesthouse`

- 1,911 descendants, including 1,693 Parts, 121 Models, 40 ProximityPrompts, 17 PointLights, and 10 Seats.
- Uses the same three-floor, door, window, garage, patio, and attic architecture without the full player-bedroom/wardrobe polish.

### `test house`

- 577 descendants.
- Contains `ExteriorFinish`, `FinishedInterior`, `PolishedStructure`, and `RoomLayoutRepair`.
- Its front door uses a dedicated `DoorInteraction` script and E prompt.

## Schaumburg High School

The school is the largest current model at 20,175 descendants: 18,227 Parts, 363 Models, 472 Seats, 153 ProximityPrompts, 240 SurfaceGuis, 163 SurfaceLights, 65 ClickDetectors, and 16 active scripts/modules.

Top-level sections:

- `Interior`: 8,008 descendants. Classrooms, offices, gym, cafeteria, scan-in stations, multi-floor restrooms and fixtures.
- `RearAthletics`: 9,933 descendants. Stadium, football area, check-in building and master lighting.
- `CampusExteriorLighting`: 631 descendants.
- `CampusParkingFinish`: 807 descendants.
- `SiteAndMasonry`: 272 descendants.
- `EntrancesRampsAndCanopy`: 184 descendants.
- `RearPhotoCompletion`: 104 descendants.
- `LandscapeAndExteriorDetails`: 89 descendants.
- `WestParkingAndStadiumApproach`: 22 descendants.
- Smoke infrastructure: `RoomSmokeRegions`, `RoomSmokePortals`, and `RoomSmokeState`.

Key interactions include classroom and office doors, school ID scanners, exit buttons, stadium scan-in, stadium master lights, basketball cart take/return, six treadmills, lunch-worker talk/order prompts, bathroom doors, sinks/fountains, and individual stall open/lock controls. Stall open uses E and lock uses F.

## The Vibe

- 549 descendants: 447 Parts, 27 Models, 21 PointLights, 10 Seats, and 5 ProximityPrompts.
- Sections: `Shell`, `Roof`, `ExteriorDetails`, `StringLights`, `Lounge`, `Kitchen`, `Cashier`, `BathroomExtension`, `PreparedFood`, and smoke state.
- Entry and both restroom doors use tweened door controllers.
- Cashier prompt starts dialogue; fridge prompt opens the kitchen fridge.
- Cashier AI can move, talk, use drawers/fridge/oven, cook and serve food, and use an MXK.
- Room smoke accumulates by room mass/density and exchanges through open doors.

## Market Square Plaza

- 14,961 descendants: 3,280 Parts, 213 Models, 5,975 Frames, 4,529 UICorners, 333 SurfaceGuis, and 10 ProximityPrompts.
- `Buildings`: 14,500 descendants; `Parking`: 218; `Landscaping`: 228; `Site`: 11.
- Named businesses with active doors include Luxury, Subway, and Walgreens.
- Luxury has an interior stockroom, staff bathroom and an animated worker.
- `MarketSquarePlazaDoors` uses attributes to find tagged doors and tween them by configured slide width.

## Burg Dream World

- 1,667 descendants and 1,104 Parts.
- Sections: `BlackVoidShell`, `CloudCanopy`, `CloudAndSmokeDecor`, `CloudFloorForms`, `DreamDetails`, `DreamExitStaircase`, `DreamStairwellGuard`, `ExteriorCloudAccents`, `OuterCloudBanks`, `PurpleLighting`, `SecondFloorReplica`, `PlayerDreamBed`, `TravelAnchors`, and `XPTokenTrader`.
- The XP trader has a Talk prompt and idle visual controller.
- Dream entry/exit is controlled by the Burg Dream service and client transition effect.

## Road kit

All road surfaces are 0.5 studs thick and use consistent center markings, edge lines and sidewalks.

- Straight `simple road`: 32 × 0.5 × 98 studs. Two live copies. Includes RoadSurface, left/right Sidewalk, left/right EdgeLine, and ten CenterDash Parts.
- `RightTurnRoad`: 52 × 0.5 × 52. Entry and exit road surfaces, inner/outer edges and sidewalks, center dashes and inner corner.
- `RoadConnectors.LeftTurnRoad`: 16 descendants.
- `FourWayIntersection`: 72 × 0.5 × 72, 33 descendants. Center surface plus four directional road arms, sidewalks, corners, outer edge marks, and center dashes.
- `roadtype1`: 72 × 0.5 × 170. Composite containing a FourWayIntersection and straight road.
- `RoadConnectors.SNAP_GUIDE` preserves snapping/alignment guidance.

When extending the map, clone the connector templates rather than remodeling widths. Keep pivots and Y elevation unchanged so the 32-stud straight roads and 72-stud intersections stay aligned.
