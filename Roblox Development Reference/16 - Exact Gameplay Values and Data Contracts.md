# Exact Gameplay Values and Data Contracts

Use this note when changing balance or wiring a new compatible model.

## Pulse values

| Setting | Value |
|---|---:|
| Normal hit duration | 2.0 seconds |
| Ghost hit duration | 2.0 seconds |
| Double-tap window | 1.0 second |
| Server completion cooldown | 1.7 seconds |
| Inspect key/duration | X / 3.0 seconds |
| Starting battery | 99 |
| Battery cost | 1 per completed hit |
| Starting juice | 99 |
| Juice cost | 1 per 10 completed hits |
| Low battery warning | exactly 15 |
| Low juice warning | exactly 10 |
| Normal smoke | 12 puffs, scale 1.0 |
| Ghost smoke | 2 puffs, then 5 after 0.5 seconds |
| Normal XP | 100 Pulse Bar XP |
| Ghost XP | 200 Pulse Bar XP |

Important Tool attributes: `TopNumberValue`, `BottomNumberValue`, `TotalCompletedUses`, `UsesPerJuiceDecrease`, `JuiceUsesTowardDecrease`, `HeadRushEnabled`, `HeadRushTintColor`, `XPGroup`, `EquipmentBagId`, `InspectDuration`, and `LastHitType`.

## Blinker values

| Setting | Value |
|---|---:|
| Checks required | 5 in a row |
| Target angle/window | 38° / ±16° |
| Lap times | 2.40, 2.05, 1.72, 1.42, 1.16 seconds |
| Intended full hold | 10 seconds |
| Server minimum for successful Blinker | 4 seconds |
| Timing-success spam guard | 0.20 seconds |
| Starting oil | 100% |
| Oil cost | 1 per accepted smoke-producing hit or cough |
| Blinker light flash | 12 steps, 0.075 seconds each |
| Successful Blinker XP | 500 Penjamin XP |
| Failed Blinker XP | 0 |

Partial release smoke tiers:

| Held duration | Tier | Puffs | Size | Travel |
|---|---|---:|---:|---:|
| under 0.9s | TooShort | 0 | 0 | 0 |
| 0.9–2.49s | Light | 3 | 0.65 | 0.70 |
| 2.5–4.49s | Normal | 12 | 1.00 | 1.00 |
| 4.5–6.99s | Long | 24 | 1.10 | 1.10 |
| 7.0–9.99s | Heavy | 32 | 1.18 | 1.22 |
| successful Blinker | Blinker | 42 | 1.28 | 1.35 |

Failure smoke is 18 total puffs in bursts of 4, 8 and 6 separated by 0.16 and 0.20 seconds.

## XP progression

- Maximum level: 100.
- Required XP for the next level: `level × 1000`.
- Total cap: `1000 × 100 × 101 / 2 = 5,050,000 XP` per group.
- Pulse reward cooldown: 1.7 seconds.
- Penjamin reward cooldown: 4 seconds.
- Penjamin XP is restricted to Tools named `MXK`, `MuhaMed`, or `ACE` with `XPGroup = Penjamin`.
- DataStore: `ToolXP_v1` outside Studio. Studio uses session-only XP.

## Equipment Bag catalog

Categories: `PulseBar` and `Penjamin`.

| ID | Display name | Workspace source | Category |
|---|---|---|---|
| `fab` | Fab Pulse | `Fab pulse` | PulseBar |
| `meta` | Meta Moon Pulse | `Meta moon pulse` | PulseBar |
| `miami` | Miami Mint Pulse | `Miami Mint pulse` | PulseBar |
| `dragon` | Dragon Melon Pulse | `dragon melon pulse` | PulseBar |
| `blue` | Blue Razz Blast Pulse | `blue razz blast pulse` | PulseBar |
| `mxk` | MXK | `MXK` | Penjamin |
| `ace` | ACE | `ACE` | Penjamin |
| `muha` | MuhaMed | `MuhaMed` | Penjamin |

Templates live at `ServerStorage.EquipmentBagTools.<id>`. Keep the template scripts and attributes synchronized with the Workspace reference before shipping changes.

## Remote and bindable contract

- `Tool.UseCompleted` RemoteEvent: client sends `Normal` or `Ghost` after the animation completes.
- `Tool.BlinkerRequest` RemoteEvent actions: `Begin`, `TimingSuccess`, `TimingMiss`, `Release`, `Finish`, `Cancel`.
- `ReplicatedStorage.PulseHeadRushEvent` BindableEvent: local animator fires tint and hit type; local controller consumes it.
- `ReplicatedStorage.EquipmentBag.Equip` RemoteEvent: requests an Equipment Bag item by catalog ID.
- `ReplicatedStorage.SchoolFootball.Action` RemoteEvent: shared football action channel.
- `ServerScriptService.TheVibeSmokeEmission` BindableEvent: receives position, puff count, size multiplier and travel multiplier from tool smoke.
- `ReplicatedStorage.BurgDream.ExitTransition` RemoteEvent: dream exit presentation.
- `ReplicatedStorage.BurgWardrobe.Session` RemoteEvent: wardrobe open/close session state.
- Burg front-end functions/events: `ListStorySaves`, `StartGame`, `SaveAndSleep`, `EnterDream`, and `SleepRequest`.

## Story save contract

- DataStore: `BurgStorySlots_v1`.
- Two Week One slots.
- Current fixed story date: Monday, October 26th, Week 1.
- Saved fields: Version, Week, Day, Date, Money, XP totals, SavedAt, Revision and WriteId.
- Revision comparison prevents one session from overwriting a newer save.

## Client preference attributes

- `BurgMusicEnabled` default true.
- `BurgUIEffectsEnabled` default true.
- `BurgRoomUIEffectsEnabled` default true.
- `BurgFOV` default 70, clamped 60–120.
- `BurgCameraOverride` prevents normal FOV/camera writers from fighting phone, wardrobe or another special view.
- `BurgTitleActive` suppresses gameplay UI effects and certain inputs while the title screen is active.
