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

## Cuckrolla flips when an item is equipped

Symptom:

- The car is stable while driving normally.
- Pulling out a Tool while seated can make the vehicle receive violent torque, flip, or tumble.

Cause:

- Some stored and world-picked Tools can reach the seated character with an anchored, collidable, touch-enabled, queryable, or non-massless part.
- The unsafe Tool can join or contact the occupied vehicle assembly during Roblox's equip frame.
- Sanitizing only after the Tool enters the Character leaves a short race where an unsafe Backpack Tool can be gripped first.

Fix:

- `ServerScriptService.VehicleToolPhysicsGuard` recognizes driver and passenger seats inside vehicle Models.
- As soon as a player sits, it sanitizes Tools in both the Character and Backpack before they can be equipped.
- Late-added and newly equipped Tools are also sanitized.
- Every Tool BasePart becomes unanchored, non-colliding, non-touching, non-queryable, and massless.
- `EquipmentBagServer.prepareTool` now applies the same complete property set.
- All 61 BaseParts under `ServerStorage.EquipmentBagTools` are stored in the safe state.

Verification:

- An intentionally unsafe test Tool began anchored, collidable, touch/query enabled, and non-massless.
- While the player occupied the driver seat, it was corrected in the Backpack before equip.
- After equipping and moving the Cuckrolla at 16 studs/second, maximum chassis angular velocity remained `0.000` and the chassis up-vector stayed `1.000`.
- The same pre-equip sanitation passed from a regular passenger `Seat`.
- Backup: `ServerStorage.VehicleToolSafetyBefore_200351`.

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

