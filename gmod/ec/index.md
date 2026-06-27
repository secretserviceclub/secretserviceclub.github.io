# ec
Allows you to create and access an external console for various purposes.

---
## Window

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.open()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.open()
</code>

- Opens the console window, allowing you to see messages.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.close()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.close()
</code>

- Closes the console window.
- No messages will be processed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.active(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.active(): boolean
</code>

- Checks if the console window is currently active.

---
## Title

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.title(name: string?): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.title(name: string?): string?
</code>

- Sets the current title of the console window.
- If no input is given, returns the current window title.

---
## Output

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.message(input: any...)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.message(input: any...)
</code>

- Creates a message to the console window.
- Giving it a color will also change the text color.
- Do note that colors are limited.

---
## Commands

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.add(name: string, callback: function(args: string[], args_str: string, cmd: string))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.add(name: string, callback: function(args: string[], args_str: string, cmd: string))
</code>

- Adds a command callback to the external console.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ec.remove(name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ec.remove(name: string)
</code>

- Removes a command callback by name.
<div hidden>

```ts

```

</div>
