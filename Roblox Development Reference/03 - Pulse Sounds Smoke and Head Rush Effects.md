# Pulse Sounds, Smoke, and Head-Rush Effects

## Sound specification

Original requested sound set:

1. Equip: short electronic startup chime.
2. Normal hit: quiet activation click followed by a two-second inhale.
3. Ghost hit: double-click confirmation sound with a deeper inhale.
4. Normal smoke: soft forward whoosh or exhale.
5. Ghost smoke: small puff followed by a stronger puff after 0.5 seconds.
6. Battery decrease: subtle digital beep.
7. Low battery at 15: warning chirp.
8. Empty battery: dry click with no hit animation.
9. Low juice at 10: a separate warning tone.

Later sound adjustments:

- Replace unnecessary beeping with believable exhale/breathing sounds.
- Remove the first beep/startup sound when equipping the tool.
- Increase the exhale volume slightly while keeping the same audio asset.

## Smoke specification

### Normal Pulse hit

- Smoke originates near the lower front of the player's face/mouth.
- Travels mostly straight forward.
- Expands and fades naturally.
- Should not originate from the center of the head or behind the player.

### Ghost Pulse hit

- First puff is small.
- Second, stronger puff appears approximately **0.5 seconds later**.
- Total Ghost smoke should still be less than the Normal hit smoke.

## Head-rush visual effect

A shared client system applies a mild first-person lightheadedness effect after a completed Pulse hit.

- Smooth blur increase followed by a return to zero.
- Mild pulsing FieldOfView expansion and contraction.
- ColorCorrection tint matching the active Pulse Bar.
- Normal effect duration: about **3.1 seconds**.
- Ghost effect duration: about **3.5 seconds** and slightly stronger.
- FOV must return exactly to the original camera value.
- Blur and ColorCorrection must reset completely.
- Do not rotate or seize control of the camera.

Current shared objects:

- `ReplicatedStorage.PulseHeadRushEvent` — BindableEvent.
- `StarterPlayer.StarterPlayerScripts.PulseHeadRushController` — LocalScript.
- `Lighting.PulseHeadRushBlur` — client-created BlurEffect.
- `Lighting.PulseHeadRushColor` — client-created ColorCorrectionEffect.

Tool attributes:

- `HeadRushEnabled`
- `HeadRushTintColor`

Very dark body colors are lifted slightly in the screen effect so the display does not simply turn black.

