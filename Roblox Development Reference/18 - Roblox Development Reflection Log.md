# Roblox Development Reflection Log

This is the continuing memory for Roblox development on **The burg**. It should be read before implementing a new request and updated after each completed, verified Roblox change.

## Standard workflow

### Before changing the game

1. Read [[00 - Roblox Project Index]].
2. Read the notes connected to the requested model or system.
3. Read the latest entries in this reflection log.
4. Inspect the live Studio hierarchy and current source instead of assuming an older note is still exact.
5. Reuse proven code patterns, attributes, Remotes, naming and cleanup behavior where they fit.
6. Check whether the change must be applied to both a Workspace reference and a `ServerStorage.EquipmentBagTools` template.

### After changing the game

Add a dated entry containing:

- User request and intended result
- Exact instance and script paths changed
- Important attributes, timing, colors, sizes and balance values
- Code architecture and events used
- Testing performed and observed results
- Bugs found and how they were fixed
- Reusable lesson or pattern
- Remaining limitations or follow-up ideas

Do not mark a request successful until the relevant behavior has been inspected or playtested in proportion to its risk.

## Reflection principles

- Treat the live Studio place as the source of truth.
- Preserve user-created work and unrelated models.
- Prefer extending existing systems over creating competing duplicate systems.
- Keep client presentation separate from server validation and resource changes.
- Keep R6 pose, first-person camera, touch, gamepad and desktop prompt behavior in mind.
- Clean up runtime UI, effects, temporary Parts, event connections, IK objects and render bindings.
- Record failed approaches when they explain a bug or prevent repeating it.
- Update existing reference notes when the current implementation changes materially.
- Store concise explanations and critical snippets or pseudocode; Studio remains the source for complete Luau files.

## Entry template

```markdown
## YYYY-MM-DD — Short change title

**Request:**

**Studio paths:**

**Implementation:**

**Exact values and contracts:**

**Verification:**

**Problems and fixes:**

**Reusable lesson:**

**Follow-up:**
```

## 2026-11-04 — Reflection workflow established

**Request:** Maintain notes for every future Roblox coding request and consult those reflections before implementing new work.

**Studio paths:** No Roblox instances were changed.

**Implementation:** Added this persistent reflection log and linked it from the project index. Future Roblox turns should begin by reviewing relevant reference notes and end by recording verified implementation details.

**Verification:** Confirmed the Obsidian reference library already contains the live game inventory, Tool reference cards, location audit, script register, exact data contracts, and maintenance notes.

**Reusable lesson:** Project memory is most useful when it captures exact paths, values, tests and failed approaches—not only a general description of the feature.

**Follow-up:** Append the next completed Roblox change below this entry and update any affected system-specific note.

## 2026-11-04 — XP and Equipment navigation redesign

**Request:** Replace the simple XP and Backpack buttons with attractive GUI tabs that include recognizable icons.

**Studio paths:**

- `StarterPlayer.StarterPlayerScripts.ToolXPMenu`
- `StarterPlayer.StarterPlayerScripts.EquipmentBagUI`
- Backup: `ServerStorage.UIBeforeNavRedesign_20261104`

**Implementation:** Rebuilt the two top-left launch buttons as a coordinated navigation dock. XP is a 132×54 blue-violet card at `(14, 12)` with a shape-built progression-chart icon and the labels `PROGRESS` / `XP & LEVELS`. Equipment is a 166×54 green card at `(154, 12)` with a shape-built backpack, `INVENTORY` / `EQUIPMENT` labels, and a `B` shortcut chip. Both use rounded icon plates, gradients, accent strips, shadows, strokes, hover enlargement, pressed scaling and color feedback. Existing panel, XP data, Equipment Bag data, title-screen visibility, B shortcut and mutual panel behavior were preserved.

