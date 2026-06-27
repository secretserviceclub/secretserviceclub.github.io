# automation
Allows control over the automation in lua.

**Quick reference:** Build events with `event_type.*`, add them with `add_event()` or `set_routine()`, then `start_routine()`. Use `automation.listener` for path_found, start_walking, stuck, path_finished.

---
## Routines and automation

The automation exposes a **routine** system: ordered lists of **events** (move, wait, input, Lua, etc.).

**Typical flow:** build a routine (e.g. Goto + Wait + RunCommand), optionally hook `automation.listener` to react to path_found / start_walking / stuck / path_finished, then call `start_routine()` to run the routine.

```lua
secret.automation.clear_routine()
secret.automation.add_event({ type = secret.automation.event_type.Goto, pos = { x = 1000, y = 2000, z = 100 }, goto_run = true, goto_destination_radius = 100 })
secret.automation.add_event({ type = secret.automation.event_type.Wait, wait_ms = 500 })
secret.automation.add_event({ type = secret.automation.event_type.RunCommand, command = "say arrived" })
secret.automation.start_routine()
```

Automation lifecycle is exposed via `automation.listener`, which uses the same API as the [!ref Signal](/libraries/signal/#library-functions) library: `add(name, identity, callback)` to register and `remove(name, identity)` to unregister. Use a string of your choice as `identity` (e.g. a script name) so you can remove the callback later.

```lua
secret.automation.listener.add("path_found", "my_hook", function()
    local waypoints = secret.automation.get_waypoints()
    print("Path has " .. #waypoints .. " waypoints")
end)
secret.automation.listener.add("path_finished", "my_hook", function()
    print("Reached destination")
    secret.automation.listener.remove("path_finished", "my_hook")
end)
```

```lua
secret.automation.clear_routine()
secret.automation.add_event({ type = secret.automation.event_type.Wait, wait_ms = 1000 })
secret.automation.add_event({ type = secret.automation.event_type.RunCommand, command = "say Done" })
secret.automation.start_routine()
```

### Event table shape

Each event in a routine is a table with optional fields. **Common fields:**

| Field | Type | Description |
|-------|------|-------------|
| `type` | number | Event type. Use `automation.event_type.Goto`, `automation.event_type.Wait`, etc. (see [Event types](#event-types-and-buttons) below). |
| `pos` | table | Position `{ x, y, z }`. |
| `angles` | table | Angles `{ p, y }`. |
| `button_mask` | number | Button mask for input. Use `automation.buttons.IN_ATTACK`, etc., or combine with bitwise OR (see [Buttons](#event-types-and-buttons)). |
| `hold_ms` | number | Hold duration in milliseconds. |
| `wait_ms` | number | Wait duration in milliseconds. |
| `wait_unit` | number | Wait unit selector (engine-defined). |
| `command` | string | Console/command string. |
| `lua_code` | string | Inline Lua code to run. |
| `lua_file` | string | Path to Lua file to run. |
| `run_in_menu` | boolean | Whether to run Lua while in menu. |
| `box_min` | table | Box min `{ x, y, z }`. |
| `box_max` | table | Box max `{ x, y, z }`. |
| `stuck_ms` | number | Stuck timeout in ms (default 2000). |
| `forward_move` | number | Forward move value. |
| `side_move` | number | Side move value. |
| `mouse_dx` | number | Mouse delta X. |
| `mouse_dy` | number | Mouse delta Y. |
| `cmd_overrides` | table | Per-event command overrides (see below). |
| `target_step_index` | number | Target step index for jumps (-1 = none). |
| `repeat_count` | number | Repeat count for the step. |
| `condition_radius` | number | Condition check radius (default 100). |
| `condition_value` | number | Condition value (default 50). |
| `look_lerp` | boolean | Whether to lerp look angles. |
| `look_lerp_ms` | number | Look lerp duration in ms (default 500). |
| `look_silent` | boolean | Silent look (no view change). |

**Conditional / goto / node fields:**

| Field | Type | Description |
|-------|------|-------------|
| `goto_look_at_waypoint` | boolean | Goto: look at waypoint. |
| `goto_look_at_waypoint_lerp_ms` | number | Goto look-at lerp ms (default 0). |
| `goto_run` | boolean | Goto: run instead of walk. |
| `goto_destination_radius` | number | Goto: consider arrived when within this distance of destination (default 0). |
| `goto_entity_repath_threshold` | number | GotoEntity: trigger repath when beyond this threshold (default 0). |
| `goto_entity_rescan_on_reach` | boolean | GotoEntity: rescan when reaching the destination. |
| `goto_entity_allow_dormant` | boolean | GotoEntity: allow dormant targets. |
| `parent_step_index` | number | Parent step index for hierarchy (-1 = none). |
| `node_pos_x` | number | Node position X. |
| `node_pos_y` | number | Node position Y. |
| `custom_node_radius` | number | Custom node radius (default 0). |
| `else_step_index` | number | Else-branch step index for conditionals (-1 = none). |
| `signal_name` | string | Signal name for `WaitForLuaSignal`; resume when `automation.signal(name)` is called. |
| `entity_classname` | string | Entity class name for entity-based events. |
| `target_entity_index` | number | Target entity index (-1 = none). |

**cmd_overrides** — Optional table that overrides player commands while the event runs:

| Field | Type | Description |
|-------|------|-------------|
| `apply_viewangles` | boolean | Apply custom view angles. |
| `viewangles` | table | View angles `{ p, y, r }`. |
| `apply_move` | boolean | Apply custom move vector. |
| `move` | table | Move vector `{ x, y, z }`. |
| `apply_buttons` | boolean | Apply button mask. |
| `buttons` | number | Button mask value. |
| `apply_impulse` | boolean | Apply impulse. |
| `impulse` | number | Impulse command. |
| `apply_weaponselect` | boolean | Apply weapon select. |
| `weaponselect` | number | Weapon slot. |
| `apply_weaponsubtype` | boolean | Apply weapon subtype. |
| `weaponsubtype` | number | Weapon subtype. |
| `apply_mouse` | boolean | Apply mouse delta. |
| `mousex` | number | Mouse X. |
| `mousey` | number | Mouse Y. |
| `apply_scroll_wheel` | boolean | Apply scroll wheel. |
| `scroll_wheel_speed` | number | Scroll speed. |
| `apply_world_clicking` | boolean | Apply world click state. |
| `world_clicking` | boolean | World clicking on/off. |
| `world_clicking_normal` | table | Normal `{ x, y, z }`. |
| `apply_is_typing` | boolean | Apply typing state. |
| `istyping` | boolean | Is typing. |
| `apply_is_forced` | boolean | Apply forced state. |
| `isforced` | boolean | Is forced. |

---
## Routine API

### Building routines

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_routine(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_routine(): table
</code>

- Current routine as 1-based array of event tables.

```lua
local events = secret.automation.get_routine()
for i, ev in ipairs(events) do
    print("Event " .. i .. " type=" .. tostring(ev.type) .. " wait_ms=" .. tostring(ev.wait_ms))
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.set_routine(events: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.set_routine(events: table)
</code>

- Replace the entire routine with the given array of event tables.

```lua
secret.automation.set_routine({
    { type = secret.automation.event_type.Wait, wait_ms = 1000 },
    { type = secret.automation.event_type.Goto, pos = { x = 100, y = 200, z = 300 }, hold_ms = 500, goto_destination_radius = 80 }
})
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.add_event(event: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.add_event(event: table)
</code>

- Append one event to the end of the routine.

```lua
secret.automation.add_event({
    type = secret.automation.event_type.RunCommand,
    command = "say Hello"
})
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.insert_event(index: number, event: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.insert_event(index: number, event: table)
</code>

- Insert an event at 1-based index (shifts others). Index 1 = start.

```lua
secret.automation.insert_event(1, { type = secret.automation.event_type.Wait, wait_ms = 500 })
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.remove_event(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.remove_event(index: number)
</code>

- Remove event at 1-based index. No-op if index &lt; 1.

```lua
secret.automation.remove_event(2)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.clear_routine()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.clear_routine()
</code>

- Clear all events.

```lua
secret.automation.clear_routine()
```

### Playback

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.start_routine()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.start_routine()
</code>

- Start the current routine.

```lua
secret.automation.start_routine()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.stop_routine()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.stop_routine()
</code>

- Stop the running routine.

```lua
if secret.automation.is_routine_running() then
    secret.automation.stop_routine()
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.is_routine_running(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.is_routine_running(): boolean
</code>

- True if a routine is running.

```lua
secret.automation.is_routine_running()
```

### Link-to-next

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_link_to_next(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_link_to_next(): table
</code>

- 1-based array of booleans: per-step link-to-next (flow between steps).

```lua
local links = secret.automation.get_link_to_next()
for i, linked in ipairs(links) do
    print("Step " .. i .. " linked to next: " .. tostring(linked))
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.set_link_to_next(links: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.set_link_to_next(links: table)
</code>

- Set link-to-next flags: table of booleans, one per step.

```lua
secret.automation.set_link_to_next({ true, true, false })
```

---
### Runtime state (during routine playback)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_waypoints(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_waypoints(): table
</code>

- Current routine waypoints: 1-based array of `{ x, y, z }`.

```lua
local waypoints = secret.automation.get_waypoints()
for i, wp in ipairs(waypoints) do
    print("Waypoint " .. i .. ": " .. wp.x .. ", " .. wp.y .. ", " .. wp.z)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_nodes(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_nodes(): table
</code>

- Current automation nodes: 1-based array of `{ x, y, z }`.

```lua
local nodes = secret.automation.get_nodes()
for i, n in ipairs(nodes) do
    print("Node " .. i .. ": " .. n.x .. ", " .. n.y .. ", " .. n.z)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_current_step_index(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_current_step_index(): number
</code>

- 1-based index of the step currently executing (0 when not running).

```lua
local step = secret.automation.get_current_step_index()
print("Current step: " .. step)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.jump_to_step(step_index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.jump_to_step(step_index: number)
</code>

- Jump to a step index in the routine (1-based). Use to skip or re-run steps during playback.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.signal(name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.signal(name: string)
</code>

- Fire a signal by name. Use with the `WaitForLuaSignal` event type: when the routine hits that event it waits until `automation.signal(name)` is called with the same name (empty string is valid).

```lua
secret.automation.signal("my_signal")
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_crosshair_trace_end(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_crosshair_trace_end(): table
</code>

- World position where crosshair trace hits: `{ x, y, z }`.

```lua
local hit = secret.automation.get_crosshair_trace_end()
print(hit.x, hit.y, hit.z)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_current_position(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_current_position(): table
</code>

- Current player position: `{ x, y, z }`.

```lua
local pos = secret.automation.get_current_position()
print(pos.x, pos.y, pos.z)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.get_current_view_angles(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.get_current_view_angles(): table
</code>

- Current view angles: `{ p, y }`.

```lua
local ang = secret.automation.get_current_view_angles()
print("Pitch: " .. ang.p .. " Yaw: " .. ang.y)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.start_pathfinder()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.start_pathfinder()
</code>

- Start pathfinding for the current destination (so `get_waypoints()` / `get_nodes()` update).

```lua
secret.automation.start_pathfinder()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.stop_pathfinder()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.stop_pathfinder()
</code>

- Stops the active pathfinding process.

```lua
if secret.automation.is_pathfinder_active() then
    secret.automation.stop_pathfinder()
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.is_pathfinder_active(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.is_pathfinder_active(): boolean
</code>

- True while pathfinding is active.

```lua
print("Active: " .. tostring(secret.automation.is_pathfinder_active()))
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.save_routine(name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.save_routine(name: string): boolean
</code>

- Saves the current routine to a file by name.

```lua
secret.automation.save_routine("my_routine")
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.load_routine(name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.load_routine(name: string): boolean
</code>

- Loads a routine from a saved file by name.

```lua
if secret.automation.load_routine("my_routine") then
    secret.automation.start_routine()
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.run_routine(name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.run_routine(name: string): boolean
</code>

- Load and start a routine by name.

```lua
secret.automation.run_routine("my_routine")
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.list_routines(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.list_routines(): table
</code>

- 1-based array of saved routine names.

```lua
local names = secret.automation.list_routines()
for i, name in ipairs(names) do
    print(i .. ": " .. name)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.list_lua_files(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.list_lua_files(): table
</code>

- 1-based array of Lua file names for ExecuteLua / `lua_file`.

```lua
local files = secret.automation.list_lua_files()
for i, name in ipairs(files) do
    print(i .. ": " .. name)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.export_routine(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.export_routine(): string
</code>

- Serialize current routine to a string.

```lua
local data = secret.automation.export_routine()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.import_routine(str: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
automation.import_routine(str: string): boolean
</code>

- Import a routine from a string (from `export_routine`).

```lua
local exported = secret.automation.export_routine()
if secret.automation.import_routine(exported) then
    secret.automation.start_routine()
end
```

---
## Event types and buttons

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.event_type

</div>

Table of event type IDs for the `type` field:

| Name | Value | Description |
|------|-------|-------------|
| `Goto` | 0 | Move to a position. |
| `LookAt` | 1 | Look at a position or angles. |
| `PressKey` | 2 | Press/release buttons (use `button_mask`, `hold_ms`). |
| `RunCommand` | 3 | Run a console command (`command`). |
| `Wait` | 4 | Wait for a duration (`wait_ms`). |
| `ExecuteLua` | 5 | Run Lua code or file (`lua_code`, `lua_file`, `run_in_menu`). |
| `WaitUntilInBox` | 6 | Wait until player is inside a box (`box_min`, `box_max`). |
| `WaitUntilStuck` | 7 | Wait until stuck for `stuck_ms`. |
| `SetMove` | 8 | Set move vector (`forward_move`, `side_move` or `cmd_overrides.move`). |
| `SetMouse` | 9 | Set mouse delta (`mouse_dx`, `mouse_dy` or `cmd_overrides`). |
| `SetCmd` | 10 | Set full command overrides (`cmd_overrides`). |
| `OnStuck` | 11 | Branch when stuck. |
| `Repeat` | 12 | Repeat a block (`repeat_count`, `target_step_index`). |
| `IfInBox` | 13 | Branch if in box. |
| `WhenPathFound` | 14 | Trigger when path is found. |
| `OnArrived` | 15 | Trigger when arrived at destination. |
| `WhenTimer` | 16 | Trigger after a timer. |
| `WhenNearPosition` | 17 | Trigger when near a position (`condition_radius`). |
| `WhenHealthBelow` | 18 | Trigger when health below value. |
| `WhenLookingAt` | 19 | Trigger when looking at target. |
| `WhenButtonHeld` | 20 | Trigger when button held. |
| `WhenHealthAbove` | 21 | Trigger when health above value. |
| `WhenOnGround` | 22 | Trigger when on ground. |
| `WhenInAir` | 23 | Trigger when in air. |
| `WhenVelocityBelow` | 24 | Trigger when velocity below value. |
| `WaitForLuaSignal` | 25 | Wait until `automation.signal(signal_name)` is called. |
| `Stop` | 26 | Stop the routine. |
| `IfEntityInBox` | 27 | Branch if entity in box. |
| `WhenNearEntity` | 28 | Trigger when near entity. |
| `GotoEntity` | 29 | Goto an entity. |

```lua
secret.automation.add_event({ type = secret.automation.event_type.Wait, wait_ms = 1000 })
secret.automation.add_event({ type = secret.automation.event_type.RunCommand, command = "say hi" })
secret.automation.add_event({ type = secret.automation.event_type.PressKey, button_mask = secret.automation.buttons.IN_ATTACK, hold_ms = 100 })
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### automation.buttons

</div>

Button mask constants for `PressKey`, `WhenButtonHeld`, and `button_mask`:

| Name | Description |
|------|-------------|
| `IN_ATTACK` | Attack. |
| `IN_JUMP` | Jump. |
| `IN_DUCK` | Duck / crouch. |
| `IN_FORWARD` | Move forward. |
| `IN_BACK` | Move back. |
| `IN_USE` | Use. |
| `IN_CANCEL` | Cancel. |
| `IN_LEFT` | Move left. |
| `IN_RIGHT` | Move right. |
| `IN_MOVELEFT` | Strafe left. |
| `IN_MOVERIGHT` | Strafe right. |
| `IN_ATTACK2` | Secondary attack. |
| `IN_RUN` | Run. |
| `IN_RELOAD` | Reload. |
| `IN_ALT1` | Alt1. |
| `IN_ALT2` | Alt2. |
| `IN_SCORE` | Score. |
| `IN_SPEED` | Speed. |
| `IN_WALK` | Walk. |
| `IN_ZOOM` | Zoom. |
| `IN_WEAPON1` | Weapon slot 1. |
| `IN_WEAPON2` | Weapon slot 2. |
| `IN_BULLRUSH` | Bullrush. |
| `IN_GRENADE1` | Grenade 1. |
| `IN_GRENADE2` | Grenade 2. |

```lua
secret.automation.add_event({
    type = secret.automation.event_type.PressKey,
    button_mask = secret.automation.buttons.IN_ATTACK,
    hold_ms = 200
})
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### Stuck reason constants

</div>

Reason IDs passed to the `stuck` event callback. Exposed on `automation` (e.g. `secret.automation.STUCK_COLLISION_BLOCKED`):

| Name | Value | Description |
|------|-------|-------------|
| `STUCK_COLLISION_BLOCKED` | 1 | Stuck due to collision. |
| `STUCK_NO_PROGRESS` | 2 | No progress made. |

```lua
secret.automation.listener.add("stuck", "my_script", function(reason_id)
    if reason_id == secret.automation.STUCK_NO_PROGRESS then
        secret.automation.stop_routine()
    end
end)
```

---
## Events

Automation fires signals during routine playback. `automation.listener` uses the [!ref Signal](/libraries/signal/#library-functions) API: register with `listener.add(name, identity, callback)` and unregister with `listener.remove(name, identity)`. The `identity` is a string you choose (e.g. script name) so you can remove the callback later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### path_found()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
path_found()
</code>

- Fired when a path to the current destination has been computed. Use `get_waypoints()` to read the path.

```lua
secret.automation.listener.add("path_found", "my_script", function()
    local waypoints = secret.automation.get_waypoints()
    for i, wp in ipairs(waypoints) do
        print(string.format("wp %d: %.0f %.0f %.0f", i, wp.x, wp.y, wp.z))
    end
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### start_walking()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
start_walking()
</code>

- Fired when movement along the path begins (after path_found). Use `get_current_step_index()` to track progress.

```lua
secret.automation.listener.add("start_walking", "my_script", function()
    local step = secret.automation.get_current_step_index()
    local pos = secret.automation.get_current_position()
    print("Walking from " .. pos.x .. " " .. pos.y .. " " .. pos.z .. " (step " .. step .. ")")
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### stuck()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
stuck(reason_id: number)
</code>

- Fired when the automation detects it can’t proceed (obstruction, no progress, etc.). The callback receives **reason_id**; use `automation.STUCK_COLLISION_BLOCKED` (1) and `automation.STUCK_NO_PROGRESS` (2) to branch. The engine may recalc the path; you can stop or adjust the routine here.

```lua
secret.automation.listener.add("stuck", "my_script", function(reason_id)
    local step = secret.automation.get_current_step_index()
    local pos = secret.automation.get_current_position()
    if reason_id == secret.automation.STUCK_COLLISION_BLOCKED then
        print("Stuck: collision blocked at step " .. step)
    elseif reason_id == secret.automation.STUCK_NO_PROGRESS then
        print("Stuck: no progress at step " .. step)
    end
    -- secret.automation.stop_routine()
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### path_finished()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
path_finished()
</code>

- Fired when the current destination is reached. Useful to chain routines or run cleanup.

```lua
secret.automation.listener.add("path_finished", "my_script", function()
    print("Destination reached")
    secret.automation.listener.remove("path_finished", "my_script")
end)
```

To run different logic per routine, store state and branch inside the callback:

```lua
local routine_name = "patrol_a"
secret.automation.listener.add("path_finished", "router", function()
    if routine_name == "patrol_a" then
        routine_name = "patrol_b"
        secret.automation.run_routine("patrol_b")
    else
        secret.automation.listener.remove("path_finished", "router")
    end
end)
secret.automation.run_routine("patrol_a")
```
<div hidden>

```ts

```

</div>
