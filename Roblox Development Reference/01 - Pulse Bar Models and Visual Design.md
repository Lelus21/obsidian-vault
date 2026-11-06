# Pulse Bar Models and Visual Design

## Core prop specification

The original Pulse Bar concept is a small handheld electronic device based on the supplied purple reference image.

- Rounded rectangular body with distinctive curved edges.
- Short rounded mouthpiece/extension on top.
- Raised glossy black vertical display on the front.
- Thick shiny silver/chrome border around the display.
- Smooth, polished plastic body.
- Compact enough for an R15 or R6 hand without covering the entire arm.
- Original target size: approximately **1.3 studs tall, 0.6 studs wide, and 0.4 studs thick**.
- Screen faces outward while held and faces the player during inspection.
- Required Tool part: `Handle`.
- Required hand alignment: `GripAttachment` or correctly configured Tool grip.
- All visible parts connected; decorative parts should not collide or add unwanted mass.

## Branding

- Do not use `GEEK BAR`, `GEEK CAR`, or other original product branding.
- Purple reference version should use only the word **Pulse** in clean white lettering.
- The earlier request for `Pulse Bar` can be used when a longer label is needed.
- The side illustration can include the small purple planet with thin yellow orbital rings.

## Screen design

The front display should include:

- Glossy black glass.
- Shiny silver border.
- Bright green curved indicators at the top and bottom.
- Purple segmented digital numbers.
- Small orange indicators around a dark center.
- Subtle glass reflections.
- A blocky Roblox-friendly style rather than excessive tiny geometry.

## Side constellation design

The `Fab pulse` includes a simple star/constellation design on both sides.

- Stars and connecting lines brighten and dim during use.
- Bright/dim cycle is synchronized on both sides.
- Animation continues briefly after the hit, then returns to the original brightness.
- Relevant SurfaceGui names: `SideConstellationFront` and `SideConstellationBack`.
- Relevant decorative object names: `Star` and `ConstellationLine`.

## Pulse Bar variants referenced in the project

- `blue razz blast pulse` — cyan/blue tint.
- `Miami Mint pulse` — mint tint.
- `dragon melo pulse` — orange/pink tint.
- `dragon melon pulse` — red tint.
- `Minneapolis Mint pulse` — dark body with cool gray/blue visual effects.
- `test test` — dark gray test version using the same Pulse systems.
- `Green pulse` — body currently reads as purple; effects follow the model color profile.
- `Meta moon pulse` — lime/light green profile.
- `Fab pulse` — green/teal body and animated constellation artwork.
- Earlier model: `mint pulse black silver` — black/silver version with the same screen style.

## Model quality preferences

- Favor a smaller number of cleanly aligned pieces.
- Use smooth geometry and consistent corner radii.
- Avoid a generic phone or plain box silhouette.
- Keep chrome borders even on all sides.
- Avoid details that float away from the body.
- Use `SmoothPlastic`, `Glass`, `Metal`, and limited `Neon` appropriately.
- Decorative objects should normally have `CanCollide = false` and be massless or welded.

