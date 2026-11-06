# Roblox Game Development Playbook

Research date: 2026-11-05. This is a reference and build plan for The Burg. Code below is illustrative Luau for a test place.

## 1. Design the first ten minutes

The Burg's pitch: a suburban roleplay game where you can take short local jobs, explore the neighborhood and make progress even if you join alone. Give new players a visible first action, show the controls as they need them, and let them earn a meaningful first reward. Watch a fresh tester play without directions before expanding the map. [Roblox onboarding](https://create.roblox.com/docs/production/game-design/onboarding)

**First playable slice:** Spawn → accept a shift at The Vibe → read an address on the phone → find the numbered porch → hand over the order → see the payout → choose another delivery or spend cash on an approved cosmetic.

- Give the player a clear objective and a nearby landmark. Start with one address, then expand to three.
- Use a single job reward and price the first cosmetic in terms of how many deliveries it takes to earn. For example, a $25 delivery and a $75 poster give a three-delivery target. Treat both as playtest values.
- Give players an easy way to cancel, retry or ask for directions. Add route variety after players can finish the basic route.
- Separate Money for purchases from XP for milestones. Keep both server-owned and show the reason for every change.

## 2. Code and game structure

| Studio location | What belongs there |
| --- | --- |
| ServerScriptService | Job state, wallet transactions, NPC interactions, save logic |
| ServerStorage | Tool and prop templates that the server clones |
| ReplicatedStorage | Remotes and shared display data |
| StarterPlayerScripts / StarterGui | Phone, objective UI, input, animation and local feedback |
| Workspace | Map models, pickup counters and tagged or named interaction points |

