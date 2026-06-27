# bit
This is an expansion to the existing Lua Bit library.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.arshift(v: number, count: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.arshift(v: number, count: number): number
</code>

- Returns the arithmetically shifted value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.band(...: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.band(...: number): number
</code>

- Performs the bitwise and for all values specified.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.bnot(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.bnot(v: number): number
</code>

- Returns the bitwise not of the value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.bor(...: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.bor(...: number): number
</code>

- Returns the bitwise OR of all values specified.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.bswap(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.bswap(v: number): number
</code>

- Swaps the byte order.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.bxor(v: number, other?: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.bxor(v: number, other?: number): number
</code>

- Returns the bitwise xor of all values specified.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.lshift(v: number, count: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.lshift(v: number, count: number): number
</code>

- Returns the left shifted value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.rol(v: number, count: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.rol(v: number, count: number): number
</code>

- Returns the left rotated value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.ror(v: number, count: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.ror(v: number, count: number): number
</code>

- Returns the right rotated value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.rshift(v: number, count: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.rshift(v: number, count: number): number
</code>

- Returns the right shifted value.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.tobit(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.tobit(v: number): number
</code>

- Normalizes the specified value and clamps it in the range of a signed 32bit integer.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### bit.tohex(v: number, chars: number = 8): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
bit.tohex(v: number, chars: number = 8): string
</code>

- Returns the hexadecimal representation of the number with the specified number of characters.

<div hidden>

```ts

```

</div>
