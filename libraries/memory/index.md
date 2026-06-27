# memory
Memory is a direct access library to reading/writing into memory.

!!!danger Dev-Locked
Only developers can access this library due to the risks.\
Also we are adding more functionality to this, such as disassemblers.
!!!

---
## memory.module
```ts
{
    name: string,
    address: memory.address,
    base: memory.address,
    size: number
}
```

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.address(value: number | string | function | userdata): memory.address

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.address(value: number | string | function | userdata): memory.address
</code>

- Creates a new address class.
- Using a string will attempt for format a hex-string to address.
- Using cfunctions or userdata retrives their absolute location in memory.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.module(name?: string): memory.module

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.module(name?: string): memory.module
</code>

- Attempts to retreive a loaded module.
- Windows are usually named .dll, while linux are .so

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.modules(): memory.module[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.modules(): memory.module[]
</code>

- Lists all modules that has been loaded.
- Windows are usually named .dll, while linux are .so

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.base(addr: memory.address): memory.module?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.base(addr: memory.address): memory.module?
</code>

- Attempts to locate the base module based on the address.
- This only works if the address with within the address-space of a module.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.fetch(module: memory.module, name: string): memory.address

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.fetch(module: memory.module, name: string): memory.address
</code>

- Attempts to search for existing routines or variables that are disclosed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.interface(module: memory.module, name: string): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.interface(module: memory.module, name: string): memory.address?
</code>

- Attempt to search for various interface routines & calls them.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.index(input: memory.address, index: number): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.index(input: memory.address, index: number): memory.address?
</code>

- Performs a simple indexing on an address.
- This equates to simply `((void**)input)[index]`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.offset(input: memory.address, offset: number): memory.address

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.offset(input: memory.address, offset: number): memory.address
</code>

- Performs a simple offset to an address
- This equates to simply `(void*)input + offset`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.relative(input: memory.address, offset: number, size: number): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.relative(input: memory.address, offset: number, size: number): memory.address?
</code>

- Performs a relative instruction operation.
- For windows-x64-intel this peaks into a subroutine using "call" opcode -> `memory.relative(addr, 0x1, 0x5)`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.vtable(input: memory.address): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.vtable(input: memory.address): memory.address?
</code>

- Performs a de-reference to a class for it's vtable.
- This equates to simply `*reinterpret_cast<void***>(address)`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.bool(input: memory.address): boolean?

</div>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.aob.hex(module: memory.module, pattern: string): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.aob.hex(module: memory.module, pattern: string): memory.address?
</code>

- Performs a hex-style signature scan on a module.
- Example: `\xA0?\xB1`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.aob.ida(module: memory.module, pattern: string): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.aob.ida(module: memory.module, pattern: string): memory.address?
</code>

- Performs a ida-style signature scan on a module.
- Example: `A0 ? B1`

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.bool(input: memory.address): boolean?
</code>

- Attempts to read a `boolean` value.
- Typically the size of a boolean is defined as 1 bit.
- However some systems differ claiming 1 byte or 8 bits.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.char(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.char(input: memory.address): number?
</code>

- Attempts to read a `char` value.
- Size: 1 Byte - 8 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.uchar(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.uchar(input: memory.address): number?
</code>

- Attempts to read a `unsigned char` value.
- Size: 1 Byte - 8 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.short(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.short(input: memory.address): number?
</code>

- Attempts to read a `short` value.
- Size: 2 Bytes - 16 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.ushort(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.ushort(input: memory.address): number?
</code>

- Attempts to read a `unsigned short` value.
- Size: 2 Bytes - 16 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.int(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.int(input: memory.address): number?
</code>

- Attempts to read a `int` value.
- Size: 4 Bytes - 32 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.uint(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.uint(input: memory.address): number?
</code>

- Attempts to read a `unsigned int` value.
- Size: 4 Bytes - 32 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.long(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.long(input: memory.address): number?
</code>

- Attempts to read a `long` value.
- Size: 4 Bytes - 32 Bits (Win) | 8 Bytes - 64 Bits (Linux)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.ulong(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.ulong(input: memory.address): number?
</code>

- Attempts to read a `unsigned long` value.
- Size: 4 Bytes - 32 Bits (Win) | 8 Bytes - 64 Bits (Linux)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.float(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.float(input: memory.address): number?
</code>

- Attempts to read a `float` value.
- Size: 4 Bytes - 32 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.double(input: memory.address): number?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.double(input: memory.address): number?
</code>

- Attempts to read a `double` value.
- Size: 8 Bytes - 64 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.sequence(input: memory.address, size: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.sequence(input: memory.address, size: number): string
</code>

- Attempts to read a sequence of bytes.
- Example returns: `A1 B2 C3`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.read.address(input: memory.address): memory.address?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.read.address(input: memory.address): memory.address?
</code>

- Attempts to read a `void*` value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.bool(input: memory.address, value: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.bool(input: memory.address, value: boolean)
</code>

- Attempts to write a `boolean` value.
- Typically the size of a boolean is defined as 1 bit.
- However some systems differ claiming 1 byte or 8 bits.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.char(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.char(input: memory.address, value: number)
</code>

- Attempts to write a `char` value.
- Size: 1 Byte - 8 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.uchar(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.uchar(input: memory.address, value: number)
</code>

- Attempts to write a `unsigned char` value.
- Size: 1 Byte - 8 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.short(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.short(input: memory.address, value: number)
</code>

- Attempts to write a `short` value.
- Size: 2 Bytes - 16 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.ushort(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.ushort(input: memory.address, value: number)
</code>

- Attempts to write a `unsigned short` value.
- Size: 2 Bytes - 16 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.int(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.int(input: memory.address, value: number)
</code>

- Attempts to write a `int` value.
- Size: 4 Bytes - 32 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.uint(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.uint(input: memory.address, value: number)
</code>

- Attempts to write a `unsigned int` value.
- Size: 4 Bytes - 32 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.long(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.long(input: memory.address, value: number)
</code>

- Attempts to write a `long` value.
- Size: 4 Bytes - 32 Bits (Win) | 8 Bytes - 64 Bits (Linux)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.ulong(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.ulong(input: memory.address, value: number)
</code>

- Attempts to write a `unsigned long` value.
- Size: 4 Bytes - 32 Bits (Win) | 8 Bytes - 64 Bits (Linux)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.float(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.float(input: memory.address, value: number)
</code>

- Attempts to write a `float` value.
- Size: 4 Bytes - 32 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.double(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.double(input: memory.address, value: number)
</code>

- Attempts to write a `double` value.
- Size: 8 Bytes - 64 Bits

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.sequence(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.sequence(input: memory.address, value: string, size: number)
</code>

- Attempts to write a sequence of bytes to the address.
- Example sequences that are valid: `A1 B2 C3` or `A1B2C3`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### memory.write.address(input: memory.address, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
memory.write.address(input: memory.address, value: memory.address)
</code>

- Attempts to write a `address` value.
<div hidden>

```ts

```

</div>
