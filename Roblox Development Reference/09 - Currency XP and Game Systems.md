# Currency, XP, and Game Systems

## Pulse Credits concept

- Currency name: **Pulse Credits**.
- Player gains Credits by successfully using/left-clicking a Pulse Bar.
- Credits are shown in a clear GUI.
- Award after a completed hit rather than immediately on a rejected click.
- Consider separate rewards for Normal and Ghost hits.
- Add server-side validation and cooldowns to prevent auto-click farming.

Possible balanced starting values:

- Normal completed hit: 1 Pulse Credit.
- Ghost completed hit: 2 Pulse Credits.
- Successful Blinker/minigame completion: larger bonus.
- Daily or streak bonuses can be added later.

## XP concept

- XP should represent player progression rather than spending money.
- Award XP for completed uses, minigame successes, exploration, quests, and interactions.
- Levels can unlock cosmetics, Pulse colors, smoke styles, animations, neighborhoods, or titles.
- Do not let constant clicking become the only meaningful progression method.

## Recommended server structure

- `leaderstats` can display Credits and Level during early development.
- Store durable values with DataStoreService on the server.
- Never trust a client-provided reward amount.
- Client reports the action; server verifies timing, tool ownership, cooldown, and result.
- Save Credits, XP, Level, unlocks, and settings.

## GUI ideas

- Small Pulse Credits counter near a screen corner.
- XP bar with level number.
- Brief `+1` or `+2` feedback after valid rewards.
- Low-profile styling consistent with the Pulse display colors.
- Avoid covering the hit-timing bar or inventory.

## Other outside-the-model ideas discussed

- Neighborhood exploration.
- Shops and unlockable variants.
- Quests and achievements.
- Collectibles.
- Map expansion using modular roads and filler homes.
- Interactive buildings and social locations.

