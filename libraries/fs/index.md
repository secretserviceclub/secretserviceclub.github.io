# fs
File system access with restrictions & canonical resolution.\
This one allows the use of "..", without breaching the workspace.

!!!warning Environment Risks
For best security, we recommend you do not run this in a `lua_State`
that could compromise you by a bad actor.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.read(path: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.read(path: string): string
</code>

- Reads a file from a given path

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.write(path: string, data: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.write(path: string, data: string)
</code>

- Writes to a file provided by the path

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.isfile(path: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.isfile(path: string): boolean
</code>

- Checks if a filesystem object is a file

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.isfolder(path: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.isfolder(path: string): boolean
</code>

- Checks if a filesystem object is a folder

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.listfiles(path: string): string[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.listfiles(path: string): string[]
</code>

- Lists files in the specified path

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.makefolder(path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.makefolder(path: string)
</code>

- Creates a folder in the specified path
- This is recursive, allowing it to generate multiple folders

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.delfolder(path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.delfolder(path: string)
</code>

- Deletes a folder from the specified path

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.delfile(path: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.delfile(path: string)
</code>

- Deletes a file from the specified path

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.append(path: string, data: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.append(path: string, data: string)
</code>

- Appends data onto the specified file

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.forward(path: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.forward(path: string): string
</code>

- Changes all "\\" separators to "/"

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.backward(path: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.backward(path: string): string
</code>

- Changes all "/" separators to "\\"

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.join(a: string, b: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.join(a: string, b: string): string
</code>

- Joins two paths together

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.extname(path: string, replace?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.extname(path: string, replace?: string): string
</code>

- Gets the extension name of a path
- If provided a replacement, will return the replaced path's extension

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.filename(path: string, replace?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.filename(path: string, replace?: string): string
</code>

- Gets the file name of a path
- If provided a replacement, will return the replaced path's file

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.dirname(path: string, replace?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.dirname(path: string, replace?: string): string
</code>

- Gets the directory name of a path
- If provided a replacement, will return the replaced path's directory

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### fs.sanitize(path: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
fs.sanitize(path: string): string
</code>

- Removes any oddities in the path, replacing them with "_" instead.

<div hidden>

```ts

```

</div>
