# New Games Research Synthesis

Updated: 2026-11-07. Purpose: turn the expanded Roblox vault into decisions we can reuse when starting a **new** game. This is a selective synthesis of the most relevant hubs and source notes, not a claim that every one of the vault's 1,658 Markdown files has been read in full. The vault spans 62 numbered sections; its [[00 Start Here]] and [[ROUTER]] explain where to go for a particular system. Treat timings and budgets below as starting hypotheses, then measure the actual game.

## The central finding

Start with a playable verb, a first reward, and one complete loop. A long feature list is not a game. [[Core Loops and Session Design]] says to write the loop in one sentence using actions the player actually performs; [[Planning and Scoping a Roblox Game]] adds a countable content unit and a performance budget before making large quantities of art. The first production target is one polished vertical slice, not a giant empty map.

**Reusable sequence:**

1. State the genre and the player fantasy in one sentence.
2. Prototype the primary action without rewards. Check input feel on keyboard, touch, and gamepad.
3. Add one immediate reward, one meaningful way to spend it, and a visible change to the action.
4. Script the first five minutes for that genre. Test with someone who has never seen the project.
5. Build one finished content unit with final art, sound, UI, save flow, and multiplayer behavior.
6. Measure join time, the first action, first reward, first spend, first session end, and device performance.
7. Only then multiply the content unit or add another system.

Sources: [[Core Loops and Session Design]], [[Planning and Scoping a Roblox Game]], [[First-Time User Experience and Onboarding]], [[Onboarding by Genre - The First Five Minutes]], [[Roadmaps Milestones and Scope Control]].

## Genre decisions must stay separate

The vault's case studies offer mechanisms, not a single recipe. [[Top Games Case Studies Start Here]] explicitly warns that public snapshots do not reveal other games' retention, revenue, or click-through rate. Use the cases to form experiments for our games, not to claim a guaranteed formula.

| If the new game is… | First playable slice | First-five-minute risk | Useful source path |
|---|---|---|---|
| Social town / roleplay | Spawn, take a prop or vehicle, claim or enter a home, meet someone | A compulsory tutorial or empty travel between scenes | [[Genre Playbook - Roleplay and Social Hangouts]], [[Case Study - Brookhaven RP]], [[Social Design and Multiplayer Play]] |
| Simulator / collection | Do the verb, collect, sell or convert, buy a visible upgrade, repeat | Currency rises but the action never changes; prices outrun income | [[Genre Playbook - Simulators]], [[Case Study - Fisch]], [[Progression and Pacing Design]] |
| Short replayable challenge | Enter a run, learn one rule, face a fair risk, finish or retry | Unfair first loss or no readable counterplay | [[Case Study - Doors]], [[Genre Playbook - Horror and Story]], [[Viral Game Anatomy - Hooks, Loops and Timing]] |
| Tycoon | Claim plot, receive a free first machine, see output, buy one upgrade | Empty plot and too many unaffordable buttons | [[Genre Playbook - Tycoons]], [[Tycoon Plots and Droppers End to End]] |
| Obby / skill game | Move and jump immediately, reach first checkpoint, introduce one mechanic | A hard failure before the player understands the jump | [[Onboarding by Genre - The First Five Minutes]], [[Teaching Through Level Design]] |

For a social town, optional lightweight goals such as the Place1 Town Explorer trail can guide new players, but houses, vehicles, props, and people should be available from the start. A progression game's XP and credits need a sink that changes play. A challenge game needs clear rules, a readable failure, and a fast retry. These are distinct designs.

## First-session specification

Write a five-row script for every project before building its tutorial: 0–10 seconds (control), 10–30 seconds (first verb), 30–60 seconds (first reward), 1–3 minutes (first loop closure), and 3–5 minutes (first meaningful choice). The timings in [[First-Time User Experience and Onboarding]] and [[Onboarding by Genre - The First Five Minutes]] are **rules of thumb**, not engine limits. Social games may skip explicit instruction entirely; horror can spend the early moments on atmosphere but must make the first threat fair.

At each step record: player action, on-screen cue, server event, reward, likely failure, and the measured percentage of players reaching it. A pop-up should not obscure the first action. [[Analytics and Funnels]] recommends server-side, low-cardinality events and a join-to-ten-minute funnel. Test with a new player, not only the builder.

## Engineering foundation before persistence or sales

- Separate client presentation from server decisions. The server owns inventory, currency, damage, prompts that grant rewards, and purchase outcomes. Validate types **and values**, ownership, location, distance, and rate. Sources: [[Server Authority and Validation]], [[Remote Abuse Patterns and Rate Limiting in Practice]].
- Use a predictable bootstrap and clear module boundaries. [[Project Structure and Bootstrapping]] recommends one server entry and one client entry with modules, handling players who already exist when a system starts.
- Give one data layer authority over player saves. A failed load must never become a new empty profile that later overwrites good data. Save cadence, migrations, session ownership, and recovery should be designed before valuable inventory is granted. Sources: [[Saved Inventory End to End]], [[Data Loss Prevention and Recovery]], [[Session Locking and Profile Libraries]].
- Keep a real pre-change backup, project map, short changelog, and revert path. A Studio edit check is not a playtest. Sources: [[Documentation and Knowledge Bases]], [[Safety Rules for AI Agents in Studio]], [[QA Checklists Before Release]].

