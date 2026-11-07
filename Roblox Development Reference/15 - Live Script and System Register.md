# Live Script and System Register

This register describes active production code. Dated ServerStorage copies are documented separately in [[17 - Backups Duplicates and Maintenance Notes]].

## Pulse Bars

### `HeldVisualAnimator` — LocalScript

Production variants share a 753-line implementation; Fab and `test test` use a 792-line version with side-star pulsing.

Responsibilities:

- Builds the runtime Normal/Ghost hit bar.
- Distinguishes a single tap from a second tap inside the one-second Ghost window.
- Runs the two-second inhale and fires `UseCompleted` only after completion.
- Plays inhale/click/confirmation sounds.
- Calculates R6 shoulder C0 and Tool Grip from the real Handle and TopExtension geometry.
- Provides an R15 IK fallback.
- Binds X to inspect, making the screen face the player.
- Fires the shared `PulseHeadRushEvent` with the Tool tint and hit type.
- Fab version animates constellation SurfaceGuis.

### `ScreenUseCounter` — server Script, 221 lines

- Validates that the Tool is equipped and rate-limits completions to 1.7 seconds per player.
- Rejects battery-zero use with `EmptyClick`.
- Creates expanding server smoke Parts and forwards exact emissions into the shared room-smoke BindableEvent.
- Awards Tool XP after a valid completion.
- Decrements counters, refreshes digit labels, and triggers low-resource sounds.

### `PickupHandler` — server Script, 48 lines

- Enables the prompt and Handle collision only when the Tool is in Workspace.
- Moves the Tool into the player Backpack and equips it.
- Disables collision while equipped and refreshes prompt state after ancestry changes.

### `PulseHeadRushController` — LocalScript, 146 lines

- Creates/reuses `PulseHeadRushBlur` and `PulseHeadRushColor` in Lighting.
- Normal effect: 3.1 seconds, peak blur 8.5, FOV increase 3.8, tint strength 0.24.
- Ghost effect: 3.5 seconds, peak blur 11, FOV increase 5, tint strength 0.30.
- Smooth 0.38-second attack and release with a 0.78-second FOV/blur pulse.
- Respects title screen, UI-effect preference, FOV preference, and camera overrides.

## Penjamin Blinker system

### `BlinkerClient` — LocalScript, about 568 lines

- Creates a 230 × 230 circular timing UI.
- Player holds click/touch and presses E, gamepad X, or the center touch button when the white marker crosses the red target.
- Requires five consecutive successes.
- Lap times accelerate through 2.40, 2.05, 1.72, 1.42, and 1.16 seconds.
- Target angle is 38° with a ±16° timing window.
- Any miss resets the streak, sends `TimingMiss`, ends the hit and displays “MISSED — COUGH!”
- Solves R6 Tool and shoulder pose from the actual device position with an 8° lean.

### `BlinkerServer` — Script, about 331 lines

- Handles world pickup and physics safety.
- Server-validates equipped state, oil, event order, timing-success spacing, five-hit streak and minimum duration.
- A full Blinker flashes marked light Parts black/white 12 times at 0.075-second intervals.
- Consumes oil and awards 500 Penjamin XP only for a successful Blinker.
- Emits scaled smoke for partial releases and staggered cough smoke after failure.

### Oil display scripts

- `OilDisplayController` writes `Oil` and `NN%` to the SurfaceGui and moves the vertical bar on the left.
- MuhaMed uses a dedicated display face/orientation.
- NOVA adds `VisibleOilController`, which physically scales its reservoir fill.

## XP and Equipment Bag

### `ToolXPService`

- Server-authoritative award validation and cooldowns.
- Publishes `PulseBar` and `Penjamin` folders under `Player.ToolXP` with TotalXP, Level, XP, RequiredXP, Completed and SaveStatus.
- Uses `ToolXP_v1` outside Studio; autosaves every 60 seconds and retries on removal/BindToClose.
- Session receipts prevent duplicate increments from a repeated UpdateAsync.
- Fires `ReplicatedStorage.ToolXPGained` with group ID, authoritative before-total, and authoritative after-total when an award increases XP.

### `ToolXPGainHUD`

