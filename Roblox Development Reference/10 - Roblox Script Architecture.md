# Roblox Script Architecture

## Pulse Tool structure

Common Tool children:

- `Handle`
- `TopExtension`
- `BlackScreen`
- Silver/chrome frame pieces
- Side SurfaceGuis and decorative details
- `UseCompleted`
- `InspectRequested`
- `HeldVisualAnimator` LocalScript
- `ScreenUseCounter` server Script
- `PickupHandler` server Script
- Sound objects under the Handle

## HeldVisualAnimator responsibilities

- Handle R6/R15 mouth pose.
- Detect Normal and Ghost activation.
- Enforce cooldown and double-tap window.
- Display and update the hit progress bar.
- Fire `UseCompleted` after the animation actually completes.
- Animate side constellation artwork where present.
- Handle the X inspection action.
- Restore grips, shoulder transforms, sounds, GUI, and artwork on unequip.
- Fire `PulseHeadRushEvent` with the tool's tint after a completed use.

## ScreenUseCounter responsibilities

- Decrease top value by 1 per completed use.
- Track use count for bottom juice decrement every 10 uses.
- Update segmented screen text.
- Trigger low/empty warnings at configured thresholds.
- Keep authority on the server.

## Shared player scripts

### PickupPromptFirstPersonFix

Location: `StarterPlayer.StarterPlayerScripts.PickupPromptFirstPersonFix`

- Desktop: disables clickable prompt mouse hitboxes.
- Touch-only: leaves normal tap behavior intact.
- Configures existing and newly added prompts.

### PulseHeadRushController

Location: `StarterPlayer.StarterPlayerScripts.PulseHeadRushController`

- Listens to `ReplicatedStorage.PulseHeadRushEvent`.
- Creates/reuses BlurEffect and ColorCorrectionEffect.
- Animates blur, FOV, tint, contrast, saturation, and brightness.
- Cancels/restarts safely if another hit happens.
- Restores the original camera FOV.

## MXK/NOVA/MuhaMed structure

- `OilDisplayController`
- Optional `VisibleOilController`
- `BlinkerClient`
- `BlinkerServer`
- Tool-specific lights, screen, Handle, pickup prompt, and RemoteEvents

The Blinker server should validate completion rather than trusting a client claiming a ten-second hold.

## Useful attributes

Pulse tools:

- `TopNumberValue`
- `BottomNumberValue`
- `DoubleTapWindow`
- `InspectDuration`
- `HeadRushEnabled`
- `HeadRushTintColor`

Buildings:

- `BuildOrigin`
- `ExteriorOnly`
- `ExteriorFinished`
- Optional backup or style attributes

## Cleanup rule

Every LocalScript that binds RenderStepped, ContextActionService, events, IK controls, or temporary GUI must disconnect/unbind/destroy and restore state during:

- Unequip
- Character death or respawn
- Script destruction
- Tool destruction
- Interrupted animation

