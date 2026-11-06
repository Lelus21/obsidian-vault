# MXK, MuhaMed, Tamu, and Blinker Systems

## MXK screen

- Screen part is named `Screen`.
- Replace `Battery` or `Oil %` with the word **Oil**.
- Numeric value includes a percent sign, for example `100%`.
- Percentage bar sits vertically along the **left side** of the screen.
- Leave equal small spacing above and below the bar.
- Reposition text to accommodate the vertical bar.
- MXK has Oil only; do not show a separate battery value.

## MXK pickup and use

- Tool must be pickable and equippable without flinging or slowing the player.
- Tool is held to the player's mouth during use.
- Fix grip so the tool is upright rather than flipped over.
- R6 arm stays connected to the torso and follows the Tool position.
- Physical pieces should be welded, non-colliding where appropriate, and massless except for the Handle.

## Blinker hold system

- Player holds click or touch for up to **10 seconds**.
- Completing 10 seconds achieves a Blinker.
- Three neon lights on the opposite side of the screen flash rapidly black and white at completion.
- The lights already exist on the model and should be animated rather than replaced.

## Circular timing minigame

Inspired by the Flee the Facility computer timing meter.

- Circular meter is larger and easy to read.
- White moving segment travels repeatedly around the circle.
- Player must time the input successfully **five times in a row**.
- Speed increases after each success.
- The meter does not disappear after only one attempt.
- A failed timing attempt ends the use.
- On failure, the player still hits the tool and then coughs smoke outward.

## MXK smoke scaling

Smoke varies with held duration instead of displaying numeric hit-size labels:

- About 1–2 seconds: barely any smoke.
- About 3 seconds: similar to a normal Pulse hit.
- About 5–6 seconds: roughly double the 3-second amount.
- About 7–9 seconds: more than the 5–6 second tier.
- 10-second Blinker: largest balanced smoke output.

## MuhaMed

- Screen displays **Oil** and a percentage such as `100%`.
- Remove the battery concept.
- Give MuhaMed the same Oil, hold, minigame, smoke, pickup, and use systems as MXK.
- Rotate the MuhaMed Tool during use so the screen faces the player.

## Tamu

- Requested screen number system similar to the Pulse screen.
- Target screen part name: `Screen`.
- If converted to the newer system, use the same clear Oil/percentage conventions unless the tool is intentionally battery-based.

## Relevant scripts

- `OilDisplayController`
- `VisibleOilController` where present
- `BlinkerClient`
- `BlinkerServer`
- Tool-specific RemoteEvents and attributes used by the client/server pair

