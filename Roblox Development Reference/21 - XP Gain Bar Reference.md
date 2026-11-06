# XP Gain Bar Reference

Captured from the live Studio implementation on 2026-11-06.

## Studio paths

- `StarterPlayer.StarterPlayerScripts.ToolXPGainHUD` builds and animates the temporary gain bar.
- `ReplicatedStorage.ToolXPGained` is the server-to-client RemoteEvent.
- `ReplicatedStorage.ToolXPConfig` defines groups, rewards, level requirements, the cap, and the total-to-level calculation.
- `ServerScriptService.ToolXPService` validates awards, publishes player XP, saves totals, and fires the gain event.
- `StarterPlayer.StarterPlayerScripts.ToolXPMenu` is the separate full XP and level menu.
- Runtime data is published under `Player.ToolXP`.

## Purpose and event flow

The gain bar appears only after `ToolXPService.Award` accepts an XP award. The server calculates the before and after totals, updates the authoritative state, publishes the new attributes under `Player.ToolXP`, and fires:

```luau
ToolXPGained:FireClient(player, groupId, beforeTotal, afterTotal)
```

The client ignores unknown groups and any event where `afterTotal <= beforeTotal`. It derives the displayed level, current-level XP, required XP, fill fraction, and level color from the total. The client never decides how much XP to grant.

## Current XP rewards and validation

| Result ID | Group | XP |
|---|---|---:|
| `StarterPulseNormal` | PulseBar | 50 |
| `PulseNormal` | PulseBar | 100 |
| `PulseGhost` | PulseBar | 200 |
| `PenBlinker` | Penjamin | 500 |

The server requires a living character, the Tool equipped in that character, a Tool `XPGroup` matching the reward group, and an initialized player XP state. Pulse Bar awards have a 1.7-second group cooldown. Penjamin awards have a 4-second group cooldown and are restricted to Tools named `MXK`, `MuhaMed`, or `ACE`.

## Level progression

- Separate totals are maintained for `PulseBar` and `Penjamin`.
- Levels run from 1 through 100.
- Required XP for the current level is `level × 1000`.
- Per-group total cap is `5,050,000` XP.
- `ToolXPConfig.Progress(total)` clamps the total, subtracts completed level requirements, and returns `level, currentLevelXP, requiredXP, completed`.
- Level 100 completion is exposed as the `Completed` attribute.

## Visual layout

The HUD is generated at runtime as `PlayerGui.ToolXPGainHUD`.

| Element | Exact implementation |
|---|---|
| ScreenGui | `ResetOnSpawn = false`, `DisplayOrder = 25`, disabled while hidden |
| Root | `CanvasGroup` named `Progress`, centered at the top |
| Root size | 92% of viewport width, 95 px high, maximum 398 × 95 |
| Normal top offset | 20 px |
| Narrow-screen top offset | 72 px when the bar's track would begin left of x = 328, keeping the XP and Equipment tabs clear |
| Track | x = 20%, y = 15, width = 60%, height = 8 px |
| Track color | RGB 12, 13, 15 with a 1 px RGB 57, 60, 65 stroke |
| Fill | Current-level XP divided by required XP |
| Gain label | Right of the bar, `+N XP`, Gotham Medium, maximum 15 px |
| Level label | Large centered number, Gotham Black, 44 px |
| Group label | Centered below the number, Gotham Medium, 12 px |
| Text treatment | RGB 244, 244, 247 with a dark stroke at 0.18 transparency |

The gain label, level number, group name, and fill use the total sent by the server. `PulseBar` displays as “Pulse Bar” and `Penjamin` displays as “Penjamin.”

## Level colors

Levels between stops use `Color3:Lerp`.

| Level | RGB | Appearance |
|---:|---|---|
| 1 | 192, 192, 192 | Silver |
| 25 | 6, 64, 43 | Dark green |
| 50 | 0, 0, 128 | Navy |
| 75 | 75, 0, 110 | Purple |
| 99 | 139, 0, 0 | Dark red |
| 100 | 243, 175, 25 | Gold |

The color is applied to both the level number and the progress fill.

## Animation and repeated gains

- The HUD fades in over 0.23 seconds with Quad Out easing.
- The displayed total animates from `beforeTotal` to `afterTotal` over 0.62 seconds with Quad Out easing.
- It remains active for 4.5 seconds after the latest valid gain.
- It fades out over 0.5 seconds and then disables its ScreenGui.
- A new gain cancels the active progress tween and pending hide task.
- Consecutive gains for the same group add together in the label. Two quick 100-XP awards display `+200 XP`.
- A different group or a previously hidden HUD resets the accumulated label and starts from that event's `beforeTotal`.
- A revision counter prevents an older delayed fade from hiding a newer gain.

## Published player data

`Player.ToolXP` has a `SaveStatus` attribute and one Folder per configured group. Each group Folder has:

- `TotalXP`
- `Level`
- `XP`
- `RequiredXP`
- `Completed`

The full XP menu reads those attributes. The gain HUD receives authoritative before and after totals through `ToolXPGained`.

## Saving

Outside Studio, `ToolXPService` uses `ToolXP_v1`. It retries initial loading up to three times, autosaves every 60 seconds, retries during player removal, and attempts a final save during `BindToClose`. Per-session receipts inside `UpdateAsync` prevent the same session's earned XP from being added twice. Receipts older than seven days are removed.

Story Mode calls `BeginStory` with the selected Story slot's XP totals. Story XP is returned to `BurgStorySaves` through `GetTotals` and is saved with that Story file.

## Verification

A Studio Free Roam playtest fired the real `ToolXPGained` event with Penjamin totals of 24,000 to 24,500. The HUD displayed `+500 XP`, `Penjamin`, and its animated level progress. Two rapid Pulse Bar events of 100 XP each combined into `+200 XP`. The game console showed no XP system errors.

Related notes: [[09 - Currency XP and Game Systems]], [[15 - Live Script and System Register]], [[16 - Exact Gameplay Values and Data Contracts]], [[18 - Roblox Development Reflection Log]].