**Exact values and contracts:** Tabs use 54-pixel height, 15-pixel corner radius, 1.25-pixel outlines, 1.035 hover scale, 0.965 pressed scale and 0.13-second Quad tweens. XP remains hidden with its shadow while `BurgTitleActive` is true.

**Verification:** Entered play mode, passed the title screen, visually inspected the dock, opened the XP panel, then opened the Equipment Bag. XP opened correctly; Equipment opened correctly and closed XP; both panels retained their content and there were no console errors.

**Problems and fixes:** The first XP icon used the Unicode sparkle `✦`, which Gotham rendered as a missing-character square. Replaced it with three rounded progress bars and a shine dot made entirely from Frames, making the icon independent of font glyph support.

**Reusable lesson:** For important Roblox UI icons, prefer ImageLabels with verified assets or icons drawn from Frames. Do not depend on uncommon Unicode symbols without playtesting the exact Roblox font.

**Follow-up:** If the title screen is redesigned later, reuse this blue/green navigation language so the front end and in-game HUD feel like one product.

## 2026-11-04 — Luxury cashier store and equipment ownership

**Request:** Make Luxury a working store where talking to the NPC at the cash register opens a menu and lets players buy the stocked devices with money.

**Studio paths:**

- `Workspace.MarketSquarePlaza.Buildings.Luxury.Interior.LuxuryWorker`
- `ReplicatedStorage.LuxuryStore.Catalog`
- `ReplicatedStorage.LuxuryStore.Open`
- `ReplicatedStorage.LuxuryStore.Purchase`
- `ServerScriptService.LuxuryStoreServer`
- `StarterPlayer.StarterPlayerScripts.LuxuryStoreClient`
- Updated: `ServerScriptService.EquipmentBagServer`
- Updated: `ServerScriptService.BurgStorySaves`
- Updated: `StarterPlayer.StarterPlayerScripts.EquipmentBagUI`
- Backup: `ServerStorage.LuxuryStoreBeforeSystem_20261104`

**Implementation:** Added an `E` cashier ProximityPrompt to `LuxuryWorker.CashierRoot`, a dark charcoal-and-gold Luxury storefront GUI, category filters, live wallet balance, product cards, owned states and purchase feedback. Purchases are validated on the server for cashier distance, catalog membership, template availability, ownership, available money and request rate. Successful purchases subtract `leaderstats.Money`, add a BoolValue under `Player.EquipmentOwnership`, and become available through the existing Equipment Bag. MuhaMed is the starter item; the old behavior that granted every catalog Tool for free was removed. Story saves now store `OwnedEquipment` with save schema version 2 while remaining compatible with version 1 saves.

**Exact values and contracts:**

- Fab Pulse `$450`; Meta Moon Pulse `$500`; Miami Mint Pulse `$550`; Dragon Melon Pulse `$600`; Blue Razz Blast Pulse `$650`; MXK `$850`; ACE `$1000`; MuhaMed `$750` and owned by default.
- Cashier prompt: keyboard `E`, gamepad `ButtonX`, 10-stud activation distance, no hold, no line-of-sight requirement, `AlwaysShow` exclusivity and non-clickable desktop behavior.
- Purchase distance is revalidated on the server at 16 studs and requests are rate-limited to one every 0.35 seconds.
- Ownership folder: `Player.EquipmentOwnership`; each owned catalog id is a `BoolValue` named `fab`, `meta`, `miami`, `dragon`, `blue`, `mxk`, `ace` or `muha`.
- Story snapshots use `Version = 2` and `OwnedEquipment = {id, ...}`. Missing/old ownership data safely defaults to `muha`.
- Equipment Bag cards for unowned tools now say `BUY AT LUXURY` and `Visit Luxury` instead of pretending the item is loading.

