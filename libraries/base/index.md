# base
This is an expansion to the existing Lua Base library.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.assert(v: any, message?: string): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.assert(v: any, message?: string)
</code>

- Raises an error if value of v is nil or false.
- Message is optional, defaults to "assertion failed!".
- If no error, returns the value v.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.collectgarbage(opt: string, arg?: any): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.collectgarbage(opt: string, arg?: any): number?
</code>

- Responsible for controlling and retrieving information about Lua's garbage collector.
```
"stop": stops the garbage collector.
"restart": restarts the garbage collector.
"collect": performs a full garbage-collection cycle (this is the default if no option supplied)
"count": returns the total memory in use by Lua (in Kbytes).
"step": performs a garbage-collection step. The step "size" is controlled by arg (larger values mean more steps) in a non-specified way. If you want to control the step size you must experimentally tune the value of arg. Returns true if the step finished a collection cycle.
"setpause": sets arg/100 as the new value for the pause of the collector (see below).
"setstepmul": sets arg/100 as the new value for the step multiplier of the collector (see below).
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.error(message: string, level?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.error(message: string, level?: number)
</code>

- Raises an error with the supplied message.
- If a level is supplied the error points to the current function (level 1 or nil), the parent function (level 2) and so on.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.gcinfo()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.gcinfo()
</code>

- Returns Kb of dynamic memory in use.

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.error(message: string, level?: number)
</code>

- Raises an error with the supplied message.
- If a level is supplied the error points to the current function (level 1 or nil), the parent function (level 2) and so on.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.getfenv(f: number | function): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.getfenv(f: number | function): table
</code>

- Returns the current environment used by the nominated function f.
- f can be a function or a number representing the stack level, where 1 is the currently running function, 2 is its parent and so on.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.getmetatable(obj: table | function | userdata): table?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.getmetatable(obj: table | function | userdata): table?
</code>

- Returns metatable for the nominated object.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.ipairs(t: table): function, table, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.ipairs(t: table): function, table, number
</code>

- Returns an iterator function, the table t, and 0, for use in the generic "for" loop.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.next(t: table, i?: index): any, any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.next(t: table, i?: index): any, any
</code>

- Traverses all entries in a table.
- Returns the next index, value pair.
- If index is nil (the default), returns the first pair.
- When called with the last index of the table (or with an index of nil for an empty table), returns nil.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.pairs(t: table): function, table, any?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.pairs(t: table): function, table, any?
</code>

- Returns the 'next' function, the table t, and nil, for use in a for loop.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.pcall(f: function, ...: any): boolean, string | any, ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.pcall(f: function, ...: any): boolean, string | any, ...any
</code>

- Calls function f with the supplied arguments in protected mode.
- Catches errors and returns.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.print(...: any)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.print(...: any)
</code>

- Prints its arguments to stdout

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.rawequal(v1: any, v2: any): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.rawequal(v1: any, v2: any): boolean
</code>

- Returns a boolean depending on v1 == v2 without invoking any table metamethods.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.rawget(t: table, i: any): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.rawget(t: table, i: any): any
</code>

- Gets the real value of table [index] without invoking metamethods.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.rawset(t: table, i: any, v: any)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.rawset(t: table, i: any, v: any)
</code>

- Sets the value of table [index] to value, without invoking metamethods.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.select(index: string | number, ...: any): ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.select(index: string | number, ...: any): ...any
</code>

- If index is a number, returns all items in the list from that number onwards.
- Otherwise index must be the string "#", in which case it returns the number of items in the list.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.setfenv(f: number | userdata | thread | function, env: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.setfenv(f: number | userdata | thread | function, env: table)
</code>

- Sets the current environment to be used by f, which can be a function, userdata, thread or stack level.
- Level 1 is the current function.
- Level 0 is the global environment of the current thread.
- The "env" argument is a table, which effectively becomes the "root" for the environment.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.setmetatable(t: table, metatable: table): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.setmetatable(t: table, metatable: table): table
</code>

- Sets the metatable for the nominated table.
- If metatable is nil, removes the metatable.
- If the original metatable has a "__metatable" entry an error is raised.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.tonumber(v: number | string, base?: number = 10): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.tonumber(v: number | string, base?: number = 10): number
</code>

- Converts n to a number using the optional base (default 10), base can be from 2 to 36.
- For bases > 10 the letters a-z (not case sensitive) represent the digits. (eg. F is 15).
- For decimal numbers you can supply fractions and exponents. Others should be unsigned.
- Returns nil if the number cannot be converted.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.tostring(v: any): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.tostring(v: any): string
</code>

- Converts its argument to a string in a reasonable format.
- If a __tostring metatable field is found, that is used for the conversion.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.type(v: any): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.type(v: any): string
</code>

- Returns a string, which is the type.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.unpack(t: table): ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.unpack(t: table): ...any
</code>

- Returns all elements from the given list (table) as individual values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### base.xpcall(f: function, err: function): boolean, any, ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
base.xpcall(f: function, err: function): boolean, any, ...any
</code>

- Calls function f with err as the custom error handler.
- If an error occurs in f it is caught and the error-handler 'err' is called, then xpcall returns false, and whatever the error handler returned.
- If there is no error in f, then xpcall returns true, followed by the function results from f.

<div hidden>

```ts

```

</div>