- Builds a temporary top-center XP gain bar from the `ToolXPGained` event.
- Shows accumulated `+N XP`, tool-group name, large level number, and current-level progress.
- Interpolates the level/fill color through silver, dark green, navy, purple, dark red, and level-100 gold.
- Fades in over 0.23 seconds, animates progress over 0.62 seconds, waits 4.5 seconds after the latest gain, then fades out over 0.5 seconds.
- Combines rapid gains for the same group and resets when the group changes.
- Moves from y = 20 to y = 72 on narrow screens to clear the top-left XP and Equipment tabs.
- Full exact reference: [[21 - XP Gain Bar Reference]].

### Equipment Bag

- `EquipmentBagServer` grants registered templates from `ServerStorage.EquipmentBagTools`, tracks selected ID and prevents duplicates.
- `EquipmentBagUI` builds the searchable category UI and preview display at runtime.
- `EquipmentBagHotbar` keeps the Roblox backpack UI visible.
- `ReplicatedStorage.EquipmentBag.Equip` is the client/server equip RemoteEvent.

## Front end, saves and personal systems

- `BurgTitleClient`: builds the title/settings interface, suppresses gameplay controls while active, controls FOV and opens the XP menu.
- `BurgTitleServer`: prepares players and handles StartGame/story selection.
- `BurgStorySaves`: two Week One save slots using `BurgStorySlots_v1`; saves money and both XP totals with revision conflict protection.
- `BurgSleepClient` / `BurgSleepServer`: sleep prompt, fade/interaction and story save; can enter the dream world.
- `BurgDreamService` / `BurgDreamClient`: teleports into/out of `BurgDreamWorld` and manages transition state.
- `BurgWardrobeServer` / `BurgWardrobeClient`: opens the bedroom wardrobe station, applies clothing categories, and safely manages mouse/camera override state.
- `BurgDeskSeatingClient` plus `DeskChairSeating`: hides competing prompts and manages the bedroom desk seat.
- `BurgPhoneClient`: phone UI, messages/apps, camera mode, Roblox capture/export, and Flappy Bird module.
- `ClientSettings`: music routing, UI-effect preferences, room-effect preferences, and 60–120 FOV preference.

## School systems

- `SchoolScanInController`: main/east scanner gates and player checked-in attributes.
- `EntranceDoorController`: tweened school entrance doors.
- `SchoolFacilitiesController`: tagged doors, water buttons, flow streams and drinking fountains.
- `SchoolRestroomController`: bathroom doors, stalls, locks, sinks and flush interactions.
- `SchoolStallPrompts`: client-side prompt visibility based on stall side, lock and occupancy.
- `CafeteriaStaffController`: lunch worker routes, requests, cooking, serving and order state.
- `LunchWorkerRig`: worker animation/pose/dialogue module.
- `CafeteriaFoodFactory` and `CafeteriaMeals`: visual food construction and consumable Tool creation.
- `GymActivities`: ball cart, basketball ownership, dribbling, stealing, shooting and scoring.
- `SchoolBasketballInput`: client charge, hand selection, target choice and shot feedback.
- `BasketballShotModel`, `BasketballTrajectory`, `BasketballPossession`: shared shot probability, ballistic solution and steal/transfer rules.
- `SchoolFootballService`: authoritative pickup, possession, throwing, catching, diving, hitsticks and recovery.
- `SchoolFootballInput`: client throw-power UI, actions and R6 pose/recovery presentation.
- `CatchMath`: segment-based body/hand reach checks with no ball attraction or teleporting.
- `StadiumScanInController`, `StadiumMasterLightingController`, and `CampusNightLighting`: stadium entry and lighting systems.
- `SchoolRoomSmokeController` / `SchoolRoomSmokeVisuals`: room mass/density, portals, settling and client overlay/emitters.

## The Vibe systems

- `CashierBehavior`: 476-line cashier state machine covering movement, dialogue, routines, cooking, serving, MXK use and smoke response.
- `CashierTalkController`: queues talk/jobs and exposes action/error attributes.
- `FoodFactory`: procedural visual foods.
- `FoodService`: prepared-food slots, serving count, Tools and consumption state.
- `RoomSmokeSystem`: room volumes, smoke mass, density, settling, open-door exchange and visibility scaling.
- `RoomSmokeController`: steps the simulation and receives `ServerScriptService.TheVibeSmokeEmission`.
- `TheVibeSmokeVisuals`: local smoke grids/overlays, respecting room UI-effect settings.
- Three `DoorController` scripts tween the entry and two restroom doors.