Use a Script for server logic, LocalScript for player-facing behavior and ModuleScript for reusable logic. Learn tables, functions, events and instance hierarchy by building one prompt and reading Studio Output. [Luau starter lesson](https://create.roblox.com/docs/tutorials/fundamentals/coding-1/create-a-script) · [Remote events and callbacks](https://create.roblox.com/docs/scripting/events/remote)

The client requests an action. The server verifies player state, distance, action ID, ownership and cooldown, then calculates the result. Prices and rewards come from server logic. Check prompts on the server too. For a purchase, check the balance, deduct funds and grant ownership as one non-yielding operation after validation. Handle retries without granting a second reward. [Client-server security](https://create.roblox.com/docs/scripting/security/client-server-boundary)

### Luau example — one delivery with a server-side payout

In a test place, add anchored Parts named `DeliveryPickup` and `DeliveryPorch` directly under Workspace. Give each a ProximityPrompt. Set its activation distance to 10 studs. Put this Script in ServerScriptService. It expects the existing server-created `leaderstats.Money` IntValue. The player's `DeliveryAddress` attribute can drive the phone UI. Test the counter and porch on foot.

```luau
local Players = game:GetService("Players")
local pickup = workspace:WaitForChild("DeliveryPickup")
local porch = workspace:WaitForChild("DeliveryPorch")
local activeOrders = {}
local reward = 25

local function isNearby(player, point)
    local character = player.Character
    local root = character and character:FindFirstChild("HumanoidRootPart")
    local humanoid = character and character:FindFirstChildOfClass("Humanoid")
    return root and humanoid and humanoid.Health > 0
        and (root.Position - point.Position).Magnitude <= 10
end

pickup:WaitForChild("ProximityPrompt").Triggered:Connect(function(player)
    if activeOrders[player] or not isNearby(player, pickup) then
        return
    end
    activeOrders[player] = true
    player:SetAttribute("DeliveryAddress", "12 Oak Street")
end)

porch:WaitForChild("ProximityPrompt").Triggered:Connect(function(player)
    if not activeOrders[player] or not isNearby(player, porch) then
        return
    end

    local stats = player:FindFirstChild("leaderstats")
    local money = stats and stats:FindFirstChild("Money")
    if not money or not money:IsA("IntValue") then
        return
    end

    activeOrders[player] = nil
    money.Value += reward
    player:SetAttribute("DeliveryAddress", nil)
end)

Players.PlayerRemoving:Connect(function(player)
    activeOrders[player] = nil
end)
```

For three porches, store a destination ID per order and compare it with the porch that fired. Add explicit payout feedback and decide what happens on death, cancellation and reconnect. A LocalScript can subscribe to `GetAttributeChangedSignal("DeliveryAddress")` and read its initial value when mounting. Server validation remains the same if the UI changes.

### Saving and economy

- Use the existing Story slot system. Keep a schema version and stable item IDs, and explicitly migrate older slots.
- Call DataStore from server code and wrap network calls in `pcall`. Use `UpdateAsync` with a non-yielding transform and a revision or session check. If loading fails, preserve the previous save and show a retry state.
- Save cash and durable ownership in the same player snapshot. Keep temporary delivery state in memory for the first build. Test new saves, older saves, rejoin, failed writes and competing sessions in an isolated test experience. Roblox Studio can otherwise access production stores when API access is enabled. [Roblox Data Stores](https://create.roblox.com/docs/cloud-services/data-stores)

## 3. Models, level art and sound

1. **Block out the route in Studio.** Use your existing modular roads. Mark the counter, crosswalk, street signs and three porches before detailing. Walk the route in R6 and check stairs, door widths and the street-facing side of each house.
2. **Build a reusable kit.** Start with a house number plate, porch, sidewalk section, takeout bag, counter sign and shop shelf. Give reusable pieces consistent dimensions, pivots, colors and naming. Group buildings by shell, roof, openings, trim, collisions and interactions.
3. **Choose a modeling workflow.** Use Studio Parts for structural shapes and gameplay collision. For a unique prop, model it in Blender, apply transforms, set its origin, export it and inspect scale, orientation, materials and collisions in Studio's Importer. The Importer supports formats including FBX, glTF and OBJ. [Models](https://create.roblox.com/docs/parts/models) · [3D Importer](https://create.roblox.com/docs/studio/importer)
4. **Review external assets.** Record the source and rights for meshes, textures, audio and animations. Inspect unfamiliar models in a scratch place and review embedded scripts before use. Check that the published experience has access to restricted assets. [Roblox assets](https://create.roblox.com/docs/assets)
5. **Polish with a few readable details.** Use clear shop signage, a consistent window style, local counter sounds and short delivery feedback. Keep sound levels balanced and provide a way to reduce loud effects.
6. **Profile a representative block.** Reuse materials and meshes, use simple collision on walkable geometry, and limit decorative particles and shadow-casting lights where they hurt measured performance. Evaluate instance streaming as the map grows and test interactions when distant map parts are absent from the client. [Performance guide](https://create.roblox.com/docs/performance-optimization/improve)

### Model acceptance checklist

- [ ] Correct scale, front direction and pivot.
- [ ] No unintended holes, floating trim, flickering overlapping surfaces or blocked walkways.
- [ ] Collision works at player scale. Decorative collision is off where it would snag the avatar.
- [ ] Meaningful names, grouped pieces and asset source recorded.
- [ ] The prop reads clearly at normal camera distance and on a phone.

## 4. UI, controls and accessibility

- Show one immediate objective, one clear confirmation and a specific error message when something fails. Keep the cash reward and destination readable at small screen sizes.
- Use `GuiButton.Activated` for buttons and test interactions with keyboard/mouse, touch and gamepad. Keep interaction labels visible and avoid making color the sole indicator. [Roblox input guide](https://create.roblox.com/docs/input)
- Test the known cursor issue by opening each menu, using any search field, closing it and turning with a physical mouse in first person. Repeat in third person and with nested menus. Check camera ownership and text focus on every exit path.
- Make heavy blur, shake and flashing optional. Check UI placement with the device simulator and confirm touch targets on actual hardware.

## 5. QA, release and iteration

| Check | Passing result |
| --- | --- |
| Fresh player | Can find the job, read the address and finish without help |
| Two clients | Each gets their own order and reward; another player cannot claim it |
| Abuse cases | Wrong porch, spam, distant interaction and repeated delivery do not award extra cash |
| Save cases | Older saves load, valid updates survive rejoin, failed reads do not overwrite existing data |
| Devices | Mouse look returns after closing menus; touch and controller prompts work |
| Art and performance | Route is walkable and readable on a lower-end device |

Use Studio's client and server views for script debugging, a multi-client playtest for replication and a real device for input and performance checks. Publish a limited test build before public release. [Studio testing modes](https://create.roblox.com/docs/studio/testing-modes) · [Publishing and audience requirements](https://create.roblox.com/docs/production/publishing/publish-games-and-places)

**Release check for The Burg.** Roblox's standards prohibit depicting or promoting vaping and associated paraphernalia. Review the current vape-inspired models, simulated inhaling, smoke and store listings before publishing. A project-specific redesign is a walkie-talkie, camera or delivery scanner with its own original silhouette and hand interaction. Review the content maturity questionnaire for the actual build and the rules that apply to its intended audience. [Roblox Community Standards](https://about.roblox.com/community-standards) · [Content maturity and compliance](https://create.roblox.com/docs/production/promotion/content-maturity)

After testers start joining, measure a short funnel: joined → accepted shift → reached porch → earned first payout → started second activity. If many players accept but never arrive, watch their route and test clearer signs or a better phone message. Use retention and session trends to decide what to improve. Use screenshots and descriptions that show the actual game. [Funnel events](https://create.roblox.com/docs/production/analytics/funnel-events) · [Retention](https://create.roblox.com/docs/production/analytics/retention) · [Discovery](https://create.roblox.com/docs/discovery)

## 6. Watch and practice

- [Intro to World Building on Roblox](https://www.youtube.com/watch?v=SgPU84AqpkY) — Roblox Creator Hub's linked world-building livestream. Practice by blocking out one street and making the destination visible from the sidewalk.
- [Roblox Studio Basics — Beginners Scripting Tutorial](https://www.youtube.com/watch?v=9MUgLaF22Yo) — supplementary video for getting oriented. Follow it by making your own server Script and checking its messages in Output. Use Creator Hub for API details.
- [Roblox Creator Hub tutorials](https://create.roblox.com/docs/tutorials) — guided building and gameplay projects. Try the first-game project in a separate place and adapt the reward feedback to The Burg.

## Build order for The Burg

- [ ] First milestone: one delivery, one porch, one phone objective and a payout.
- [ ] Add two addresses, better signage and cancel/retry behavior.
- [ ] Add a simple spending target and test Story save/reload.
- [ ] Fix first-person menu handoff, run two-client and phone tests, then invite a few testers.
- [ ] Expand into the gym challenge or neighborhood errands once the first route feels good.

Related notes: [[19 - The Burg Game Ideas]], [[10 - Roblox Script Architecture]], [[14 - Live Buildings Roads and Locations Audit]], [[18 - Roblox Development Reflection Log]].
