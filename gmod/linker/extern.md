# extern
These are functions that are ported to allow for easy access.\
This makes it easier to use instead of just relying on<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.meta(library: string, name?: string): function | table
</code>and<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.global(library: string, name?: string): function | table
</code>

---

## Example
This is an example of how you can use ported functions.\
With this you can run it interstate.

```lua
-- lua_run util.AddNetworkString("test") net.Receive("test", function() print(net.ReadString()) end)
linker.net.Start("test")
linker.net.WriteString("hello world")
linker.net.SendToServer() -- prints "hello world" on the server
```

---
## NET
You can access this by doing<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.net.*
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.GetList(): string[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.GetList(): string[]
</code>

- Retrieves a list of all network names

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.IDToString(id: number): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.IDToString(id: number): string?
</code>

- Converts a network ID to its string counterpart

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.StringToID(name: string): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.StringToID(name: string): number?
</code>

- Converts a network name to its ID counterpart

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.Start(messageName: string, unreliable?: boolean = false)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.Start(messageName: string, unreliable?: boolean = false)
</code>

- Begins a new net message.
- If another net message is already started and hasn't been sent yet, it will be discarded.
- After calling this function, you will want to call `net.Write*` functions to write your data, if any, and then finish with<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.SendToServer()
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.SendToServer()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.SendToServer()
</code>

- Sends the current net message to the server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteBit(boolean: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteBit(boolean: boolean)
</code>

- Appends a boolean (as 1 or 0) to the current net message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteUInt(value: number, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteUInt(value: number, size: number)
</code>

- Appends an unsigned integer with the specified number of bits to the current net message.
- For size reference: `1 = bit, 4 = nibble, 8 = byte, 16 = short, 32 = long`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteInt(value: number, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteInt(value: number, size: number)
</code>

- Appends an integer with the specified number of bits to the current net message.
- For size reference: `1 = bit, 4 = nibble, 8 = byte, 16 = short, 32 = long`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteString(value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteString(value: string)
</code>

- Appends a string to the current net message.
- The size of the written data is 8 bits for every ASCII character in the string + 8 bits for the null terminator.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteFloat(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteFloat(value: number)
</code>

- Appends a float (number with decimals) to the current net message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteDouble(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteDouble(value: number)
</code>

- Appends a double (number with decimals) to the current net message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteVector(value: Vector)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteVector(value: Vector)
</code>

- Appends a vector to the current net message.
- Vectors sent by this function are compressed, which may result in precision loss.
- XYZ components greater than 16384 or less than -16384 are irrecoverably altered (most significant bits are trimmed) and precision after the decimal point is low.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteAngle(value: Angle)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteAngle(value: Angle)
</code>

- Similar to<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteVector(value: Vector)
</code>however uses a different lua class to inherit Angle metatables

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteMatrix(value: Matrix) 

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteMatrix(value: Matrix) 
</code>

- Writes a VMatrix to the current net message.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.WriteData(value: string, size: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.WriteData(value: string, size: number)
</code>

- Writes a chunk of binary data to the message.
- The size determines the length of the message, having a different size than the message size would cut-off or corrupt data.

## NW
You can access this by doing<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.nw.*
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetList(target: Entity): {[index: string]: any}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetList(target: Entity): {[index: string]: any}
</code>

- Retrieves a list of all keys and their data

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetBool(target: Entity, key: string, fallback?: any): boolean | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetBool(target: Entity, key: string, fallback?: any): boolean | any
</code>

- Retrieves a networked boolean value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetInt(target: Entity, key: string, fallback?: any): number | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetInt(target: Entity, key: string, fallback?: any): number | any
</code>

- Retrieves a networked integer (whole number) value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetFloat(target: Entity, key: string, fallback?: any): number | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetFloat(target: Entity, key: string, fallback?: any): number | any
</code>

- Retrieves a networked float value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetString(target: Entity, key: string, fallback?: any): string | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetString(target: Entity, key: string, fallback?: any): string | any
</code>

- Retrieves a networked string value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetVector(target: Entity, key: string, fallback?: any): Vector | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetVector(target: Entity, key: string, fallback?: any): Vector | any
</code>

- Retrieves a networked vector value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetAngle(target: Entity, key: string, fallback?: any): Angle | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetAngle(target: Entity, key: string, fallback?: any): Angle | any
</code>

- Retrieves a networked angle value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nw.GetEntity(target: Entity, key: string, fallback?: any): Entity | any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nw.GetEntity(target: Entity, key: string, fallback?: any): Entity | any
</code>

- Retrieves a networked entity value at specified index on the entity.

## NVAR
You can access this by doing<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
linker.nvar.*
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetBool(target: Entity, key: number): boolean | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetBool(target: Entity, key: number): boolean | nil
</code>

- Retrieves a networked boolean value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetInt(target: Entity, key: number): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetInt(target: Entity, key: number): number | nil
</code>

- Retrieves a networked integer (whole number) value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetFloat(target: Entity, key: number): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetFloat(target: Entity, key: number): number | nil
</code>

- Retrieves a networked float value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetString(target: Entity, key: number): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetString(target: Entity, key: number): string | nil
</code>

- Retrieves a networked string value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetVector(target: Entity, key: number): Vector | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetVector(target: Entity, key: number): Vector | nil
</code>

- Retrieves a networked vector value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetAngle(target: Entity, key: number): Angle | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetAngle(target: Entity, key: number): Angle | nil
</code>

- Retrieves a networked angle value at specified index on the entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### nvar.GetEntity(target: Entity, key: number): Entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
nvar.GetEntity(target: Entity, key: number): Entity | nil
</code>

- Retrieves a networked entity value at specified index on the entity.

<div hidden>

```ts

```

</div>
