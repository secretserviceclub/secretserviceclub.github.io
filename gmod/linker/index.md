# linker
Responsible for finding and retrieving lua functions that could be detoured and overwritten.\
Its also a powerful library utilizing reflection's interstate capabilities.

!!!warning Meta-Table Transfer
We do not transfer metatables for security reasons (for now).\
However you can repair them using `debug.setmetatable`.
!!!

---
## Example
You can call some functions cross-state if you feel the client-side is too unsafe.
```lua
-- do note safety of isolate function still applies here
local print = print
local tostring = tostring
local setmetatable = debug.setmetatable
local FindMetaTable = FindMetaTable
local PrintTable = PrintTable

print("menu-state or anystate can now call client-side functions")
linker.isolate(true)

local lp = GLOBAL.LocalPlayer()
print("HP: " .. Entity.Health(lp))
print("Alive: " .. tostring(Player.Alive(lp)))

local pos = Entity.EyePos(lp)
setmetatable(pos, FindMetaTable("Vector"))
print("Position: " .. tostring(pos))

local color = Entity.GetColor(lp)
PrintTable(color)

linker.isolate(false)
```

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### linker.meta(library: string, name?: string): function | table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.meta(library: string, name?: string): function | table
</code>

- Fetches a metatable class function, like `"Player.GetEyeAngles"`
- Not providing a name will return the entire table

```lua
local GetEyeAngles = linker.meta("Player", "GetEyeAngles") -- Get's Player's metatable GetEyeAngles
local Entity = linker.meta("Entity") -- Get's Entity.*, basically all functions under Entity
--> ex: Entity.GetClass
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### linker.global(library: string, name?: string): function | table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.global(library: string, name?: string): function | table
</code>

- Fetches a global class function, like `"surface.CreateFont"`
- To fetch raw globals do `"GLOBAL"`, like `"GLOBAL.SysTime"`
- Not providing a name will return the entire table

```lua
local SysTime = linker.global("GLOBAL", "SysTime") -- Get's SysTime global
local util = linker.global("util") -- Get's util.*, basically all functions under util
--> ex: util.TraceLine
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### linker.isolate(state?: boolean): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.isolate(state?: boolean): boolean
</code>

- Creates an abolute isolated states, where _G and the ENV will only access linker libraries
- This is for absolute safety, if any access happens thats not available in linker, it will throw an error for protection reasons
```lua
linker.isolate(true)

-- creates detour resistance, these will always be original functions
net.Start("example")
net.SendToServer()

local a = some_random_global_variable -- error, linker does not recognize this global

linker.isolate(false)

local a = some_random_global_variable -- doesn't error as env is restored
```

<div hidden>

```ts

```

</div>
