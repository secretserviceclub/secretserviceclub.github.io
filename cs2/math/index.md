# math
Angle helpers on top of the standard Lua `math` library.

---
## Angles

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.calc_angle(src, dst): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.calc_angle(src: {x,y,z} | number,number,number, dst: {x,y,z} | number,number,number): number, number, number
</code>

- Returns pitch, yaw, roll from `src` to `dst`.
- Vectors can be tables `{x,y,z}` or three numbers.

```lua
local p, y, r = secret.math.calc_angle(eye, target)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.angle_forward(angles): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.angle_forward(angles: {x,y,z} | number,number,number?): number, number, number
</code>

- Returns a unit forward vector from pitch / yaw (/ roll).
- Accepts `{x,y,z}`, `{pitch,yaw,roll}`, or `pitch, yaw[, roll]`.

```lua
local pitch, yaw = secret.game.get_view_angles()
local fx, fy, fz = secret.math.angle_forward(pitch, yaw)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.normalize_angles(angles): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.normalize_angles(angles: {x,y,z} | number,number,number): number, number, number
</code>

- Normalizes pitch / yaw into usable view ranges.

---
## Lerp

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.lerp(a, b, t): number | number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.lerp(a: number, b: number, t: number): number
math.lerp(a: vector, b: vector, t: number): number, number, number
</code>

- Linear interpolate. Scalar or vector form.

```lua
local x, y, z = secret.math.lerp(from, to, 0.5)
```
