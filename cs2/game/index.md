# game
Helpers for the current match, local player, screen projection, and view angles.

---
## State

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.in_game(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.in_game(): boolean
</code>

- Returns if you are currently in a game.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.is_connected(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.is_connected(): boolean
</code>

- Returns if you are connected to a server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.is_paused(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.is_paused(): boolean
</code>

- Returns if the game is paused.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.max_clients(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.max_clients(): number | nil
</code>

- Returns the max client count for the server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.latency(flow?: number): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.latency(flow?: number): number | nil
</code>

- Returns average net latency.
- `flow` is optional (`0` outgoing, `1` incoming). Defaults to outgoing.

```lua
print(secret.game.latency())
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.net_address(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.net_address(): string | nil
</code>

- Returns the current net channel address.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.is_loopback(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.is_loopback(): boolean
</code>

- Returns if the current connection looks like loopback / localhost.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.get_screen_size(): number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.get_screen_size(): number, number
</code>

- Returns screen width and height.

```lua
local w, h = secret.game.get_screen_size()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.map_name(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.map_name(): string | nil
</code>

- Returns the full map name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.map_short(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.map_short(): string | nil
</code>

- Returns the short map name (e.g. `de_dust2`).

```lua
if secret.game.in_game() then
    print(secret.game.map_short())
end
```

---
## Locals

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.local_player(): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.local_player(): entity | nil
</code>

- Returns your local player pawn. See [entities](/cs2/entities/).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.local_controller(): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.local_controller(): entity | nil
</code>

- Returns your local player controller.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.local_origin(): { x, y, z } | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.local_origin(): { x: number, y: number, z: number } | nil
</code>

- Returns your origin as a table with `x`, `y`, `z`.

```lua
local o = secret.game.local_origin()
if o then
    print(o.x, o.y, o.z)
end
```

---
## Screen / angles

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.world_to_screen(x: number, y: number, z: number): boolean, number?, number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.world_to_screen(x: number, y: number, z: number): boolean, number?, number?
</code>

- Converts a world position to screen coordinates.
- Returns `true, sx, sy` on success, otherwise `false`.

```lua
local ok, sx, sy = secret.game.world_to_screen(x, y, z)
if ok then
    print(sx, sy)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.get_view_angles(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.get_view_angles(): number, number, number
</code>

- Returns pitch, yaw, roll.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.set_view_angles(pitch: number, yaw: number, roll: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.set_view_angles(pitch: number, yaw: number, roll: number)
</code>

- Sets your view angles.

```lua
local p, y, r = secret.game.get_view_angles()
secret.game.set_view_angles(p, y + 1, r)
```

---
## Players

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### game.players(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
game.players(): table
</code>

- Returns a **1-based** list of players with `handle`, `x`, `y`, `z`, `health`, `name`.
- For entity methods use [entities](/cs2/entities/).

```lua
for _, p in ipairs(secret.game.players()) do
    print(p.name, p.health)
end
```

<div hidden>

```ts

```

</div>