**Verification:** Entered Free Roam, moved the player to the cashier, activated the actual cashier prompt and confirmed the menu opened. With `$3000`, bought Fab Pulse for `$450`; balance became `$2550`, `EquipmentOwnership.fab` appeared, and the Tool appeared in `EquipmentBagInventory`. A duplicate Fab purchase was rejected without another deduction. With `$0`, ACE returned `You need $1000 more.` Reloading the character preserved both MuhaMed and Fab ownership and rebuilt the correct Backpack/inventory state. Final console output contained no game-script errors.

**Problems and fixes:** The production templates are named by catalog ids (`fab`, `meta`, etc.) rather than their display/source names, so template lookup was made compatible with both id and source naming. LuxuryWorker is under `Luxury.Interior`, not directly under `Luxury`; the server path was corrected. The automated playtest camera remained at the title camera after server teleport, which initially hid the proximity prompt; moving the test camera to the cashier verified that the real prompt-to-menu route works. `AlwaysShow` exclusivity prevents nearby display-item prompts from replacing the cashier interaction.

**Reusable lesson:** Treat shop stock, ownership and inventory as separate layers. The client may render catalog data, but the server must validate proximity, price, funds, ownership and template existence. Persist stable catalog ids rather than Tool instance names so cosmetic renames do not invalidate saves.

**Follow-up:** When Green Pulse or NOVA receive production-ready Equipment Bag templates and gameplay behavior, add them to both `EquipmentBag.Catalog` and `LuxuryStore.Catalog` before selling them.

## 2026-11-06 — XP gain bar documented

**Request:** Capture all information from the new XP bar in the Obsidian reference notes.

**Studio paths:** `StarterPlayer.StarterPlayerScripts.ToolXPGainHUD`, `ReplicatedStorage.ToolXPGained`, `ReplicatedStorage.ToolXPConfig`, and `ServerScriptService.ToolXPService`.

**Implementation:** Created [[21 - XP Gain Bar Reference]] and updated the live system register and exact data contracts with its event flow, dimensions, responsive offset, labels, level colors, animation timings, reward values, cooldowns, repeated-gain behavior, published attributes, and save behavior. No Studio code was changed.

**Verification:** In Free Roam, fired the real gain event for a 500-XP Penjamin increase and visually confirmed the HUD. Two rapid 100-XP Pulse Bar events combined into `+200 XP`. No XP system errors appeared in the game console.

## 2026-11-05 — Starter Pulse

New equipment sessions and fresh Story saves start with `starterpulse`, a basic graphite Pulse Bar with 15% battery and 0% juice. Empty juice blocks activation and server-side use counting on this Tool. Existing Story slots load their saved ownership, with MuhaMed retained as the fallback for older slots without an ownership list. Luxury no longer grants MuhaMed automatically.

The template is `ServerStorage.EquipmentBagTools.starterpulse`. The Equipment Bag catalog and preview use the same id. Updated `EquipmentBagServer`, `BurgStorySaves`, `LuxuryStoreServer` and the Luxury catalog. Backups are in `ServerStorage.StarterPulseBefore_20261105`.

Studio playtest confirmed the new Tool in the fresh player's Backpack, the starter ownership flag, no automatic MuhaMed, and screen values of 15 and 0%. Story save reload was not playtested.

## 2026-11-05 — Starter Pulse burnt use and XP

Updated `ServerStorage.EquipmentBagTools.starterpulse` so 0% juice shows `0% BURNT` and still permits normal hits while battery remains. Removed the second-tap Ghost interaction and reject Ghost requests on the server. A completed normal hit costs one battery point and uses `ToolXPConfig.Rewards.StarterPulseNormal` for 50 Pulse Bar XP. The Equipment Bag card lists the starter reward. Studio playtest verified the completion handler rejected Ghost, then awarded 50 XP and dropped battery from 15 to 14 for a normal completion at zero juice.

## 2026-11-05 — Menu cursor handoff

