# reflection
Responsible for lua-scripting execution and handling of API access cross-states.\
You can use this to also contact other lua_State instances, and create new ones.\
Do note you are responsible for spinning up new states.

!!!warning lua_State Data Transfer
Data transfer for these types are prohibited due to complications & safety:
- Thread
- Proto
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.is(name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.is(name: string): boolean
</code>

- checks if the current execution is of a named `lua_State`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.get(name: string): lua_State?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.get(name: string): lua_State?
</code>

- attempts to locate a `lua_State`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.current(): lua_State

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.current(): lua_State
</code>

- gets the current `lua_State` this is executed in

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.all(): {[index: string]: lua_State}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.all(): {[index: string]: lua_State}
</code>

- gets all instances of `lua_State` and their names

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.name(lua_State* state): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.name(lua_State* state): string
</code>

- converts a `lua_State` to its named counterpart

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.execute(source: string, name: string, state?: lua_State): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.execute(source: string, name: string, state?: lua_State): string?
</code>

- executes lua on a `lua_State` or the current active state its in

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.compile(source: string, name: string): function | string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.compile(source: string, name: string): function | string
</code>

- compiles lua on the the current active state its in

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.open(name: string): lua_State

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.open(name: string): lua_State
</code>

- spawns a new `lua_State` instance or returns one if it already exists

```lua
-- creates a new lua_State
local state = reflection.open("lua_State.magic")

-- execute lua right onto the stack
reflection.execute([[
    print("new lua_State boys!")
]], "test", state)

-- you can use basic stack manipulation here as well
print("\nprinting this lua_State's stuff")
reflection.stack(function(L)
    L:pushvalue(-10002)
    L:pushnil()
    while L:next(-2) do
        if L:isstring(-2) then
            print(L:getstring(-2))
        end
        L:pop()
    end
end, state)

-- if you really don't need it, you can close it
reflection.close(state)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.close(state: lua_State)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.close(state: lua_State)
</code>

- destroys a `lua_State` instance
- this won't work on games with built-in `lua_State` instances

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### reflection.stack(func: function(L: lua_State), state?: lua_State): any...

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
reflection.stack(func: function(L: lua_State), state?: lua_State): any...
</code>

- creates a stack isolated bridge to a lua_State.
- do note that you don't need to do this but using this reduces the risk of overflows.
```lua
-- this is in menu-state or another lua-state
local other_state = reflection.get("other_state")

local res = reflection.stack(function(L)
    L:pushnumber(20)
    local num = L:tonumber(-1)
    L:pop()
    return num
end, other_state)

print(res) -- 20

-- you can also do it outside the stack isolation if needed:
L:pushnumber(20)
local res = L:tonumber(-1)
L:pop()

print(res) -- 20
```

---
## Lua State
These are interface & function definitions for how we handle `lua_State`

!!!warning Non-Preemptive Errors
This library can cause internal errors in Lua, likely causing a crash.
!!!

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:execute(source: string, name: string): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:execute(source: string, name: string): string?
</code>

- executes lua on a `lua_State`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:compile(source: string, name: string): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:compile(source: string, name: string): string?
</code>

- compiles lua on a `lua_State`.
- do note that doing this will push the function onto the stack, consider seeing more in CAPI.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:stack(func: function(L: lua_State)): any?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:stack(func: function(L: lua_State)): any?
</code>

- creates a stack isolated bridge to a lua_State.
- do note that you don't need to do this but using this reduces the risk of overflows.

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:api(): API

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:api(): API
</code>

- Pushes the API onto the stack for access

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:call(inputs: number, outputs: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:call(inputs: number, outputs: number)
</code>

- Calls a function thats pushed onto the stack
- This will *consume* the no. inputs first, then execute the functions
```lua
L:reflection.compile("print(({...})[1])", "example")
L:pushstring("hello world")
L:call(1, 0) -- calls "example" with "hello world"
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pop(count?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pop(count?: number)
</code>

- Pops a value off of the stack at the top

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:remove(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:remove(index: number)
</code>

- Removes a value at an index off of the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:length(index: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:length(index: number): number
</code>

- Used to get the length of a value

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:next(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:next(index: number): boolean
</code>

- A pair-style iterator function for going through table
```lua
L:newtable() -- example

L:pushnil() -- push an invalid key to jump-start the iterator
while L:next(-2) do -- target table for key-grabbing
    -- this pushes 2 values onto the stack, -1: value, -2: key
    L:pop(); -- pop the value, keep the key so 'next' can keep going
end

L:pop() -- pop table off stack
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushany(value: any)

</div>

<div style="margin-bottom: 10px;"><code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushany(value: any)
</code></div>

- Transfers any datatype from your environment to the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getany(index: number): any

</div>

<div style="margin-bottom: 10px;"><code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getany(index: number): any
</code></div>

- Transfers any datatype from the stack to your environment

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:gettop(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:gettop(): number
</code>

- Gets the current size of the Lua stack
- This is useful for vararg style handling

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:gettype(index: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:gettype(index: number): number
</code>

- Gets the type ID of a given value

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:gettypename(index: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:gettypename(index: number): string
</code>

- Gets the typename of a given value

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:newtable()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:newtable()
</code>

- Generates a blank table and pushes it onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:newref(index: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:newref(index: number): number
</code>

- Creates a reference link to a value
- This will make the value immune to the garbage collector

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushref(reference: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushref(reference: number)
</code>

- Pushes the referenced value back onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:rmref(reference: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:rmref(reference: number)
</code>

- Removes the referenced value from registry

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getupvalue(index: number, id: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getupvalue(index: number, id: number): string
</code>

- Gets the "upvalue" of a function at the top of the stack
- Upvalues are values passed to a function not as a parameter, but by reference

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:setupvalue(index: number, id: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:setupvalue(index: number, id: number): string
</code>

- Sets the "upvalue" of a function at the top of the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getfenv(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getfenv(index: number)
</code>

- Grabs the ENV and pushes it onto the stack
- You can use this to manipulate the environment

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:setfenv(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:setfenv(index: number)
</code>

- Sets the ENV of a functions at the index
- This consumes the table you provide it at the top of the stack
- You can use this to manipulate the environment

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getmetatable(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getmetatable(index: number): boolean
</code>

- Grabs the metatable of a table or userdata, and pushes it onto the stack
- The boolean is provided for if it fails to grab the metatable

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:setmetatable(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:setmetatable(index: number)
</code>

- Sets the metatable of a table or userdata at the index
- This consumes the table you provide it at the top of the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getfield(index: number, key: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getfield(index: number, key: string)
</code>

- Gets the value from a table and pushes it onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:setfield(index: number, key: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:setfield(index: number, key: string)
</code>

- Sets a value in a table by key
- Index corresponds to where the table is on the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:gettable(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:gettable(index: number)
</code>

- Gets the value from a table and pushes it onto the stack
- This will consume a value just before it to determine the key

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:settable(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:settable(index: number)
</code>

- Sets a value in a table by the key at the top of the stack
- The top of the stack is the key, and top-1 is the value

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:rawget(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:rawget(index: number)
</code>

- Gets the value from a table and pushes it onto the stack
- This will consume a value just before it to determine the key
- Unlike gettable this will not invoke metatable callbacks

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:rawset(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:rawset(index: number)
</code>

- Sets a value in a table by the key at the top of the stack
- The top of the stack is the key, and top-1 is the value
- Unlike settable this will not invoke metatable callbacks

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getboolean(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getboolean(index: number): boolean
</code>

- Attempts to get a boolean value from the Lua stack
- If the type is invalid, an error will be thrown

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getnumber(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getnumber(index: number)
</code>

- Attempts to get a number value from the Lua stack
- If the type is invalid, an error will be thrown

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:getstring(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:getstring(index: number)
</code>

- Attempts to get a string value from the Lua stack
- If the type is invalid, an error will be thrown

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushboolean(value: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushboolean(value: boolean)
</code>

- Pushes a boolean onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushnil()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushnil()
</code>

- Pushes a nil value onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushnumber(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushnumber(value: number)
</code>

- Pushes a number onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushstring(value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushstring(value: string)
</code>

- Pushes a string onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushfunction(value: function) 

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushfunction(value: function) 
</code>

- Pushes a function onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushtable(value: table) 

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
 L:pushtable(value: table) 
</code>

- Pushes a table onto the stack

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:pushvalue(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:pushvalue(index: number)
</code>

- Makes a copy of a value at the index and pushes it to the top of the stack

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isboolean(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isboolean(index: number): boolean
</code>

- Checks if the value at index on the stack is a boolean

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:iscfunction(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:iscfunction(index: number): boolean
</code>

- Checks if the value at index on the stack is a cfunction

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isfunction(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isfunction(index: number): boolean
</code>

- Checks if the value at index on the stack is a function

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:islightuserdata(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:islightuserdata(index: number): boolean
</code>

- Checks if the value at index on the stack is a lightuserdata

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isnil(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isnil(index: number): boolean
</code>

- Checks if the value at index on the stack is nil

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isnumber(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isnumber(index: number): boolean
</code>

- Checks if the value at index on the stack is a number

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isstring(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isstring(index: number): boolean
</code>

- Checks if the value at index on the stack is a string

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:istable(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:istable(index: number): boolean
</code>

- Checks if the value at index on the stack is a table

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isthread(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isthread(index: number): boolean
</code>

- Checks if the value at index on the stack is a thread

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:isuserdata(index: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:isuserdata(index: number): boolean
</code>

- Checks if the value at index on the stack is a userdata

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### L:istype(index: number, type: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
L:istype(index: number, type: number): boolean
</code>

- Checks if the value matches a specific type ID

<div hidden>

```ts

```

</div>
