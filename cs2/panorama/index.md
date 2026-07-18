# panorama
Run Panorama JavaScript and call UI APIs from Lua.

---
## Helpers

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### panorama.ready(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
panorama.ready(): boolean
</code>

- Returns if panorama is ready to use.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### panorama.root(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
panorama.root(): string | nil
</code>

- Returns the active root panel name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### panorama.find(panel_id: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
panorama.find(panel_id: string): boolean
</code>

- Returns if a panel with the given id exists.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### panorama.run(code: string, panel?: string, origin?: string): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
panorama.run(code: string, panel?: string, origin?: string): any
</code>

- Runs JavaScript and returns the result.
- Pass `panel` to run on a specific panel, otherwise the active root is used.

```lua
if secret.panorama.ready() then
    print(secret.panorama.run("return MyPersonaAPI.GetXuid();"))
end
```

---
## Proxies

Indexing `secret.panorama` lets you call APIs directly:

```lua
local xuid = secret.panorama.MyPersonaAPI.GetXuid()
```

If the first key matches a panel id, calls are scoped to that panel:

```lua
secret.panorama.CSGOMainMenu.UiToolkitAPI -- etc
```

`run`, `ready`, `find`, and `root` stay as normal functions.

```lua
secret.listener.add("paint", "pano_once", function()
    if not secret.panorama.ready() then return end
    print(secret.panorama.MyPersonaAPI.GetXuid())
    secret.listener.remove("paint", "pano_once")
end)
```

<div hidden>

```ts

```

</div>
