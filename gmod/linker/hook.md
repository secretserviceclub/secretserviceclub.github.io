# hook
This is a first-order hook library replacement using C++.\
Acting as the full replacement, this is by all mean **untraceable** with the ability to use it interstate.\
We recommend you look at the Garry's Mod Wiki for hooks you can attach to.

!!!Pure-Lua Hooks
Do note some hooks on Garry's Mod are **PURE-LUA**, therefore cannot be hooked reliably.\
This means in order to use those hooks will require a breach of security on the user-end.
!!!

!!!warning Meta-Table Transfer
We do not transfer metatables for security reasons (for now).\
However you can repair them using `debug.setmetatable`.
!!!

---
## Example
This is a simple implementation of removing swaying & bobing on weapons.\
Using the meta-tables already existing in menu-state, we can perform math operations quite easily.

```lua
local V = debug.getmetatable(Vector())
local A = debug.getmetatable(Angle())

linker.hook.add("CalcViewModelView", "No-Sway", function(wep, vm, ovec, oang, vec, ang)
    -- fix up metatables
    debug.setmetatable(ovec, V)
    debug.setmetatable(oang, A)
    debug.setmetatable(vec, V)
    debug.setmetatable(ang, A)
    
    -- do ur math here!
    return ovec, oang
end)
```

With linker's<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.meta(library: string, name?: string): function | table
</code>we can grab entire meta-table stacks of userdata values.

```lua
local Entity_Meta = linker.meta("Entity")
Entity_Meta.__index = Entity_Meta
local V = debug.getmetatable(Vector())
local A = debug.getmetatable(Angle())

linker.hook.add("CalcViewModelView", "No-Sway", function(wep, vm, ovec, oang, vec, ang)
    -- wep has the meta-table type of "Entity", same with "VM"
    debug.setmetatable(wep, Entity_Meta)
    debug.setmetatable(vm, Entity_Meta)

    -- Now you can get information about them, ex:
    local class = wep:GetClass()
    if class ~= "weapon_physgun" then
        debug.setmetatable(ovec, V)
        debug.setmetatable(oang, A)
        debug.setmetatable(vec, V)
        debug.setmetatable(ang, A)
        
        -- do ur math here!

        return ovec, oang
    end
end)
```

<div hidden>

```ts

```

</div>