`LuxuryStoreClient` now uses a visible modal button for GUI cursor access. Removed its per-frame mouse unlock and saved cursor restoration. `EquipmentBagUI` clears search focus when hidden and enables its modal button only while the bag is visible. Verified first-person mouse mode was `LockCenter` with the normal camera after closing Luxury and verified the bag released focus when hidden. Studio automation supplied zero mouse delta while locked, so physical mouse-look recovery was not verified.

## 2026-11-06 — Schaumburg-inspired town square

**Request:** Begin the map with a polished town square inspired by Schaumburg Town Square in Illinois, including its brick clock-tower landmark, green civic gateway and a central fountain.

**Studio path:** `Workspace.SchaumburgTownSquare`

**Placement and scale:** Final live bounds are centered at approximately `(655.7, 29.7, 239.1)` in the clear lot beside the existing road network. The ground pivot is approximately `(655.7, 0.8, 237.6)`, and overall bounds are about `150 × 59.3 × 141` studs. Four invisible, non-colliding snap markers are under `Connectors`: `RoadConnectorSouth`, `RoadConnectorNorth`, `RoadConnectorEast`, and `RoadConnectorWest`, each with a `SnapAttachment`.

**Organization:** `Amenities`, `ClockTower`, `Connectors`, `Fountain`, `Gateway`, `GroundAndPaths`, `Landscaping`, `Lighting`, and `RetailShells`. The model's PrimaryPart is `Connectors.TownSquarePivot`, so the complete square can be moved as one unit.

**Implementation:** Built a brick-paved civic plaza with concrete approaches, a teal segmented entrance arch labeled `SCHAUMBURG TOWN SQUARE`, a tall red-brick clock tower with pale stone bands and four visible clock faces, a two-tier illuminated fountain with five water particle jets, two low brick storefront shells labeled `TOWN CAFE` and `LOCAL MARKET`, trees, hedges, flower planters, benches, warm lampposts, flags, waste bins, and a stepped tower approach with rails. Styling intentionally uses optimized Roblox primitives and readable silhouettes rather than dense geometry.

**Verification:** Final model contains `266` anchored BaseParts, `24` Models, `5` ParticleEmitters, and `9` PointLights. Structural audit found `0` unanchored parts and `0` invisible colliders. Front and aerial Studio captures confirmed the plaza composition, fountain, tower, landscaping, and south-facing signage. Three SurfaceGuis that initially faced north were corrected to face the main southern entrance.

**Reusable lesson:** Audit the intended footprint against existing roads before building a large map landmark. Keep a civic set piece under one PrimaryPart with named folders and cardinal snap connectors; this makes future roads, parking, and surrounding commercial blocks much easier to align without rebuilding the square.

## 2026-11-06 — Town square neighborhood road expansion

**Request:** Expand the town square with original ideas, roads, sidewalks, and connectors that can begin the surrounding neighborhood.

**Studio path:** `Workspace.TownSquareNeighborhoodExpansion`

**Implementation:** Added a 32-stud-wide east-west frontage road directly against the town-square entrance and a matching southbound neighborhood boulevard. Both roads use 0.4-stud asphalt, 4-stud sidewalks, raised curbs, white edge lines, yellow dashed center lines, and a broad gateway crosswalk. Added a ten-space public parking lot with an accessible space, driveway, wheel stops and landscaped islands. Supporting details include a glass `TOWN LOOP` bus shelter, warm streetlights, `TOWN SQUARE DR` and `NEIGHBORHOOD BLVD` signs, stop control, bike racks, trees, and a brick `NEIGHBORHOODS` monument.

**Connectors:** `WestNeighborhoodConnector`, `EastNeighborhoodConnector`, and `SouthNeighborhoodConnector` each contain a `RoadSnap` Attachment. Six corresponding sidewalk endpoints use `SidewalkSnap` Attachments. Exact coordinates and dimensions are recorded in [[05 - Roads Sidewalks and Map Pieces]].

