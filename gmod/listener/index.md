# listener
Global signal system for multi-purpose callbacks.

---

[!ref Signal](/libraries/signal/#library-functions)

## Aimbot & triggerbot

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### should_aimbot_target(entIndex: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
should_aimbot_target(entIndex: number): boolean
</code>

- Determines if the player should be targeted by the aimbot or not.
- Also applies to legit bot.

```lua
secret.listener.add("should_aimbot_target", "notarget", function(index)
    return true -- blocks
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### should_triggerbot_target(entIndex: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
should_triggerbot_target(entIndex: number): boolean
</code>

- Determines if the player should be targeted by the triggerbot.

```lua
secret.listener.add("should_triggerbot_target", "notrigger", function(index)
    return true -- blocks
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### override_vischeck(aimbot_target_index: number, tstart: vector, tend: vector, record: boolean): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
override_vischeck(aimbot_target_index: number, tstart: vector, tend: vector, record: boolean): boolean
</code>

- Called every time the cheat performs a visibility check between you and a potential aimbot target.
- Currently only **ragebot** uses this listener.  
- **tstart** – starting position of the trace (usually your eye position).  
- **tend** – ending position of the trace (usually the target hitbox).  
- **record** - is the trace running at a backtrack record?
- **Return value**:
  - `true`  → force the vischeck to succeed (target is always considered visible).  
  - `false` → force the vischeck to fail (target is never considered visible).  
  - `nil`   → do nothing and let the default engine visibility check decide.

```lua
-- simple override, treat everyone as visible.
secret.listener.add("override_vischeck", "always_visible", function(target_index, tstart, tend, record)
    return true
end)

-- custom logic, allow vis if distance < 500 units
secret.listener.add("override_vischeck", "short_range_vis", function(target_index, tstart, tend, record)
    local dist = (tend - tstart):Length()
    if dist < 500 then
        return true
    end
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### should_aimbot_autofire(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
should_aimbot_autofire(): boolean
</code>

- Called every time the ragebot decides whether it should autofire.
- Useful for custom logic to control when the ragebot fires (e.g., based on target state, weapon, or other conditions).

```lua
secret.listener.add("should_aimbot_autofire", "custom_logic", function()
    -- only allow autofire if some condition is met
    return LocalPlayer():Health() > 50
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### override_aimbot_angle(target_ent_index: number, original_angle: Angle, target_angle: Angle): boolean,(Angle)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
override_aimbot_angle(target_ent_index: number, original_angle: Angle, target_angle: Angle): boolean,(Angle)
</code>

- Lets you override the final aim angle before the aimbot uses it.
- return **true, new_angle** to apply your override.
- return **false** to use the default angle.

```lua
secret.listener.add("override_aimbot_angle", "67", function(target_ent_index, original_angle, target_angle)
    local target = Entity(target_ent_index)

    -- override when target is low hp
    if target and target:Health() < 30 then
        local new_ang = Angle(67, 67, 0)
        return true, new_ang
    end

    return false
end)
```

---
## ESP

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### should_draw_player(entIndex: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
should_draw_player(entIndex: number): boolean
</code>

- Determines if the player should be drawn in the esp or not.

```lua
secret.listener.add("should_draw_player", "nodraw", function(index)
    return true -- blocks
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### should_draw_entity(entIndex: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
should_draw_entity(entIndex: number): boolean
</code>

- Determines if an entity should be drawn in the esp or not.

```lua
secret.listener.add("should_draw_entity", "nodraw", function(index)
    return true -- blocks
end)
```

### Player overrides

Global overrides run **before** the ESP-specific listeners below (`esp_player_name`, `esp_player_usergroup`, `esp_player_team_name`, `esp_player_team_color`). They affect the **playerlist** and the baseline values ESP builds from.

Use **override** listeners when you want one RP name, usergroup, or team everywhere (playerlist, staff detection, team filter labels, etc.). Use **esp_player_*** listeners when you only want a different display on ESP (for example a nickname on ESP while the playerlist keeps the real RP name).

The first registered callback that returns a non-`nil` value wins for each override event.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### override_player_rpname(entIndex: number): string {#override_player_rpname}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
override_player_rpname(entIndex: number): string
</code>

- Overrides the RP name of a player globally (playerlist, ESP baseline, staff checks, etc.).
- If a non-empty string is returned, that value is used as the player's RP name.
- Does **not** change the steam name shown when **display steam name** is enabled in the playerlist.
- [`esp_player_name`](#esp_player_name) can still override the name shown on ESP only.

```lua
secret.listener.add("override_player_rpname", "real_name", function(index)
    return "Maverick Trevillian"
end)

secret.listener.add("esp_player_name", "nickname", function(index)
    return "67 kid" -- playerlist shows Maverick Trevillian; ESP shows 67 kid
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### override_player_usergroup(entIndex: number): string {#override_player_usergroup}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
override_player_usergroup(entIndex: number): string
</code>

- Overrides the usergroup of a player globally (playerlist, ESP baseline, staff highlight, etc.).
- If a non-empty string is returned, that value is used as the player's usergroup.
- [`esp_player_usergroup`](#esp_player_usergroup) can still override the usergroup shown on ESP only.

```lua
secret.listener.add("override_player_usergroup", "real_usergroup", function(index)
    return "admin"
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### override_player_team(entIndex: number, teamIndex: number): table {#override_player_team}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
override_player_team(entIndex: number, teamIndex: number): table
</code>

- Overrides team information for a **specific player** globally (playerlist, ESP baseline, team filter labels, etc.).
- Return a table to apply the override. All fields are optional; omitted fields keep the current value.

| Field | Type | Description |
|-------|------|-------------|
| `index` | number | Team index shown in the playerlist (e.g. `1`) |
| `name` | string | Team name |
| `color` | table | `{ r, g, b, a? }` team color (0–255) |

- [`esp_player_team_name`](#esp_player_team_name) and [`esp_player_team_color`](#esp_player_team_color) can still override team display on ESP only.

```lua
secret.listener.add("override_player_team", "real_team", function(ent_index, team_index)
    return {
        index = 1,
        name  = "Sigma Squad",
        color = { r = 255, g = 175, b = 50 }
    }
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### esp_player_name(entIndex: number): string {#esp_player_name}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
esp_player_name(entIndex: number): string
</code>

- Overrides the name shown for a player **on ESP only**.
- Runs after [`override_player_rpname`](#override_player_rpname) (if registered).
- If a non-empty string is returned, the ESP will display that value instead of the global RP name.
- Returning `nil` or a non-string will cause the default name to be used.

```lua
secret.listener.add("esp_player_name", "custom_name", function(index)
    return "67 kid" -- esp only; playerlist still uses override_player_rpname / game RP name
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### esp_player_usergroup(entIndex: number): string {#esp_player_usergroup}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
esp_player_usergroup(entIndex: number): string
</code>

- Overrides the usergroup shown for a player **on ESP only**.
- Runs after [`override_player_usergroup`](#override_player_usergroup) (if registered).
- If a non-empty string is returned, the ESP will display that value instead of the global usergroup.
- Returning `nil` or a non-string will cause the default usergroup to be used.

```lua
secret.listener.add("esp_player_usergroup", "custom_usergroup", function(index)
    return "admin"
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### esp_player_team_name(entIndex: number): string {#esp_player_team_name}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
esp_player_team_name(entIndex: number): string
</code>

- Overrides the team name shown for a player **on ESP only**.
- Runs after [`override_player_team`](#override_player_team) (if registered).
- If a non-empty string is returned, the ESP will display that value instead of the global team name.
- Returning `nil` or a non-string will cause the default team name to be used.

```lua
secret.listener.add("esp_player_team_name", "custom_team", function(index)
    return "sigma squad"
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### esp_player_team_color(entIndex: number): table {#esp_player_team_color}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
esp_player_team_color(entIndex: number): table
</code>

- Overrides the team color used for a player **on ESP only** (team text, team-based box color, etc.).
- Runs after [`override_player_team`](#override_player_team) (if registered).
- Return a table with `r`, `g`, `b`, and optionally `a` (0–255).

```lua
secret.listener.add("esp_player_team_color", "pink_team", function(index)
    return { r = 255, g = 50, b = 200 }
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### esp_player_name_color(entIndex: number): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
esp_player_name_color(entIndex: number): table
</code>

- Override the color used for a player’s name in ESP. Return a table `{ r, g, b, a }` (0–255). Return nothing or a non-table to keep the default (priority/friend/dormant/config) color.

```lua
secret.listener.add("esp_player_name_color", "my_script", function(ent_index)
    return { r = 255, g = 100, b = 100, a = 255 }
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### esp_player_usergroup_color(entIndex: number): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
esp_player_usergroup_color(entIndex: number): table
</code>

- Override the color used for a player’s usergroup text in ESP. Return a table `{ r, g, b, a }` (0–255). Return nothing or a non-table to keep the default color.

```lua
secret.listener.add("esp_player_usergroup_color", "my_script", function(ent_index)
    return { r = 200, g = 200, b = 255, a = 255 }
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### draw_player_esp(ctx: table): draw_item | draw_item[] {#draw_player_esp}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
draw_player_esp(ctx: table): draw_item | draw_item[]
</code>

- Used for drawing custom elements on player ESP.
- Context fields such as `name`, `usergroup`, and `team` reflect **ESP display values** (after global overrides and ESP-specific listeners).

**Context (`ctx`) fields:**

| Field | Type | Description |
|-------|------|-------------|
| `index` | number | Player entity index |
| `name` | string | Player name |
| `usergroup` | string | Usergroup |
| `team` | string | Team name |
| `weapon` | string | Active weapon name |
| `hp` | number | Current health |
| `hp_max` | number | Max health |
| `armor` | number | Current armor |
| `armor_max` | number | Max armor |
| `distance` | number | Distance from local player |
| `simulation` | number | Simulation time |
| `alive` | boolean | Is alive |
| `dormant` | boolean | Is dormant |
| `visible` | boolean | Is visible to local player |
| `friend` | boolean | Marked as friend |
| `priority` | boolean | Marked as priority |
| `team_color` | table | `{ r, g, b, a }` team color |
| `bounds` | table | Screen bounding box `{ x, y, w, h }` |

**Draw item fields:**

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `text` | string | — | Text to draw (**required**) |
| `color` | table | white | `{ r, g, b, a }` or `{ 255, 80, 80, 255 }` |
| `position` | string \| number | `"bottom"` | `"top"`, `"bottom"`, `"right"`, `"left"` or `0`–`3` |
| `outline` | boolean | `true` | Draw text outline |
| `side_font` | boolean | `false` | Use the narrow side ESP font |
| `x` | number | — | Absolute screen X (overrides `position`) |
| `y` | number | — | Absolute screen Y (overrides `position`) |

- **Position values:** `0` / `"top"`, `1` / `"bottom"`, `2` / `"right"`, `3` / `"left"`.
- Friend, priority, and dormant targets may override your `color` the same way built-in ESP does.

```lua
secret.listener.add("draw_player_esp", "my_player_esp", function(ctx)
    return {
        text = "custom tag",
        color = { 255, 80, 80, 255 },
        position = "top"
    }
end)

secret.listener.add("draw_player_esp", "multi_line", function(ctx)
    if ctx.dormant then return end

    return {
        { text = ctx.name, position = "top", color = { r = 255, g = 255, b = 255 } },
        { text = ctx.weapon, position = "bottom", side_font = true },
    }
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### draw_entity_esp(ctx: table): draw_item | draw_item[] {#draw_entity_esp}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
draw_entity_esp(ctx: table): draw_item | draw_item[]
</code>

- Used for drawing custom elements on entity ESP
- Scripted entities only.

**Context (`ctx`) fields:**

| Field | Type | Description |
|-------|------|-------------|
| `index` | number | Entity index |
| `name` | string | Entity / class name |
| `distance` | number | Distance from local player |
| `dormant` | boolean | Is dormant |
| `scripted` | boolean | Is a scripted entity |
| `has_owner` | boolean | Has an owner entity |
| `team_color` | table | `{ r, g, b, a }` team color |
| `bounds` | table | Screen bounding box `{ x, y, w, h }` |

```lua
secret.listener.add("draw_entity_esp", "ent_tags", function(ctx)
    if not ctx.scripted then return end

    return {
        text = ctx.name,
        color = { r = 200, g = 255, b = 200, a = 255 },
        position = "right"
    }
end)
```

---
## Game loop

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### think()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
think()
</code>

- Called every frame.

```lua
secret.listener.add("think", "spam_console", function()
    print("spammmm!")
end)
```

---
## Rendering

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint_traverse()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint_traverse()
</code>

- Mostly used for custom drawing.
- This is a 2D render context.

```lua
secret.listener.add("paint_traverse", "draw_box", function()
    surface.SetDrawColor(255,255,255,255)
    surface.DrawRect(25, 25, 100, 100)
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### view_render_post()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
view_render_post()
</code>

- Occurs after ViewRender has been ran, usually used for screengrab proof esp.
- This is a 3D render context.

```lua
secret.listener.add("view_render_post", "draw_2d_box", function()
    cam.Start2D()
    surface.SetDrawColor(255,255,255,255)
    surface.DrawRect(25, 25, 100, 100)
    cam.End2D()
end)
```

---
## Network

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### server_connect(ip: string, port: number, hostname: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
server_connect(ip: string, port: number, hostname: string)
</code>

- Called when connecting to a server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### server_disconnect(reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
server_disconnect(reason: string)
</code>

- Called when disconnected/kicked/banned from a server.

---
## Input & usercmd

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### presend(CUserCmd: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
presend(CUserCmd: table)
</code>

- Called right before movement packets are sent.
- Provides full access to the native Garry's Mod `CUserCmd` class.
- Provides additional functions not found in the default GMod class, allowing extended control over the usercmd.

```lua
secret.listener.add("presend", "viewangles", function(cmd)
    cmd.angles = Angle(50, 50, 0) -- sets our viewangles
    cmd.SetWorldClicker(cmd, Vector(20, 20, 20)) -- sets our context menu angle, not present in the garry's mod class.
end)
```

**CUserCmd** — properties available on the `cmd` table:

| Property | Access | Type |
|----------|--------|------|
| `buttons` | get/set | number |
| `command` | get/set | number |
| `tick` | get/set | number |
| `angles` | get/set | Angle |
| `forward` | get/set | number |
| `side` | get/set | number |
| `up` | get/set | number |
| `impulse` | get/set | number |
| `seed` | get/set | number |
| `hash` | get | number |
| `mousex` | get/set | number |
| `mousey` | get/set | number |
| `prediction` | get | bool |

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### wndproc(vk_key: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
wndproc(vk_key: number): boolean
</code>

- Called whenever a Windows virtual key event is received.
- If `true` is returned, the input will be blocked from reaching the game.

```lua
secret.listener.add("wndproc", "block_space", function(vk)
    if vk == 0x20 then -- space key
        return true -- block input
    end
end)
```
<div hidden>

```ts

```

</div>
