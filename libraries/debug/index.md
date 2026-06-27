# debug
This is an expansion to the existing Lua debug library.\
This allows you to create many ways of accessing data that would be otherwise impossible.\
As well as providing security features for safety of instrusions to lua-based APIs not from the **Interstellar Engine**.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getfenv(obj: function | number): table?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getfenv(obj: function | number): table?
</code>

- Returns the environment of object obj.
- This differs a bit from the base function getfenv, which takes a function or a level number, and converts the level number into a function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.gethook(thread: thread | function | number): function, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.gethook(thread: thread | function | number): function, number, number
</code>

- Returns the current hook settings as three values: Hook Function, Mask, Count

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getinfo(thread: thread | function | number, field?: string, what?: function): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getinfo(thread: thread | function | number, field?: string, what?: function): table
</code>

- Returns a table with information about a function or stack level
```
f - returns "func" field
l - returns "currentline" field
L - returns a table whose indices are the numbers of the lines that are valid on the function. (A valid line is a line with some associated code, that is, a line where you can put a break point. Non-valid lines include empty lines and comments.)
n - returns "name" and "namewhat" fields
S - returns "source", "short_src", "linedefined" and "what" fields
u - returns "nups" field
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getlocal(level: number | function, local: number): string, any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getlocal(level: number, local: number): string, any
</code>

- Returns the name and value of the local variable with the index 'local' of the function at 'level' on the stack.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getmetatable(obj: proto | function | table | userdata): table?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getmetatable(obj: proto | function | table | userdata): table?
</code>

- Returns the metatable of the given object or nil if it does not have a metatable.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getregistry(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getregistry(): table
</code>

- Returns the registry table, which is a special table used by C functions to store information it wants to keep isolated from Lua functions.
- This can act as permanent storage for variables to be retreived later on.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getupvalue(level: number | function, upvalue: number): string, any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getupvalue(level: number | function, upvalue: number): string, any
</code>

- Similar to debug.getlocal, returns the names and values of the upvalues for the nominated function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setfenv(obj: function | number, tbl: table): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setfenv(obj: function | number, tbl: table): any
</code>

- Sets the environment of the given object to the given table, returns the object.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setlocal(obj: function | number, local: number, value: any)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setlocal(obj: function | number, local: number, value: any)
</code>

- Sets the value of the local variable with the index 'local' of the function at 'level' on the stack.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.sethook(thread: thread | function | number, f?: function, mask?: number, count?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.sethook(thread: thread | function | number, f?: function, mask?: number, count?: number)
</code>

- Sets the function f as a hook to be called when the "mask" condition is satisfied.
- If count is non-zero, it is called after every "count" instructions.
- The thread argument is optional and defaults to the current thread.
- If called without arguments, turns off the hook.
- The function f is called with its first parameter being a string, which can be one of: `call, return, tail return, line, count`
```
c - called every time Lua calls a function
r - called every time Lua returns from a function
l - called every time Lua enters a new line of code
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setmetatable(obj: proto | function | table | userdata, tbl: table): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setmetatable(obj: proto | function | table | userdata, tbl: table): any
</code>