**Verification:** Aerial Studio review confirmed that the road meets the town-square gateway cleanly and that the boulevard, parking lot, bus shelter, and signage form a readable neighborhood entrance. The final expansion contains `138` BaseParts; all are anchored, no invisible colliders were found, and an overlap audit found `0` intersections with the pre-existing road, turn, connector, or four-way models. Overall bounds are approximately `193.5 × 11.4 × 148.5` studs.

**Reusable lesson:** When extending a landmark into a map hub, build the frontage street and sidewalks to the existing boundary first, then create outward-facing road and sidewalk attachments before adding decoration. This keeps parking, transit, and landscaping visually polished without sacrificing future snap compatibility.

## 2026-11-06 — Town square sidewalk and sign repair

**Request:** Fix the town-square expansion's uneven sidewalk joins and rotate its signs correctly.

**Implementation:** Split the south frontage sidewalk and curb around the boulevard mouth, trimmed both boulevard sidewalk runs so they begin outside the intersection, opened the west sidewalk and curb at the parking driveway, and added a 20-stud gateway curb opening aligned to the crosswalk. Added clean corner pads at the T-junction. Rotated the stop sign upright to `(0, 180, 0)`, rotated the bus-stop sign toward the road to `(0, 90, 0)`, and normalized the street-name and neighborhood monument blades.

**Backup:** `ServerStorage.TownSquareNeighborhoodExpansion_BeforeSidewalkFix_192815`

**Verification:** Aerial and street-level Studio captures confirmed a clear T-junction, flush gateway crossing, open parking driveway, upright stop sign, readable street blades, and road-facing bus sign. The repaired expansion contains `145` anchored BaseParts, `0` invisible colliders, and all required replacement sidewalk/curb pieces are present.

**Reusable lesson:** Sidewalks should be generated as segmented runs around every road mouth and driveway, not as uninterrupted strips laid over intersections. Treat curb openings, pedestrian crossings, and sign sightlines as part of road geometry rather than later decoration.

## 2026-11-06 — Road kit standardized to Town Square width

**Request:** Make every straight, left-turn, right-turn, and four-way road piece match the Town Square road width.

**Implementation:** Rebuilt eight live road-piece models around their existing pivots using the shared Town Square profile: 32-stud asphalt, two 4-stud sidewalks, 0.4-stud road thickness, 0.5-stud sidewalk thickness, matching raised curbs, edge lines, and yellow center markings. Straight pieces remain 98 studs long. Turns now use three 32-stud asphalt sections with curved segmented center markings and a 68-stud footprint. Four-way intersections use five 32-stud sections with a 96-stud footprint. Every piece now has a `RoadPivot` PrimaryPart, width attributes, road connectors, and sidewalk connectors.

**Placement corrections:** Shifted `roadtype1` by `+12 Z`, aligned its nested straight to the four-way east connector at an exact `0.000`-stud gap, and shifted the loose `RightTurnRoad` by `+8 Z` to remove widening collisions.

**Backup:** `ServerStorage.RoadKitBeforeTownSquareWidth_193618`

**Verification:** Studio overview confirmed consistent widths and markings across straight roads, both turns, and all four-way copies. The standardized kit contains `8` road models and `218` BaseParts. All models report `RoadWidth = 32` and `SidewalkWidth = 4`; all parts are anchored, with `0` invisible colliders and `0` dimension failures.

**Reusable lesson:** When widening modular roads, preserve each model's pivot and orientation but re-evaluate connector offsets and every placed sample. A correct cross-section can still produce overlaps unless expanded intersections and turns are re-snapped after their footprint changes.

## 2026-11-06 — Cuckrolla equipped-item flip fix

**Request:** Prevent the Cuckrolla from flipping or tumbling when a player pulls out any item while inside the car.

**Diagnosis:** The prepared Starter Pulse was stable in an isolated driver-seat test, but the source audit found unsafe states elsewhere: several Tool templates had collidable/touch-enabled/non-massless parts, and three templates retained an anchored part. `EquipmentBagServer` cleaned collision and mass only when cloning catalog items, which did not cover arbitrary world-picked Tools and left a race for unsafe Backpack items equipped after sitting.

