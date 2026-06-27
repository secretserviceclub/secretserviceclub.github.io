# signal
The Lua event handler for interstate & C++ calls.\
You can use this to contact other `lua_State` objects, make calls to C++, or have C++ make calls to you.\
Some libraries will have a `Signal` section to let you know of events they have, the functions here are for those libraries.

---
## Lua Functions
This is strictly for Lua based calls without a C++ counterpart.\
Supports interstate functionality, so that you can make calls to other `lua_State` threads.

```lua
local state = reflection.open("example")

reflection.execute([[
signal.add("test", "example", function(...)
    print(...)
end)
]], "example_name", state)

signal.call(state, "test", "hello world") -- print on example lua_State: [example] hello world
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.add(name: string, identity: string, callback: function)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.add(name: string, identity: string, callback: function)
</code>

- Adds a function to an signal, this will call the callback when C++ invokes it

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.remove(name: string, identity: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.remove(name: string, identity: string)
</code>

- Removes a function from a signal

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.get(name: string, identity: string): function?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.get(name: string, identity: string): function?
</code>

- Attempts to retrieve a function from the signal callbacks

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.call(state: lua_State, name: string, ...any): ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.call(state: lua_State, name: string, ...any): ...any
</code>

- Calls events on a `lua_State`
- Must have the same matching name for them to actually call

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.connect(name: string, callback: function, identity: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.connect(name: string, callback: function, identity: string)
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.add(name: string, identity: string, callback: function)
</code>
- Different call style under the RBLX standard

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.disconnect(name: string, identity: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.disconnect(name: string, identity: string)
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.remove(name: string, identity: string)
</code>
- Different call style under the RBLX standard

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.connection(name: string, identity: string): function?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.connection(name: string, identity: string): function?
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.get(name: string, identity: string): function?
</code>
- Different call style under the RBLX standard

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.fire(state: lua_State, name: string, ...any): ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.fire(state: lua_State, name: string, ...any): ...any
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.call(state: lua_State, name: string, ...any): ...any
</code>
- Different call style under the RBLX standard

---
## Library Functions
These exists on libraries that have events or invokers, you can use these to talk to C++

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.add(name: string, identity: string, callback: function)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.add(name: string, identity: string, callback: function)
</code>

- Adds a function to an signal, this will call the callback when C++ invokes it

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.remove(name: string, identity: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.remove(name: string, identity: string)
</code>

- Removes a function from a signal

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.get(name: string, identity: string): function?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.get(name: string, identity: string): function?
</code>

- Attempts to retrieve a function from the signal callbacks

[!badge variant="secondary" text="stub"] <code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.call(name: string, ...any): ...any
</code>

- Useful under conditions where C++ has multiple functions for a single purpose
- Depends on the C++ developer's implementation

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.connect(name: string, callback: function, identity: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.connect(name: string, callback: function, identity: string)
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.add(name: string, identity: string, callback: function)
</code>
- Different call style under the RBLX standard

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.disconnect(name: string, identity: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.disconnect(name: string, identity: string)
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.remove(name: string, identity: string)
</code>
- Different call style under the RBLX standard

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### signal.connection(name: string, identity: string): function?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.connection(name: string, identity: string): function?
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.get(name: string, identity: string): function?
</code>
- Different call style under the RBLX standard

[!badge variant="secondary" text="stub"] <code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.fire(name: string, ...any): ...any
</code>

- Same as<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
signal.call(name: string, ...any): ...any
</code>
- Different call style under the RBLX standard

<div hidden>

```ts

```

</div>
