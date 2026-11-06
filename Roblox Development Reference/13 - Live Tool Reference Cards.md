# Live Tool Reference Cards

Current Studio references for the handheld device family. Pair this with [[02 - Pulse Bar Interaction and R6 Animation]], [[03 - Pulse Sounds Smoke and Head Rush Effects]], and [[04 - MXK MuhaMed Tamu and Blinker Systems]].

## Shared Pulse construction

Each full Pulse variant contains:

- `Handle`: 0.70 × 1.30 × 0.50 studs, SmoothPlastic.
- `BlackScreen`: 0.10 × 1.10 × 0.30 studs, black Glass.
- Three `SilverSideFrame` Parts, normally Metal.
- `TopExtension`, representing the mouthpiece.
- `BlockyLEDDisplay` SurfaceGui under `BlackScreen`, including upper and lower digits.
- Side constellation SurfaceGuis with `Star` and `ConstellationLine` Frames.
- `PickupPrompt` on Handle: E, “Pick Up,” 8-stud range.
- `UseCompleted` RemoteEvent and `InspectRequested` BindableEvent.
- `HeldVisualAnimator` LocalScript, `ScreenUseCounter` Script, and `PickupHandler` Script.
- 11 Sounds in Handle and three EqualizerSoundEffects.

Shared starting values are top/battery `99`, bottom/juice `99`, one battery point per completed hit, and one juice point per 10 completed hits.

## Pulse variant colors

| Workspace Tool | Handle color | Head-rush tint | Equipment Bag ID |
|---|---|---|---|
| `blue razz blast pulse` | `#0989CF` | `#23ABE8` | `blue` |
| `dragon melo pulse` | `#FF66CC` | `#FF8E5C` | not registered |
| `dragon melon pulse` | `#FF3842` | `#FF443A` | `dragon` |
| `Fab pulse` | `#0D69AC` | `#28BE8B` | `fab` |
| `Green pulse` | `#5B9A4C` | `#9669E8` | not registered |
| `Meta moon pulse` | `#B480FF` | `#B4FF80` | `meta` |
| `Miami Mint pulse` | `#FFFFFF` | `#78EEC6` | `miami` |
| `Minneapolis Mint pulse` | `#0A0D11` | `#7091A6` | not registered |
| `test test` | `#111111` | `#787E8A` | not registered |

The production Equipment Bag deliberately exposes five Pulse variants: Fab, Meta, Miami, Dragon Melon, and Blue Razz Blast. The other Workspace variants are live world references or experiments.

## Pulse input and pose

- Single click/tap: Normal hit, 2 seconds.
- Second click within 1 second: Ghost hit, also 2 seconds.
- `X`: 3-second inspect animation.
- R6 pose render order: `Character + 1`.
- Use pose turns the screen toward the player, gives the device a 10° left lean, and positions the actual mouthpiece tip 0.07 studs in front of the head.
- R6 shoulder is solved from the device position so the arm remains attached and beside the Tool.
- R15 fallback uses an IKControl from right upper arm to right hand with a torso elbow pole.
- On equip, the script stores and restores the base Tool grip and cleans up all temporary attachments/IK on unequip or destruction.

## Pulse visual animation

- Runtime hit bar: 230 × 36 pixels, 92 pixels above the bottom center.
- Normal color: RGB 74, 238, 127.
- Ghost color: RGB 178, 105, 255.
- Fab and `test test` use the extended 792-line animator with side-art pulse support.
- Side constellation cycle: 0.9 seconds with a 2-second fade tail after the hit.
- The star/line system brightens toward white, varies transparency, and raises SurfaceGui brightness by up to 1.75.

## Pulse sound set

| Sound | Source | Volume |
|---|---|---:|
| `NormalClick` | bundled `button.wav` | 0.20 |
| `NormalInhale` | bundled `action_swim.mp3` | 0.13 |
| `GhostConfirm` | bundled electronic ping | 0.27 |
| `GhostInhale` | bundled `action_swim.mp3` | 0.15 |
| `NormalWhoosh` | asset `9113059730` | 0.40 |
| `GhostPuffSmall` | asset `9113059730` | 0.14 |
| `GhostPuffLarge` | asset `9113059730` | 0.23 |
| `BatteryBeep` | bundled electronic ping | 0.12 |
| `LowBatteryChirp` | bundled electronic ping | 0.30 |
| `LowJuiceTone` | bundled electronic ping | 0.30 |
| `EmptyClick` | bundled `button.wav` | 0.27 |

Equip chime is disabled. Low-battery warning plays twice at battery 15. Low-juice warning plays at juice 10.

## Penjamin-family construction

### MXK

- Bounds: 0.4 × 0.8 × 0.3; 26 descendants.
- `Handle` is a 0.35 × 0.80 × 0.20 UnionOperation.
- Screen, three neon Blinker lights, oil SurfaceGui, and PickupPrompt.
- Equipment Bag ID `mxk`; XP group `Penjamin`.

### ACE

- Bounds: 0.4 × 0.8 × 0.3; 30 descendants.
- `Handle` is black SmoothPlastic, 0.40 × 0.80 × 0.28.
- Screen plus three lavender neon lights.
- Equipment Bag ID `ace`; XP group `Penjamin`.

### MuhaMed

- Bounds: 0.4 × 1.0 × 0.5; 33 descendants.
- Black 0.25 × 1.00 × 0.50 Handle UnionOperation.
- `Screen`, `OilDisplayFace`, `RearAccent`, `TopCapInner`, and `TopCapOuter`.
- The display is intentionally oriented `UprightScreenOut` and faces the player in use.
- Equipment Bag ID `muha`; XP group `Penjamin`.

### NOVA

- Bounds: 0.6 × 0.9 × 0.4; 85 descendants.
- 36 Parts and 35 WeldConstraints.
- Ten named Blinker lights plus a visible oil reservoir.
- Key geometry includes `BodyCore`, `LowerShell`, seven `GripRib` Parts, `OffsetMouthpiece`, `MouthpieceCollar`, `MouthpieceOpening`, display bezel, reservoir recess/ticks/top/bottom, rear spine, side button, and upper shoulder.
- `VisibleOilController` scales the oil window from 0.002 to 0.235 studs tall while keeping the reservoir bottom fixed.
- Not currently registered in the Equipment Bag catalog and has no XPGroup attribute.

## Shared Penjamin attributes

- `OilPercent = 100`
- `OilUsePerBlinker = 1`
- `BlinkerHoldSeconds = 10`
- `BlinkerSkillChecks = 5`
- `BlinkerSkillMinimumSeconds = 4`
- `FailedTimingEndsHit = true`
- `CoughSmokePuffs = 18`
- `RigType = R6`
- `PickupMode = ProximityPrompt`
- `HeldPositionRaised = true`
- `GripOrientation = Upright` or MuhaMed’s `UprightScreenOut`

All world Penjamins disable collision/touch, make Parts massless, clear assembly velocity, anchor only while lying in Workspace, and unanchor when picked up. This is the fix that prevents equipping from flinging or slowing the character.