- Sets the metatable for the given object to the given table (which can be nil).
- Bypasses the check for the "__metatable" entry.
- Returns the object.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setupvalue(level: number | function, upvalue: number, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setupvalue(level: number | function, upvalue: number, value: number)
</code>

- Similar to debug.setlocal, sets the values of the upvalue for the nominated function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.traceback(thread?: number | function | string, message?: string, level?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.traceback(thread?: number | function | string, message?: string, level?: number)
</code>

- Returns a string with a traceback of the stack call.
- An optional message string is prepended to the beginning of the traceback message.

---
## Extension

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.registry(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.registry(): table
</code>

- Gets the true debug registry table.
- This table is used to keep permanent objects, preventing GC from removing them.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.global(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.global(): table
</code>

- Gets the true global table.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.env(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.env(): table
</code>

- Gets the current stack's environment.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.clone(value: function | proto | userdata): function | proto | userdata

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.clone(value: function | proto | userdata): function | proto | userdata
</code>

- Copys a value in memory, creating a completely new value but with the same characteristics.

```lua
local original_func = function(a, b) return a + b end
local cloned_func = debug.clone(original_func)

print(original_func(5, 3))  -- Output: 8
print(cloned_func(5, 3))    -- Output: 8 (cloned function has the same behavior)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.replace(target: function | proto | userdata, value: function | proto | userdata)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.replace(target: function | proto | userdata, value: function | proto | userdata)
</code>

- Replaces a value by reference in memory, effectively replacing all occurences of it.

```lua
local original = function() print("original call!") end
local replaced = function() print("replaced call!") end 
original()
debug.replace(original, replaced) --  replace, now its gonna print "replaced call!" instead of "original call!"
original()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.newcclosure(func: function): function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.newcclosure(func: function): function
</code>

- Creates a new cfunction closure which is untraceable.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getgc(iterator?: boolean): (table | function | proto | userdata)[] | function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getgc(iterator?: boolean): (table | function | proto | userdata)[] | function
</code>

- Gets the garbage collector table.
- This has iterator functionality in foreach-loops.
- Do note this contains every value in existance.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.topointer(data: any, str: boolean): string | number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.topointer(data: any, str: boolean): string | number
</code>

- Converts a datatype into it's absolute pointer location.
- Output looks like this: `"0xd8ad9caa"` or `3635244450`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.frompointer(ptr: number): function | table | proto | userdata

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.frompointer(ptr: number): function | table | proto | userdata
</code>

- Scans memory to find the pointer association.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.toproto(f: function): proto

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.toproto(f: function): proto
</code>

- Converts an function to a prototype object

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.fromproto(p: proto): function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.fromproto(p: proto): function
</code>

- Converts an prototype into a function handle
- Do note this creates a completely new function

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getprotos(f: function | proto): proto[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getprotos(f: function | proto): proto[]
</code>

- Gets a list of subset protos under a function.
- Think of these as `function() end` inside of the current function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.dump(f: function | proto): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.dump(f: function | proto): string
</code>

- Converts a function or proto into it's bytecode representation.
- This is done with debug information available.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.tosignature(f: function | proto): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.tosignature(f: function | proto, options?: string = "ocu", max?: number = 20): string
</code>

- Creates a signature based on several factors.
- Each options character represents a different form of signature.
- max indicates how much scanning each options should introduce, this is to limit the size of the output string.
- ^ (we will make it semi-automatic later on by unique scanning)
```
o = opcodes
c = constants
u = upvalues
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.fromsignature(sig: string): function | proto | undefined

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.fromsignature(sig: string): function | proto | undefined
</code>

- Attempts to look for a certain function or proto based on the given signature.
- Depending on parameters when you first created the signature, substle changes in a function can invalidate a signature entirely.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.tscan(input: table, comparator: function(value: table): boolean): table?, string[]?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.tscan(input: table, comparator: function(value: table): boolean): table?, string[]?
</code>

- Based on the comparator, attempts to scan for another table thats associated.
- This works to counter-act attempts to hide tables via a proxy or other means.
- This returns a signature array for you to use<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.tresolve(input: table, string[]): table?
</code>instead.

```lua
local function fetch()
    local real_table = {["a"] = true} -- target
    return real_table
end

local test = setmetatable({}, {
    __index = function(self, index)
		return fetch()[index]
	end
})

local test = setmetatable({}, {
    __index = function(self, index)
		return test[index]
	end
})

local test = setmetatable({}, {
    __index = test
})

-- this uses the scanner to find the hidden table
local value, signature = debug.tscan(test, function(value)
    return rawget(value, "a")
end)

if value then
    print("FOUND")
    PrintTable(value)

    -- this uses the signature array to find it instead of re-scanning
    local value = debug.tresolve(test, signature)
    
    if value then
        print("RESOLVED")
        PrintTable(value)
    end
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.tresolve(input: table, string[]): table?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.tresolve(input: table, string[]): table?
</code>

- Like<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.tscan(input: table, comparator: function(value: table): boolean): table?, string[]?
</code>
- However, instead of "scanning" it uses the already generated signature array to find the value.
- This is extremely efficient compared to re-scanning for the designated value via a comparator.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getconstant(f: function | proto, index: number): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getconstant(f: function | proto, index: number): any
</code>

- Gets a function's constant by their index

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getconstants(f: function | proto): {[index: string]: any}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getconstants(f: function | proto): {[index: string]: any}
</code>

- Gets all constants from a function or proto

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setconstant(f: function | proto, index: number, value: any): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setconstant(f: function | proto, index: number, value: any): boolean
</code>

- Sets a constant in a function or proto at an index
- Returns a `boolean` on if it was able to do so

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.iscfunction(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.iscfunction(f: function): boolean
</code>

- Checks if the provided function is made by "C"

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.islfunction(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.islfunction(f: function): boolean
</code>

- Checks if the provided function is made by "Lua"

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setbuiltin(func: cfunction, ffid: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setbuiltin(func: cfunction, ffid: number)
</code>

- Changes a cfunction to be a Fast Function with an ID.
- This will make them appear as `"builtin: xx"`
- Use newcclosure if you plan to make a detour with this.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getbuiltin(func: cfunction): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getbuiltin(func: cfunction): number
</code>

- Gets the ffid number of a cfunction.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getupvalues(func: function): {[index: string]: any}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getupvalues(func: function): {[index: string]: any}
</code>

- Gets a list of upvalues and that a function has.
```lua
local a, b, c = 1, 2, 3
local f = function() print(a, b, c) end
PrintTable(debug.getupvalues(f))
-- prints: {"a" = 1, "b" = 2, "c" = 3}
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.validlevel(level: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.validlevel(level: number): boolean
</code>

- Checks if the level exists and is valid.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getcallstack(): function[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getcallstack(): function[]
</code>

- Gets a list of functions that have been used at the current execution.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getbase(level: number): function?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getbase(level: number): function?
</code>

- Gets the current executing function at a level.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.typestack(count?: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.typestack(count?: number): string
</code>

- Fetches a list of the current stack memory.
- This is used to debug and print out what it looks like.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.getstack(index: number): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.getstack(index: number): any
</code>

- Fetchs directly from the lua stack.
- This can be used to get values in stack memory.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.setstack(index: number, data: any)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.setstack(index: number, data: any)
</code>

- Sets a value at an index in stack memory.
- Warning: this is rather dangerous and can poison the lua stack.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.sync(f: function, callback: function): function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.sync(f: function, callback: function): function
</code>

- Creates a hook towards a target Lua/C function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.async(f: cfunction, callback: function): function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.async(f: cfunction, callback: function): function
</code>

- Creates a hook towards a target C function.
- Unlike sync hooks, this cannot be found due to it being a low-level hook.
- This runs callbacks in a different stack environment preventing stack tracing.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.restore(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.restore(f: function): boolean
</code>

- Attempts to restore a Lua/C function to its original state.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.is(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.is(f: function): boolean
</code>

- Checks if a Lua/C function has been hooked.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.inside(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.inside(): boolean
</code>

- If we are currently executing inside an active hook.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.original(f: function): function?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.original(f: function): function?
</code>

- Fetches the original Lua/C function that has been hooked.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.active(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.active(f: function): boolean
</code>

- Checks if a Lua/C function is actively being hooked.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.disable(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.disable(f: function): boolean
</code>

- Disables an on-going hook from running, effectively making it the original temporarily.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### debug.hook.enable(f: function): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
debug.hook.enable(f: function): boolean
</code>

- Enables an on-going hook, allowing callbacks to be ran.

## CAPI

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:registry()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:registry()
</code>

- Gets the true debug registry table, pushing it onto the stack.
- This table is used to keep permanent objects, preventing GC from removing them.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:global()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:global()
</code>

- Gets the true global table, pushing it onto the stack.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:env()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:env()
</code>

- Gets the current stack's environment, pushing it onto the stack.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getgc()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getgc()
</code>

- Gets the garbage collector table, pushing it onto the stack.
- Do note this contains every value in existance.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:newcclosure(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:newcclosure(index: number)
</code>

- Creates a new cfunction closure which is untraceable.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:clone(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:clone(index: number)
</code>

- Copys a value in memory, creating a completely new value but with the same characteristics.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:replace(target: number, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:replace(target: number, value: number)
</code>

- Replaces a value by reference in memory, effectively replacing all occurences of it.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:topointer(index: number, str: boolean): string | number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:topointer(index: number, str: boolean): string | number
</code>

- Converts a datatype into it's absolute pointer location.
- Output looks like this: `"0xd8ad9caa"` or `3635244450`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:frompointer(ptr: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:frompointer(ptr: number)
</code>

- Scans memory to find the pointer association, pushing it onto the stack.

<div hidden>

```ts

```

</div>
