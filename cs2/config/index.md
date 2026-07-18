# config
Read and write cheat settings from Lua using string keys; each key has a fixed type (`bool`, `int`, `float`, `color`, `multi`, or `string`). The in-game menu and [ui](/cs2/ui/) controls reference the same keys-often via `config_name` on a widget.

---
## Get and set

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.get(key: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.get(key: string)
</code>

- Reads a value by config key. Return shape depends on the key’s type:
  - **bool** — single boolean
  - **int** / **float** — single number
  - **string** — single string
  - **color** — four values `r, g, b, a` in **0–255** (use multiple assignment)
  - **multi** — table with **string** keys (e.g. `"0"`, `"1"`) mapping to booleans

```lua
local autostrafe = secret.config.get("misc_auto_strafe")
local smooth = secret.config.get("misc_auto_strafe_smooth")

local r, g, b, a = secret.config.get("Scheme")
print("Scheme:", r, g, b, a)

local multi = secret.config.get("some_multi_key")
for k, v in pairs(multi) do
    print(k, v)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.set(key: string, value: boolean | number | string | table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.set(key: string, value: boolean | number | string | table)
</code>

- Writes a value; `value` must match the key’s type:
  - **bool** — boolean
  - **int** / **float** — number
  - **string** — string
  - **color** — table with **1-based** indices `1-4`, channels **0–255**
  - **multi** — table with **string** keys that parse as integers and **boolean** values

```lua
secret.config.set("misc_auto_strafe", false)
secret.config.set("misc_auto_strafe_smooth", 50)
secret.config.set("Scheme", { 255, 255, 255, 255 })

secret.config.set("some_multi_key", {
    ["0"] = true,
    ["1"] = false,
})
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.type(key: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.type(key: string): string
</code>

- Returns `"bool"`, `"int"`, `"float"`, `"color"`, `"multi"`, or `"string"`.

```lua
local t = secret.config.type("misc_auto_strafe")
if t == "bool" then
    -- ...
end
```

---
## Files

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.load(config_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.load(config_name: string)
</code>

- Loads a saved config by name.

```lua
secret.config.load("my_config")
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.save(config_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.save(config_name: string)
</code>

- Saves the current settings.

```lua
secret.config.save("my_config")
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.list(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.list(): table
</code>

- **1-based** list of saved config names.

```lua
local names = secret.config.list()
for i, name in ipairs(names) do
    print(i, name)
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### config.directory(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
config.directory(): string
</code>

- Absolute path of the configs folder.

```lua
print(secret.config.directory())
```

<div hidden>

```ts

```

</div>
