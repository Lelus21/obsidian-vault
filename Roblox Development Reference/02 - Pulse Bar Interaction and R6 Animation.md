# Pulse Bar Interaction and R6 Animation

## Pickup and equipping

- Pulse Bars can be picked up during playtesting and moved into the player's Backpack.
- Interaction uses a ProximityPrompt with a keyboard pickup key such as **E**.
- Desktop prompts must not capture the centered first-person cursor.
- Mobile players retain tap interaction.
- Equipped tools must not fling the character, slow walking, or alter turning behavior.

## Normal hit

- Activated by one click or one tap.
- Lasts approximately **2 seconds**.
- Tool moves toward the player's mouth.
- Only the mouthpiece tip approaches the lower front of the face.
- Tip must stop just before entering the head.
- Screen remains oriented sensibly and should not become heavily tilted.

## Ghost hit

- Activated by tapping/clicking twice within the double-tap window.
- Original requested window: about **1 second**.
- Uses a slightly deeper inhale and separate confirmation feedback.
- Smoke behavior differs from a normal hit; see [[03 - Pulse Sounds Smoke and Head Rush Effects]].

## R6 pose requirements

- Game uses R6; do not add a second rig-conversion system that conflicts with Roblox's R6 setting.
- Earlier bug: the arm moved behind the player, as if the shoulder rotation was reversed.
- The right arm/hand pose should be calculated from the tool's actual target position.
- The arm should remain connected visually to the torso.
- The tool screen should face the player while using or inspecting it.
- During use, apply only a slight left tilt, approximately 10 degrees.
- The hand should stay beside the Tool instead of appearing above it.
- For R15 compatibility, an `IKControl` can target attachments at the mouth and inspection position.
- For R6, adjust the `Right Shoulder` Motor6D `C0`, preserving and restoring its original value.

## Inspect animation

- Press **X** or controller `ButtonX` while holding the Pulse Bar.
- Turn the device so its screen faces the player.
- Inspection should not begin while inhaling, on cooldown, or already inspecting.
- Restore the normal grip and arm pose after inspection.

## Hit progress GUI

- Small bar above the player's inventory/hotbar.
- Must not dominate the screen because normal hits are short.
- Normal hit label: `NORMAL HIT`.
- During the double-tap window, it can say `NORMAL HIT • TAP AGAIN FOR GHOST`.
- Ghost hit label: `GHOST HIT`.
- Normal fill color: green.
- Ghost fill color: purple.
- Hide the bar after the hit completes or is cancelled.

## Screen counters

- Top number represents battery for Pulse Bars.
- Top number decreases by **1 every completed use**.
- Bottom number represents juice.
- Bottom number decreases by **1 every 10 completed uses**.
- It may take multiple animations before the bottom number visibly changes.
- Low-battery warning threshold: **15**.
- Low-juice warning threshold: **10**.
- Empty battery: play a dry click and do not start the animation.

