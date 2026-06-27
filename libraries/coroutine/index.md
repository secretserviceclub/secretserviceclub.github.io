# coroutine
This is an expansion to the existing Lua Coroutine library.

Coroutines are a very powerful way of splitting execution of a function up until some event occurs (for example, a timer fires, or input arrives).\
The function chooses when to "yield" execution.

The yield / resume sequence allows variables to be passed back and forward between the thread and the caller.\
For example the thread can yield with an argument which tells the caller why it yielded, and the caller can resume with an argument telling the thread why it was resumed.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### coroutine.create(f: function): thread

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
coroutine.create(f: function): thread
</code>

- Creates a thread consisting of the body f.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### coroutine.resume(t: thread, ...: any): boolean, ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
coroutine.resume(t: thread, ...: any): boolean, ...any
</code>

- Start or resume a thread created by coroutine.create. Any values supplied after the thread are returned as results from the coroutine.yield inside the thread.
- If this is the first call for this thread, the values are supplied to the function itself.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### coroutine.running(): thread

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
coroutine.running(): thread
</code>

- Returns the running coroutine, or no value when called by the main thread.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### coroutine.status(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
coroutine.status(): string
</code>

- Returns a string indicating the status of the thread.
- Raises an error if the argument is not a thread.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### coroutine.wrap(f: function): function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
coroutine.wrap(f: function): function
</code>

- Creates a thread with body f, and then returns a function that can be used to resume the thread.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### coroutine.yield(...: any): ...any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
coroutine.yield(...: any): ...any
</code>

- Yields execution back to the caller, effectively creating co-operative multi-tasking, values supplied to yield are returned to coroutine.resume.
- The coroutine cannot be running a C function, a metamethod, or an iterator.

<div hidden>

```ts

```

</div>
