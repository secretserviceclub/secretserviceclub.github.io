# console
Manages the cheat’s custom console: log messages, register commands that users can run from the console, and execute or list those commands from Lua.

---
## Logging

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### console.log(text: string, log_type: number, display_date: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
console.log(text: string, log_type: number, display_date: boolean)
</code>

-  Logs a message onto a custom console with the specified text and log type. 
- 0 = Success
- 1 = Warning
- 2 = Error
- 3 = Message
- 4 = Note

---
## Commands

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### console.add_command(name: string, description: string, func: function)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
console.add_command(name: string, description: string, func: function)
</code>

-  Creates a custom console command with the specified name and description, which executes the provided function when invoked.

```lua
secret.console.add_command("my_command", "This is a custom command", function(args)
    print("Received arguments:", args)
    secret.console.log("my_command executed!", 0, false)
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### console.remove_command(name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
console.remove_command(name: string)
</code>

-  Removes an existing custom console command with the specified name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### console.get_command_list(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
console.get_command_list(): table
</code>

-  Retrieves a list of available commands.

```lua
local commandList = secret.console.get_command_list()
for _, commandName in ipairs(commandList) do
    print(commandName) 
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### console.execute_command(name: string, args: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
console.execute_command(name: string, args: string)
</code>

-  Executes a command with the specified name and optional argument.

!!!warning
Currently only 1 argument is supported.
!!!
<div hidden>

```ts

```

</div>
