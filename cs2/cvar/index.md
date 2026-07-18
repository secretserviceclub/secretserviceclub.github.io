# cvar
Read and write engine convars.

---
## Get / set

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cvar.get(name: string): boolean | number | string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cvar.get(name: string): boolean | number | string | nil
</code>

- Returns the convar value, or `nil` if it was not found.
- Supports bool, int, float, and string types.

```lua
print(secret.cvar.get("sensitivity"))
print(secret.cvar.get("sv_cheats"))
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cvar.set(name: string, value: boolean | number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cvar.set(name: string, value: boolean | number): boolean
</code>

- Sets a bool / int / float convar.
- Returns `true` on success.

```lua
secret.cvar.set("sensitivity", 1.2)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### cvar.exists(name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
cvar.exists(name: string): boolean
</code>

- Returns if the convar exists.

```lua
if secret.cvar.exists("mp_teammates_are_enemies") then
    print(secret.cvar.get("mp_teammates_are_enemies"))
end
```

<div hidden>

```ts

```

</div>
