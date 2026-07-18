# trace
World / entity line and hull traces.

---
## Line

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### trace.line(start, end, skip?): table | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
trace.line(start: vector, end: vector, skip?: entity): { fraction, hit, entity, ... } | nil
</code>

- Traces a line from `start` to `end`.
- Vectors can be `{x,y,z}` or three numbers each.
- `skip` defaults to the local player pawn.

```lua
local tr = secret.trace.from_eyes(8192)
if tr and tr.hit then
    print(tr.fraction, tr.entity and tr.entity:name())
end
```

```lua
local me = secret.game.local_player()
local ex, ey, ez = me:eye_pos()
local pitch, yaw = secret.game.get_view_angles()
local fx, fy, fz = secret.math.angle_forward(pitch, yaw)
local dist = 8192
local tr = secret.trace.line(ex, ey, ez, ex + fx * dist, ey + fy * dist, ez + fz * dist)
```

Result fields: `fraction`, `all_solid`, `hit`, `start_pos`, `end_pos`, `pos`, `normal`, `entity`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### trace.from_eyes(distance?: number, skip?: entity): table | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
trace.from_eyes(distance?: number, skip?: entity): table | nil
</code>

- Traces from the local eye position along the current view angles.
- `distance` defaults to `8192`.

---
## Hull

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### trace.hull(start, end, mins, maxs, skip?): table | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
trace.hull(start: vector, end: vector, mins: vector, maxs: vector, skip?: entity): table | nil
</code>

- Hull / bbox trace with `mins` / `maxs`.