**Implementation:** Added `ServerScriptService.VehicleToolPhysicsGuard`. It recognizes `VehicleSeat` drivers and regular passenger `Seat` instances inside a vehicle Model. On seating, it sanitizes every Tool in both the Backpack and Character before equip, watches late-added Tools and descendants, and publishes `VehicleToolGuardActive` / `VehiclePhysicsSafe` diagnostic attributes. Tool parts are forced unanchored, non-colliding, non-touching, non-queryable, and massless. Updated `EquipmentBagServer.prepareTool` with the same complete safety properties and hardened all 61 BaseParts under `ServerStorage.EquipmentBagTools` at the source.

**Backup:** `ServerStorage.VehicleToolSafetyBefore_200351`

**Verification:** First confirmed the normal prepared Starter Pulse produced `0.000` chassis angular velocity while seated. Then created an intentionally unsafe 3-stud Tool with an anchored, collidable, touch/query-enabled, non-massless Handle. The new guard corrected every property while the Tool was still in the Backpack, before equip. After equipping and moving the Cuckrolla at 16 studs/second for 2.5 seconds, maximum angular velocity remained `0.000` and minimum chassis up-vector remained `1.000`. A separate regular passenger-seat test also passed. Final audit found `0` unsafe Equipment Bag template parts, the guard enabled, and no console errors.

**Reusable lesson:** Vehicle Tool safety must run before the grip is created, not only after a Tool appears in the Character. Sanitize seated players' Backpacks and equipped Tools, and cover regular passenger Seats as well as the driver VehicleSeat.

## 2026-11-06 — Cuckrolla equipped-item flip fix corrected

**Request:** The user reported that the first fix did not work: the Cuckrolla still twitched and barrel-rolled as soon as the Pulse was pulled out.

**Correction to the earlier entry:** The earlier unsafe-Tool verification did not represent live vehicle physics because the title flow had left `HumanoidRootPart` anchored. The Tool-part sanitation remains valid defense-in-depth, but it was not the complete cause or fix.

**Reproduction:** A clean control with the real Cuckrolla and no held Tool stayed upright. Equipping the real Starter Pulse caused violent rotation even after all Tool parts were massless/non-colliding, all character parts were made massless/non-colliding, the Pulse's seated grip animation was suppressed, and `RequiresHandle` was disabled. This isolated the remaining failure to the Roblox `Humanoid:EquipTool()` transition acting through the seated character/vehicle assembly, not to one bad decorative Pulse part.

**Implementation:** Reworked `ServerScriptService.VehicleToolPhysicsGuard`. It retains complete Tool sanitation, then creates a temporary `VehicleToolUprightGuard` `BodyGyro` on the vehicle chassis only while an occupant has a Tool equipped. `MaxTorque = (5e7, 0, 5e7)` and the upright target resist roll/pitch while zero Y torque leaves steering yaw alone. A short bounded recovery routine re-seats the same Humanoid if equip momentarily clears its seat. The stabilizer and `VehicleToolStabilizerActive` attribute are removed as soon as no occupant holds a Tool.

**Verification:** Used the actual `BurgGarageServer` spawn profile at the garage bay with the production Cuckrolla, R6 character, and Starter Pulse. Empty-hand control remained upright. With the Pulse equipped and the chassis moving, minimum/ending up-vector was `0.997`, the player stayed in the driver seat, the Tool remained held, the stabilizer was active, and speed reached about `39.68` studs/second. After unequip, the gyro was gone, the active attribute cleared, the player remained seated, and the chassis up-vector was `0.999`.

**Backups:** `ServerStorage.VehicleToolGripFixBefore_20261106` and `ServerStorage.VehicleToolStabilizerBefore_20261106` (in addition to the original `VehicleToolSafetyBefore_200351`).

