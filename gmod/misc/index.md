# misc
Miscellaneous API features that don't have their own table.

---
## Identity & screenshot

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_username(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_username(): string
</code>

- Current username in the cheat.

```lua
secret.misc.get_username()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.in_screenshot(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.in_screenshot(): boolean
</code>

- True while a screenshot is being captured.

```lua
secret.misc.in_screenshot()
```

---
## Freecam

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_freecam_pos(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_freecam_pos(): table
</code>

- Freecam position `{ x, y, z }`. Nil if freecam is off.

```lua
local pos = secret.misc.get_freecam_pos()
if pos then print(pos.x, pos.y, pos.z) end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_freecam_angles(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_freecam_angles(): table
</code>

- Freecam view angles.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_spectating(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_spectating(): number
</code>

- Spectated player entity index, or 0 if not spectating.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.start_spectating(index: number, firstperson: boolean): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.start_spectating(index: number, firstperson: boolean): boolean
</code>

- Start spectating a player. Requires freecam to be on and a valid alive player index (not local player). **firstperson:** true = first person, false = third person. Returns false if not in game, freecam off, invalid index, or target not valid.

```lua
if secret.misc.start_spectating(ply:EntIndex(), false) then
    print("Spectating " .. ply:Nick())
end
```

---
## Input

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.sendmouse(action: string, x?: number, y?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.sendmouse(action: string, x?: number, y?: number)
</code>

- Send a mouse action. **action:** `"left"` (down/up with boolean), `"right"` (down/up), `"move"` (dx, dy), `"wheel"` (amount).

```lua
secret.misc.sendmouse("left", true)
secret.misc.sendmouse("left", false)
secret.misc.sendmouse("move", 100, 200)
secret.misc.sendmouse("wheel", 120)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.sendkey(vk: number, press: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.sendkey(vk: number, press: boolean)
</code>

- Send key press or release. **vk** is virtual key code (e.g. `0x44` = D, `0x20` = Space).

```lua
secret.misc.sendkey(0x44, true)
secret.misc.sendkey(0x44, false)
```

---
## ESP

!!!warning Deprecated
`misc.add_to_player_esp` and `misc.add_to_ent_esp` have been removed. Use [!ref draw_player_esp](/gmod/listener/#draw_player_esp) and [!ref draw_entity_esp](/gmod/listener/#draw_entity_esp) instead.
!!!

---
## Aimbot

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_aimbot_target(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_aimbot_target(): number
</code>

- Current aimbot target entity index, or nil if none.

---
## Console & cvars

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.command(cmd: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.command(cmd: string)
</code>

- Run a console command string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.setcvar(cvar: string, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.setcvar(cvar: string, value: string)
</code>

- Set a cvar to a value.

---
## Network

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_address(): string | false

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_address(): string | false
</code>

- Address of the current server, or false if not connected.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.is_connected(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.is_connected(): boolean
</code>

- True if connected to a server.

---
## Entity list

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.add_to_entity_list(entity_name: string, action: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.add_to_entity_list(entity_name: string, action: boolean)
</code>

- Add (`true`) or remove (`false`) an entity from the entity list. Entity must already be in the list (scripted entities).

```lua
secret.misc.add_to_entity_list("gmod_hands", true)
secret.misc.add_to_entity_list("gmod_hands", false)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_entity_list(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_entity_list(): table
</code>

- Table of scripted entity class names to boolean (selected or not).

```lua
for name, selected in pairs(secret.misc.get_entity_list()) do
    print(name, selected)
end
```

---
## Time & misc

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.desync_time(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.desync_time(): number
</code>

- Desynced time when using the desync feature.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.current_charge(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.current_charge(): number
</code>

- Current charge ticks when using tickbase shift.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### misc.get_random_source(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
misc.get_random_source(): string
</code>

- Random loaded Lua source file name/path. Affected by "static source" in the Lua tab.