## Economy and progression

Choose a currency only when it has a distinct job, source, and sink. Two currencies with the same loop should be merged. Model the time a player needs to afford each meaningful purchase from their expected income; plot the **whole** ladder, including late game, rather than tuning just the first prices. Sources: [[Currency Architecture - Soft Hard and Event Currencies]], [[Economy Inflation Sinks and Faucets Math]], [[Progression and Pacing Design]].

For a new economy, simulate several player types and session lengths before launch, but use simulation for comparisons rather than predictions. For a town job system, pay for server-observed activity instead of idle time. Any permanent currency, inventory, or premium purchase requires idempotent server handling and save tests. Sources: [[Simulating an Economy Before Launch]], [[Weekend Build - Roleplay Town with Jobs and Paychecks]], [[Purchase Data and Receipts]].

## World and art direction

One district needs a readable path, a skyline landmark, and a reason to enter. [[Level Design Principles - Flow Sightlines and Landmarks]] says players see light, motion, silhouette, and openings before they read signs. Use paths and landmark silhouettes to guide the first route; make optional discoveries branch from it and rejoin. For a town, favor a small number of dense story locations over a huge field of façades.

Choose grid size, pivot rules, wall height, and door size before building a modular kit. Keep contact faces flat and hide seams with trim. Define an art budget per content unit, then audit materials, draw calls, lights, particles, and memory. A copyable model is valuable only if it looks correct at player scale and on a low-end device. Sources: [[Modular Environment Kits]], [[Art Budgets - Triangles Draw Calls Memory]], [[Performance Fundamentals]], [[Mobile and Low-End Optimization]].

## UI, accessibility, and game feel

- Design by viewport and input capability rather than assuming `TouchEnabled` means a phone. Test small phones, tablets, desktop, console, and notched displays. [[Responsive UI for Phone Tablet Console and PC]] gives 12 px text, 44 px tap, and 8 px spacing as test targets, not universal engine requirements.
- Encode important states in text, shape, or icon as well as color. Make the first action and reward readable with sound off. Respect text size, transparency, and motion preferences. Sources: [[Accessibility]], [[Colour-Blind Safe Design]], [[Motion Sensitivity and Camera Comfort]].
- Every input should respond quickly, with feedback tied to the actual action or hit. Rewards benefit from motion and a clear payoff. Keep one owner for FOV and camera effects; provide a reduced-motion option. Sources: [[Game Feel and Juice]], [[Anticipation]], [[Motion Sensitivity and Camera Comfort]].

## Release and growth

Before release, test at least one real low-end phone, multiple clients, join and rejoin, data failure, and the core loop end to end. Record frame time rather than only FPS, memory, join seconds, and the worst stalls. Studio play mode is useful for correctness but cannot prove device performance. Sources: [[Performance Fundamentals]], [[Mobile and Low-End Optimization]], [[QA Checklists Before Release]].

Use honest store-page art that matches the game and reads at small size. Other games' public pages can inspire an icon or title experiment, but do not infer their private conversion metrics. For monetization, show what is bought and avoid fake scarcity or hidden odds. Sources: [[Cross-Game Patterns - Thumbnails Icons and Titles That Get Clicks]], [[Ethical Design and Player Trust]], [[Top Games Case Studies Start Here]]. Recheck changing Roblox policies and APIs against official documentation at the time of publication; the vault labels many platform facts as checked in October 2026.

## Three promising directions for our next game

These are proposals derived from the notes, not features approved for implementation.

1. **Neighborhood Stories:** a compact social town with immediate house/vehicle access, short optional neighborhood errands, and staged community events. First slice: one block, two homes, one shop, three props, one shared event. Keep jobs optional. Use [[Genre Playbook - Roleplay and Social Hangouts]] and the Place1 map lessons as starting points.
2. **Market Makers:** build and run a small stall, serve NPC and player requests, visibly improve displays, and join a short market event. First slice: one stall, three item types, one customer pattern, one upgrade. Use [[Core Loops and Session Design]], [[Weekend Build - Roleplay Town with Jobs and Paychecks]], and [[Economy Inflation Sinks and Faucets Math]].
3. **Signal Run:** a short cooperative exploration challenge around readable landmarks and timed signals. First slice: one 3–5 minute route with one fair hazard, one checkpoint, and a fast retry. Use [[Case Study - Doors]], [[Teaching Through Level Design]], and [[Level Design Principles - Flow Sightlines and Landmarks]].

**Recommended next decision:** choose the primary fantasy and target genre for one project, then fill [[25 - New Roblox Game Brief Template]] and build a single vertical slice. Avoid combining all three proposals into one experience.

## Research status and limits

This pass inventoried the 62-section vault and read the routing notes, relevant section hubs, source summaries, and detailed planning, core-loop, and onboarding sections. It deliberately does not treat all 1,658 Markdown files as equally relevant to every game. Specific code examples in worked builds are often labelled reviewed but not run; they must be integrated and tested in the destination project. Public game teardowns are dated snapshots, and their explanations of success are hypotheses. Current platform policies, prices, and API behavior require a fresh official check before shipping a feature that depends on them.
