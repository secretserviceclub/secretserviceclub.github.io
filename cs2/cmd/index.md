# cmd
Modify the current usercmd from [createmove](/cs2/listener/).

---
## Module

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd.current(): cmd | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd.current(): cmd | nil
</code>

- Returns the active cmd, or `nil` outside of createmove.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd.buttons

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd.buttons: { attack, jump, duck, forward, back, use, turnleft, turnright, moveleft, moveright, attack2, reload, sprint, speed, score, scope, zoom, lookatweapon }
</code>

- Button bit flags used by `has_button`, `set_button`, and `remove_button`.
- `speed` is an alias of `sprint`. `zoom` is an alias of `scope`.

```lua
local B = secret.cmd.buttons
```

---
## Usercmd

The cmd object is only valid for the duration of the callback.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:valid(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:valid(): boolean
</code>

- Returns if the cmd is still valid.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:command_number(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:command_number(): number | nil
</code>

- Returns the command sequence number.

---
## Buttons

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_buttons(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_buttons(): number | nil
</code>

- Returns the button mask.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:set_buttons(mask: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:set_buttons(mask: number)
</code>

- Replaces the full button mask.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:has_button(bit: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:has_button(bit: number): boolean
</code>

- Returns if the given button is held.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:set_button(bit: number, down?: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:set_button(bit: number, down?: boolean)
</code>

- Sets a button on or off. `down` defaults to `true`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:remove_button(bit: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:remove_button(bit: number)
</code>

- Releases a button.

---
## Angles

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_view_angles(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_view_angles(): number, number, number
</code>

- Returns pitch, yaw, roll on the cmd.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:set_view_angles(pitch: number, yaw: number, roll: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:set_view_angles(pitch: number, yaw: number, roll: number)
</code>

- Sets pitch, yaw, roll on the cmd (including subtick history).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:lock_angles()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:lock_angles()
</code>

- Pushes the cmd viewangles into the game view (silent-aim style lock).

```lua
cmd:set_view_angles(p, y, r)
cmd:lock_angles()
```

---
## Movement

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_move(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_move(): number, number, number
</code>

- Returns forward, side (left), and up move.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:set_move(forward: number, side: number, up: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:set_move(forward: number, side: number, up: number)
</code>

- Sets forward, side, and up move.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_forward_move() / set_forward_move(v)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_forward_move(): number | nil
cmd:set_forward_move(value: number)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_left_move() / set_left_move(v)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_left_move(): number | nil
cmd:set_left_move(value: number)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_up_move() / set_up_move(v)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_up_move(): number | nil
cmd:set_up_move(value: number)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:rotate_movement(yaw: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:rotate_movement(yaw: number)
</code>

- Rotates forward/side move toward `yaw` without changing viewangles.

```lua
cmd:set_forward_move(1)
cmd:set_left_move(0)
cmd:rotate_movement(target_yaw)
```

---
## Impulse / mouse

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_impulse() / set_impulse(v)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_impulse(): number | nil
cmd:set_impulse(value: number)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cmd:get_mouse_delta() / set_mouse_delta(dx, dy)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cmd:get_mouse_delta(): number, number
cmd:set_mouse_delta(dx: number, dy: number)
</code>

```lua
secret.listener.add("createmove", "example", function(cmd)
    if not cmd:valid() then return end
    if cmd:has_button(secret.cmd.buttons.jump) then
        cmd:remove_button(secret.cmd.buttons.jump)
    end
end)
```

<div hidden>

```ts

```

</div>
