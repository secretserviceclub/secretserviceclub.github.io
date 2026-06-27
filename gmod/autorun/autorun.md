# autorun
Autorun is a special folder under the `luas` directory.\
These folders get generated when needed, you can use this to create automated startup scripts.

---
## Locations

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/*.lua
</code>

- Executes shared lua files both menu & client
- On the client this will execute as soon as the lua_State is created, which is before `lua/includes/init.lua`
- On the menu this will execute as soon as you initialize or attach to the process

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/firstframe/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/firstframe/*.lua
</code>

- Executes shared lua files both menu & client
- On the client this will execute as soon as the first-frame of the game-world is rendered
- On the menu this will execute as soon as the first-frame of the game-world is rendered

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/client/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/client/*.lua
</code>

- On the client this will execute as soon as the lua_State is created, which is before `lua/includes/init.lua`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/menu/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/menu/*.lua
</code>

- On the menu this will execute as soon as you initialize or attach to the process

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/client/firstframe/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/client/firstframe/*.lua
</code>

- On the client this will execute as soon as the first-frame of the game-world is rendered

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/menu/firstframe/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/menu/firstframe/*.lua
</code>

- On the menu this will execute as soon as the first-frame of the game-world is rendered

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/client/[SERVER_ADDRESS]/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/client/[SERVER_ADDRESS]/*.lua
</code>

- This is server specific based on `IP_PORT` format, for example: `127.0.0.1_27017`, for localhost it would be `loopback`
- On the client this will execute as soon as the lua_State is created, which is before `lua/includes/init.lua`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/menu/[SERVER_ADDRESS]/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/menu/[SERVER_ADDRESS]/*.lua
</code>

- This is server specific based on `IP_PORT` format, for example: `127.0.0.1_27017`, for localhost it would be `loopback`
- On the menu this will execute as soon as the client's lua_State is created, which is before `lua/includes/init.lua`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/client/[SERVER_ADDRESS]/firstframe/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/client/[SERVER_ADDRESS]/firstframe/*.lua
</code>

- This is server specific based on `IP_PORT` format, for example: `127.0.0.1_27017`, for localhost it would be `loopback`
- On the client this will execute as soon as the first-frame of the game-world is rendered

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### /autorun/menu/[SERVER_ADDRESS]/firstframe/*.lua

</div>

<code class="language-markdown" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
/autorun/menu/[SERVER_ADDRESS]/firstframe/*.lua
</code>

- This is server specific based on `IP_PORT` format, for example: `127.0.0.1_27017`, for localhost it would be `loopback`
- On the menu this will execute as soon as the first-frame of the game-world is rendered

<div hidden>

```md

```

</div>
