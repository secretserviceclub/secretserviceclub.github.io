# detour
Listeners, Blockers & Overrides for the Garry's Mod functions.\
These are C++ made detours using `linker`, providing you with a unique way of changing the behaviors of functions.\
This is not limited to the client-state, we have provided interstate capabilities.

---

## Example
These are special in a sense they directly hook and change features of Lua from C++, making them untraceable and highly capable of mimicing behaviors.

```lua
linker.listener.add("Player.ConCommand", "log", function(trace, command)
    if trace:find("cl_bad.lua") then
        print("cl_bad, ran " .. command)
    end
end)

linker.blocker.add("Player.ConCommand", "blockdis", function(trace, command)
    if trace:find("cl_bad.lua") then
        print("cl_bad tried to run", command)
        return true -- block command
    end
end)
  
linker.override.add("file.Exists", "overridedis", function(trace, filename, pathname)
    if trace:find("cl_bad.lua") then
        return false -- make file.Exists return false
    end
end)

linker.override.add("lua", "overridedis", function(trace, source_code, source_path)
   if source_path == "@anticheat.lua" then
        return 'print("disabled anticheat!")', source_path
   end
end)
```

---

## Lua

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lua(source_code: string, source_path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lua(trace: string, source_code: string, source_path: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `lua` not run.
- Override changes the returns of `lua`, you can use this to override the source code or source path.

---

## File

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Open(trace: string, file_name: string, file_mode: string, file_path: string): file_class

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Open(trace: string, file_name: string, file_mode: string, file_path: string): file_class
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Open` return a default value as specified on the Garry's Mod Wiki.
- Override changes the parameters passed into `file.Open`, not the returning values.

!!!warning Common Server Tracker
This function is commonly used by servers to track you.
!!!

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.AsyncRead(trace: string, file_name: string, file_path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.AsyncRead(trace: string, file_name: string, file_path: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.AsyncRead` return a default value as specified on the Garry's Mod Wiki.
- Override changes the parameters passed into `file.AsyncRead`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.CreateDir(trace: string, file_name: string, file_path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.CreateDir(trace: string, file_name: string, file_path: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.CreateDir` not do anything.
- Override changes the parameters passed into `file.CreateDir`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Delete(trace: string, file_name: string, file_path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Delete(trace: string, file_name: string, file_path: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Delete` not do anything.
- Override changes the parameters passed into `file.Delete`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Exists(trace: string, file_name: string, file_path: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Exists(trace: string, file_name: string, file_path: string): boolean
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Exists` return a default value as specified on the Garry's Mod Wiki.
- Override changes the returns of `file.Exists`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.IsDir(trace: string, file_name: string, file_path: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.IsDir(trace: string, file_name: string, file_path: string): boolean
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.IsDir` return a default value as specified on the Garry's Mod Wiki.
- Override changes the returns of `file.IsDir`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Rename(trace: string, file_target: string, file_new: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Rename(trace: string, file_target: string, file_new: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Rename` not do anything.
- Override changes the parameters passed into `file.Rename`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Size(trace: string, file_name: string, file_path: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Size(trace: string, file_name: string, file_path: string): number
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Size` return a default value as specified on the Garry's Mod Wiki.
- Override changes the returns of `file.Size`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Time(trace: string, file_name: string, file_path: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Time(trace: string, file_name: string, file_path: string): number
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Time` return a default value as specified on the Garry's Mod Wiki.
- Override changes the returns of `file.Time`.

!!!warning Common Server Tracker
This function is commonly used by servers to track you.
!!!

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Find(trace: string, file_name: string, file_path: string): string[]?, string[]?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Find(trace: string, file_name: string, file_path: string): string[]?, string[]?
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Find` return a default value as specified on the Garry's Mod Wiki.
- Override changes the parameters passed into `file.Find`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### file.Scan(trace: string, file_name: string, file_path: string, is_folder: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
file.Scan(trace: string, file_name: string, file_path: string, is_folder: boolean)
</code>

- A special event tied to `file.Find`, used to change the individual values returned from the array collection.
- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `file.Scan` not pass the value into the table for `file.Find`.
- Override changes the value being pushed into `file.Find` array collections.

---
## Net
<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.Start(trace: string, net_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.Start(trace: string, net_name: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.Start`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.SendToServer(trace: string, net_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.SendToServer(trace: string, net_name: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>
- Blocker forces the network message to be dropped if you return true.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.Abort(trace: string, net_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.Abort(trace: string, net_name: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>
- Blocker prevents network messages from being dropped, unaffected by blocker from<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.SendToServer(trace: string, net_name: string)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadHeader(trace: string, net_name: string, bytes: number, bits: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadHeader(trace: string, net_name: string, bytes: number, bits: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>
- This is called when a net-message is incoming and about to be read.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.Receive(channel: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.Receive(channel: string)
</code>

- Blocker event name only, Garry's Mod implements `net.Receive` in Lua, so this is not a direct C detour target.
- The events usable by this blocker event is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.Received(trace: string, net_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.Received(trace: string, net_name: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>
- This is called after a network message has been fully processed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteBit(trace: string, net_name: string, value: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteBit(trace: string, net_name: string, value: boolean)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteBit`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteUInt(trace: string, net_name: string, value: number, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteUInt(trace: string, net_name: string, value: number, size: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteUInt`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteInt(trace: string, net_name: string, value: number, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteInt(trace: string, net_name: string, value: number, size: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteInt`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteString(trace: string, net_name: string, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteString(trace: string, net_name: string, value: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteString`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteFloat(trace: string, net_name: string, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteFloat(trace: string, net_name: string, value: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteFloat`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteDouble(trace: string, net_name: string, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteDouble(trace: string, net_name: string, value: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteDouble`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteVector(trace: string, net_name: string, value: Vector)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteVector(trace: string, net_name: string, value: Vector)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteVector`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteAngle(trace: string, net_name: string, value: Angle)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteAngle(trace: string, net_name: string, value: Angle)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteAngle`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteMatrix(trace: string, net_name: string, value: Matrix)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteMatrix(trace: string, net_name: string, value: Matrix)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteMatrix`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteData(trace: string, net_name: string, value: string, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteData(trace: string, net_name: string, value: string, size: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the parameters passed into `net.WriteData`, not the returning values.
- For overriding make sure you provide the correct size in the return, it could corrupt your message in transport.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadBit(trace: string, net_name: string, value: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadBit(trace: string, net_name: string, value: boolean)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadBit`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadUInt(trace: string, net_name: string, value: number, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadUInt(trace: string, net_name: string, value: number, size: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadUInt`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadInt(trace: string, net_name: string, value: number, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadInt(trace: string, net_name: string, value: number, size: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadInt`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadString(trace: string, net_name: string, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadString(trace: string, net_name: string, value: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadString`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadFloat(trace: string, net_name: string, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadFloat(trace: string, net_name: string, value: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadFloat`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadDouble(trace: string, net_name: string, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadDouble(trace: string, net_name: string, value: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadDouble`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadVector(trace: string, net_name: string, value: Vector)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadVector(trace: string, net_name: string, value: Vector)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>
- Due to methods of data transfer, override is disabled for this function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadAngle(trace: string, net_name: string, value: Angle)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadAngle(trace: string, net_name: string, value: Angle)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>
- Due to methods of data transfer, override is disabled for this function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadMatrix(trace: string, net_name: string, value: Matrix)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadMatrix(trace: string, net_name: string, value: Matrix)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>
- Due to methods of data transfer, override is disabled for this function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.ReadData(trace: string, net_name: string, value: string, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.ReadData(trace: string, net_name: string, value: string, size: number)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Override changes the returns of `net.ReadData`.

---
## Command

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### RunConsoleCommand(trace: string, ...: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
RunConsoleCommand(trace: string, ...: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `RunConsoleCommand` not do anything.
- Override changes the parameters passed into `RunConsoleCommand`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### Player.ConCommand(trace: string, command: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
Player.ConCommand(trace: string, command: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `Player.ConCommand` not do anything.
- Override changes the parameters passed into `Player.ConCommand`, not the returning values.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### AddConsoleCommand(trace: string, command: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
AddConsoleCommand(trace: string, command: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `AddConsoleCommand` not do anything.
- Override changes the parameters passed into `AddConsoleCommand`, not the returning values.

---
## Engine

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### engine.WriteDupe(trace: string, name: string, data: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
engine.WriteDupe(trace: string, name: string, data: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `engine.WriteDupe` not do anything.
- Override changes the parameters passed into `engine.WriteDupe`, not the returning values.

!!!warning Common Server Tracker
This function is commonly used by servers to track you.
!!!

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### engine.OpenDupe(trace: string, path: string, data: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
engine.OpenDupe(trace: string, path: string, data: string): string
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `engine.OpenDupe` not do anything.
- Override changes the returns of `engine.OpenDupe`, specifically the JSON'ed dupe data.

!!!warning Common Server Tracker
This function is commonly used by servers to track you.
!!!

---
## SQL

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### sql.Query(trace: string, query: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
sql.Query(trace: string, query: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>
- Blocker will make `sql.Query` return a default value as specified on the Garry's Mod Wiki.
- Override changes the parameters passed into `sql.Query`, not the returning values.

!!!warning Common Server Tracker
This function is commonly used by servers to track you.
!!!

---
## CVAR

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### CreateConVar(trace: string, name: string, default?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
CreateConVar(trace: string, name: string, default?: string)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>

!!!warning Common Server Tracker
This function is commonly used by servers to track you.
!!!

---
## HTTP

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### HTTP(trace: string, payload: http_data)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
HTTP(trace: string, payload: http_data)
</code>

- The events usable by this function is<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.listener.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.blocker.*
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.override.*
</code>

```ts
http_data {
    url: string,
    method: string,
    body?: string,
    type?: string,
    headers: {[index: string]: string},
    parameters: {[index: string]: string}
}
```

- Blocker will make `HTTP` not do anything.
- Override changes the parameters passed into `HTTP`, not the returning values.

---
## Presets
!!!danger Dev-Locked
We are deciding the best approach for implementations.
!!!

<div hidden>

```ts

```

</div>
