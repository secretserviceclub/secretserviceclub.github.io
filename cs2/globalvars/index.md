# globalvars
Read-only engine globals.

```lua
print(secret.globalvars.curtime, secret.globalvars.tickcount)
```

---
## Fields

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.realtime: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.realtime: number
</code>

- Time since the game started.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.framecount: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.framecount: number
</code>

- Absolute frame count.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.absolute_frametime: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.absolute_frametime: number
</code>

- Averaged frame time.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.max_clients: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.max_clients: number
</code>

- Max clients on the current server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.curtime: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.curtime: number
</code>

- Current server time.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.frametime: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.frametime: number
</code>

- Delta time between frames.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.tick_fraction: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.tick_fraction: number
</code>

- Fractional tick value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.tickcount: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.tickcount: number
</code>

- Current tick count.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.map: string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.map: string | nil
</code>

- Relative map path.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### globalvars.map_name: string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
globalvars.map_name: string | nil
</code>

- Current map name.

```lua
local fps = 1 / secret.globalvars.frametime
print(secret.globalvars.map_name, fps)
```

<div hidden>

```ts

```

</div>