## World utility scripts

- `PickupPromptFirstPersonFix`: sets `ClickablePrompt = false` on desktop prompts so centered first-person mouse look is not captured; touch-only prompts remain clickable.
- `ProximityPromptLayout`: finds prompts sharing a carrier and offsets/layouts them using `PromptLayoutBaseOffset`.
- `VehicleToolPhysicsGuard`: detects driver and passenger vehicle seats; sanitizes every Backpack/equipped Tool; and, only while a Tool is held, adds a chassis `VehicleToolUprightGuard` that blocks roll/pitch torque without blocking steering yaw. It also restores a briefly lost seat after equip and removes the stabilizer immediately on unequip/exit.
- `MarketSquarePlazaDoors`: initializes and tweens attribute-tagged plaza doors.
- House door/window/covering controllers: generic TweenService implementations driven by instance attributes.

## Active source manifest

The following paths/groups account for the active source containers found outside ServerStorage backups:

- `ReplicatedStorage`: `BurgFrontEnd.ClientSettings`, `EquipmentBag.Catalog`, `PhoneSystem.FlappyBird`, `SchoolFootball.Config`, `SchoolFootball.CatchMath`, `ToolXPConfig`, and `ToolXPGained`.
- `ServerScriptService`: `BurgDreamService`, `BurgSleepServer`, `BurgStorySaves`, `BurgTitleServer`, `BurgWardrobeServer`, `EquipmentBagServer`, `MarketSquarePlazaDoors`, `ProximityPromptLayout`, `SchoolFootballServer`, `SchoolFootballService`, `ToolXPBootstrap`, `ToolXPService`, and `VehicleToolPhysicsGuard`.
- `StarterPlayerScripts`: `BasketballStealPrompts`, `BurgDeskSeatingClient`, `BurgDreamClient`, `BurgDreamTraderVisuals`, `BurgPhoneClient`, `BurgSleepClient`, `BurgTitleClient`, `BurgWardrobeClient`, `EquipmentBagHotbar`, `EquipmentBagUI`, `PickupPromptFirstPersonFix`, `PulseHeadRushController`, `SchoolBasketballInput`, `SchoolFootballInput`, `SchoolRoomSmokeVisuals`, `SchoolStallPrompts`, `TheVibeSmokeVisuals`, `ToolXPGainHUD`, and `ToolXPMenu`.
- Pulse Tools: each live Pulse has `PickupHandler`, `HeldVisualAnimator`, and `ScreenUseCounter`.
- Penjamin Tools: MXK, ACE, MuhaMed and NOVA have `BlinkerClient`, `BlinkerServer`, and `OilDisplayController`; NOVA also has `VisibleOilController`.
- School: `BasketballPossession`, `BasketballShotModel`, `BasketballTrajectory`, `CafeteriaFoodFactory`, `CafeteriaMeals`, `CafeteriaStaffController`, `CampusNightLighting`, `EntranceDoorController`, `GymActivities`, `LunchWorkerRig`, `SchoolFacilitiesController`, `SchoolRestroomController`, `SchoolRoomSmokeController`, `SchoolScanInController`, `StadiumMasterLightingController`, and `StadiumScanInController`.
- The Vibe: `CashierBehavior`, `CashierTalkController`, `FoodFactory`, `FoodService`, `RoomSmokeController`, `RoomSmokeSystem`, entry `DoorController`, and two restroom `DoorController` copies.
- Houses: `besthouse` has four active controllers; `thetesthouse` has door and window controllers; `test house` has `DoorInteraction`.
- Other Workspace systems: `BurgDreamWorld.XPTokenTrader.TraderInteraction` and `MarketSquarePlaza...LuxuryWorkerIdle`.

The small `SchoolFootballServer` and `ToolXPBootstrap` Scripts are one-line entry points that require/start their corresponding service ModuleScripts.
