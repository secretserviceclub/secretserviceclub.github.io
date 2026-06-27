# lxz
LXZ is a library with an amalgamation of several compression libraries, including LZMA, ZLIB, ZSTD and more.\
You can view more about them on their github: [!ref target="blank" text="bxzstr Github"](https://github.com/tmaklin/bxzstr)

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.encode.z(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.encode.z(input: string, async?: function(output: string)): string?
</code>

- Compresses the input string using ZLIB compression.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.encode.zstd(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.encode.zstd(input: string, async?: function(output: string)): string?
</code>

- Compresses the input string using Zstandard (ZSTD) compression.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.encode.bz2(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.encode.bz2(input: string, async?: function(output: string)): string?
</code>

- Compresses the input string using Bzip2 (BZ2) compression.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.encode.lzma(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.encode.lzma(input: string, async?: function(output: string)): string?
</code>

- Compresses the input string using LZMA (Lempel-Ziv-Markov chain algorithm).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.encode.glzma(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.encode.glzma(input: string, async?: function(output: string)): string?
</code>

- Compresses the input string using Garry's LZMA.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.decode.z(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.decode.z(input: string, async?: function(output: string)): string?
</code>

- Decompresses a ZLIB-compressed string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.decode.zstd(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.decode.zstd(input: string, async?: function(output: string)): string?
</code>

- Decompresses a Zstandard (ZSTD) compressed string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.decode.bz2(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.decode.bz2(input: string, async?: function(output: string)): string?
</code>

- Decompresses a Bzip2 (BZ2) compressed string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.decode.lzma(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.decode.lzma(input: string, async?: function(output: string)): string?
</code>

- Decompresses an LZMA-compressed string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### lxz.decode.glzma(input: string, async?: function(output: string)): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
lxz.decode.glzma(input: string, async?: function(output: string)): string?
</code>

- Decompresses a Garry's LZMA-compressed string.

<div hidden>

```ts

```

</div>
