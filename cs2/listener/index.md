# listener
Callbacks for game / paint / cmd events.

---

[!ref Signal](/libraries/signal/#library-functions)

## paint

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint(width: number, height: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint(width: number, height: number)
</code>

- Called every frame with the screen width and height.

```lua
secret.listener.add("paint", "example", function(w, h)
    -- ...
end)
```

---
## createmove

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### createmove(cmd: cmd)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
createmove(cmd: cmd)
</code>

- Called each createmove with the current [cmd](/cs2/cmd/).
- The cmd is only valid inside this callback.

```lua
secret.listener.add("createmove", "bhop_strip", function(cmd)
    cmd:remove_button(secret.cmd.buttons.jump)
end)
```

---
## game_event

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game_event(event: game_event)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game_event(event: game_event)
</code>

- Called when a game event is fired.
- The event object is only valid inside this callback.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:valid(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:valid(): boolean
</code>

- Returns if the event is still valid.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:name(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:name(): string | nil
</code>

- Returns the event name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_bool(key: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_bool(key: string): boolean
</code>

- Returns a boolean field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_int(key: string): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_int(key: string): number | nil
</code>

- Returns an int field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_float(key: string): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_float(key: string): number | nil
</code>

- Returns a float field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_string(key: string): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_string(key: string): string | nil
</code>

- Returns a string field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_uint64(key: string): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_uint64(key: string): string | nil
</code>

- Returns a uint64 field as a string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_player_index(key: string): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_player_index(key: string): number | nil
</code>

- Returns a player index field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_controller(key: string): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_controller(key: string): entity | nil
</code>

- Returns the controller for a player field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### event:get_pawn(key: string): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
event:get_pawn(key: string): entity | nil
</code>

- Returns the pawn for a player field.

```lua
secret.listener.add("game_event", "deaths", function(ev)
    if not ev:valid() or ev:name() ~= "player_death" then return end
    local victim = ev:get_controller("userid")
    if victim then
        print(victim:name(), "died")
    end
end)
```

---
## level_init

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### level_init(map: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
level_init(map: string)
</code>

- Called when a map loads.

```lua
secret.listener.add("level_init", "reset", function(map)
    print(map)
end)
```

---
## level_shutdown

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### level_shutdown()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
level_shutdown()
</code>

- Called when a map unloads.

---
## frame_stage

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### frame_stage(stage: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
frame_stage(stage: number)
</code>

- Called on client frame stage.

```lua
secret.listener.add("frame_stage", "example", function(stage)
    print(stage)
end)
```

---
## Delay / unload

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### Delay(seconds: number, callback: () => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
Delay(seconds: number, callback: () => void)
</code>

- Schedules `callback` after `seconds` of realtime.
- Available as `Delay` and `secret.Delay`.
- Cleared automatically when the script stops.

```lua
Delay(1.5, function()
    print("later")
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### __shutdown()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
__shutdown()
</code>

- Optional global. Called right before the script state is closed.

```lua
function __shutdown()
    print("script unloading")
end
```

<div hidden>

```ts

```

</div>
