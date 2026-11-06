# Bugs, Fixes, and Lessons Learned

## First-person mouse becomes stuck near prompts

Symptom:

- WASD movement continues.
- Mouse cannot turn the camera when the centered cursor is over an `E` prompt.

Cause:

- Desktop `ProximityPrompt.ClickablePrompt` hitboxes capture the centered first-person mouse.

Fix:

- `StarterPlayer.StarterPlayerScripts.PickupPromptFirstPersonFix` sets `ClickablePrompt = false` for desktop players on all ProximityPrompts.
- Keyboard and gamepad interaction continue normally.
- Touch-only players keep Roblox tap interaction.
- The fix also configures prompts added later through `Workspace.DescendantAdded`.

## Tool flings or slows the character

Likely causes:

- Tool pieces collide with the avatar or world.
- Decorative parts have mass.
- Tool pieces are not welded to the Handle.
- Anchored parts remain inside an equipped Tool.
- Incorrect grip offsets force geometry into the character.

Fix pattern:

- Only the world pickup is anchored; equipped Tool parts must be unanchored.
- Weld all visible parts to `Handle`.
- Set decorative parts `Massless = true`.
- Disable collisions, touches, and unnecessary queries on decorative pieces.
- Keep the Handle compact and correctly aligned.

## R6 arm moves backward or disconnects visually

- Preserve the original `Right Shoulder.C0`.
- Calculate the target from the Tool's actual desired Handle position.
- Account for `RightGrip` and the current Tool grip transform.
- Do not aim the arm at an unrelated face coordinate.
- Restore `C0` after use, inspection, unequip, or script destruction.

## Tool enters the player's head

- Find the mouthpiece tip in Handle object space.
- Position that tip just in front of the lower face.
- Calculate the desired Handle CFrame from the tip target.
- Blend the correction rather than teleporting the Tool abruptly.

## House roof gaps and protruding walls

- Wall height must stop below the roof plane unless it intentionally fills a gable.
- Fill triangular gable areas completely.
- Close inner walls where two wings meet; a hollow filler still needs every exterior face.
- Add roof-to-wall flashing so overlapping roof sections look intentional.
- Inspect from above because street-level views can hide major holes.

## Interior project became messy

- Avoid building rooms without a locked floor plan.
- Confirm stairs, halls, doors, and room access before decorating.
- Use one material/color system throughout.
- If the building is only background scenery, use a hollow exterior rather than an unnecessary interior.