**Reusable lesson:** A physics test is invalid if the avatar root or vehicle assembly is anchored. For vehicle/equipment bugs, reproduce with the production spawn path, verify finite/unanchored assembly physics, test the actual Tool, and validate both equip and unequip transitions. When the engine's equip transition itself introduces roll torque, use a temporary vehicle-side roll/pitch stabilizer rather than increasingly invasive Tool rewrites.

## 2026-11-06 — Place1 Schaumburg town foundation

**Request:** Use the whole empty Place1 baseplate to create a giant Schaumburg-inspired town foundation with streets, stores, and original ideas that can be continued later.

**Studio path:** `Workspace.SchaumburgTownBase` in the separate Studio project named `Place1`.

**Implementation:** Built a roughly 900 × 900-stud organized town grid with a 44-stud main boulevard pair, four 32-stud secondary roads, sixteen buildable blocks, segmented 5-stud sidewalks, curbs, markings, central crosswalks, and four cardinal road connectors. Added a brick civic plaza with a fountain, Veterans Gateway arch and clock tower; twelve named storefronts; five civic/public buildings; a high school; an apartment building; ten exterior-only houses; parking, transit shelters, streetlights, traffic signals, signs, benches, bike racks, trees and landscaping.

**Organization:** The root Model has eleven numbered folders and `11_MapConnectors.TownPivot` as its PrimaryPart. Exact dimensions, district names, store names, road coordinates and connector details are in [[22 - Place1 Schaumburg Town Base]].

**Verification:** Structural audit found `1,285` anchored BaseParts, `202` Models, `0` unanchored parts and `0` invisible colliders. Bounds are approximately `966 × 102.9 × 902` studs. Play mode spawned the player on the town-square brick plaza at about `(61.2, 6.0, 60.5)`, with Brick as the floor material. Aerial and street-level views confirmed the grid, storefronts, clock tower, fountain, traffic signals and road readability. No console errors appeared.

**Reusable lesson:** For a large starter town, establish the road hierarchy, block boundaries and expansion connectors first. Keep every district in a named folder and use exterior-only building shells so future gameplay interiors can replace individual buildings without rebuilding the map.

## 2026-11-06 — Place1 Schaumburg town foundation

**Request:** Use the whole empty Place1 baseplate to create a giant Schaumburg-inspired town foundation with streets, stores, and original ideas that can be continued later.

**Studio path:** `Workspace.SchaumburgTownBase` in the separate Studio project named `Place1`.

**Implementation:** Built a roughly 900 × 900-stud organized town grid with a 44-stud main boulevard pair, four 32-stud secondary roads, sixteen buildable blocks, segmented 5-stud sidewalks, curbs, markings, central crosswalks, and four cardinal road connectors. Added a brick civic plaza with a fountain, Veterans Gateway arch and clock tower; twelve named storefronts; five civic/public buildings; a high school; an apartment building; ten exterior-only houses; parking, transit shelters, streetlights, traffic signals, signs, benches, bike racks, trees and landscaping.

**Organization:** The root Model has eleven numbered folders and `11_MapConnectors.TownPivot` as its PrimaryPart. Exact dimensions, district names, store names, road coordinates and connector details are in [[22 - Place1 Schaumburg Town Base]].

**Verification:** Structural audit found `1,285` anchored BaseParts, `202` Models, `0` unanchored parts and `0` invisible colliders. Bounds are approximately `966 × 102.9 × 902` studs. Play mode spawned the player on the town-square brick plaza at about `(61.2, 6.0, 60.5)`, with Brick as the floor material. Aerial and street-level views confirmed the grid, storefronts, clock tower, fountain, traffic signals and road readability. No console errors appeared.

**Reusable lesson:** For a large starter town, establish the road hierarchy, block boundaries and expansion connectors first. Keep every district in a named folder and use exterior-only building shells so future gameplay interiors can replace individual buildings without rebuilding the map.
