# entities
Access players and controllers in the entity list.

---

Do note that you should call `:valid()` after a map change.

---
## Lookup

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.get(index: number): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.get(index: number): entity | nil
</code>

- Returns the entity at the given index.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.max_index(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.max_index(): number
</code>

- Returns the highest entity index.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.for_each_player(callback: (ent: entity) => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.for_each_player(callback: (ent: entity) => void)
</code>

- Iterates every player pawn.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.for_each_controller(callback: (ent: entity) => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.for_each_controller(callback: (ent: entity) => void)
</code>

- Iterates every player controller.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.for_each(callback: (ent: entity) => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.for_each(callback: (ent: entity) => void)
</code>

- Iterates every valid entity index.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.for_each_class(class_name: string, callback: (ent: entity) => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.for_each_class(class_name: string, callback: (ent: entity) => void)
</code>

- Iterates entities whose schema class name matches exactly (e.g. `C_SmokeGrenadeProjectile`).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.for_each_weapon(callback: (ent: entity) => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.for_each_weapon(callback: (ent: entity) => void)
</code>

- Iterates world weapon entities.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entities.for_each_projectile(callback: (ent: entity) => void)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entities.for_each_projectile(callback: (ent: entity) => void)
</code>

- Iterates grenade / projectile entities.

```lua
secret.entities.for_each_player(function(ent)
    if not ent:valid() or not ent:alive() then return end
    if ent:is_enemy() then
        print(ent:name(), ent:health())
    end
end)
```

---
## Entity

Methods on entity userdata. Pawn and controller resolve through each other where needed (`:pawn()`, `:controller()`, `:name()`, etc).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:valid(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:valid(): boolean
</code>

- Returns if the entity is still valid.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:handle(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:handle(): number
</code>

- Returns the entity handle.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:index(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:index(): number
</code>

- Returns the entity index used by `entities.get`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:origin(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:origin(): number, number, number
</code>

- Returns origin as `x, y, z`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:eye_pos(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:eye_pos(): number, number, number
</code>

- Returns eye position as `x, y, z`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:velocity(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:velocity(): number, number, number
</code>

- Returns velocity as `x, y, z`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:is_player(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:is_player(): boolean
entity:is_controller(): boolean
entity:is_weapon(): boolean
entity:is_projectile(): boolean
entity:is_bomb(): boolean
</code>

- Type checks for common entity kinds.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:health(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:health(): number | nil
</code>

- Returns health.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:armor(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:armor(): number | nil
</code>

- Returns armor.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:has_helmet(): boolean | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:has_helmet(): boolean | nil
</code>

- Returns if the player has a helmet.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:team(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:team(): number | nil
</code>

- Returns the team number.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:alive(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:alive(): boolean
</code>

- Returns if the player is alive.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:name(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:name(): string | nil
</code>

- Returns the player name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:is_enemy(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:is_enemy(): boolean
</code>

- Returns if the player is an enemy.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:is_teammate(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:is_teammate(): boolean
</code>

- Returns if the player is a teammate.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:is_local(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:is_local(): boolean
</code>

- Returns if this is the local player.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:steam_id64(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:steam_id64(): string | nil
</code>

- Returns the SteamID64.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:pawn(): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:pawn(): entity | nil
</code>

- Returns the linked pawn from a controller.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:controller(): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:controller(): entity | nil
</code>

- Returns the linked controller from a pawn.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:flags(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:flags(): number | nil
</code>

- Returns entity flags.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:dormant(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:dormant(): boolean
</code>

- Returns if the entity is dormant.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:money(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:money(): number | nil
</code>

- Returns account money.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:weapon(): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:weapon(): entity | nil
</code>

- Returns the active weapon entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:weapon_name(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:weapon_name(): string | nil
</code>

- Returns the active weapon name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:clip(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:clip(): number | nil
</code>

- Returns ammo in the clip.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:scoped(): boolean | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:scoped(): boolean | nil
</code>

- Returns if the player is scoped.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:flash_duration(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:flash_duration(): number | nil
</code>

- Returns flashbang duration.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:class_name(): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:class_name(): string | nil
</code>

- Returns the schema class name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:weapons(): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:weapons(): table
</code>

- Returns a 1-based list of weapon entities from weapon services.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:observer_target(): entity | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:observer_target(): entity | nil
</code>

- Returns the current observer target.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:observer_mode(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:observer_mode(): number | nil
</code>

- Returns the observer mode.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:hitbox_center(index: number): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:hitbox_center(index: number): number, number, number
</code>

- Returns hitbox / bone center as `x, y, z`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:bone_pos(index: number): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:bone_pos(index: number): number, number, number
</code>

- Returns bone position as `x, y, z`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:bone_count(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:bone_count(): number
</code>

- Returns the bone count.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:eye_angles(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:eye_angles(): number, number, number
</code>

- Returns eye angles as `pitch, yaw, roll`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:aim_punch(): number, number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:aim_punch(): number, number, number
</code>

- Returns aim punch as `pitch, yaw, roll`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:visible(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:visible(): boolean
</code>

- Returns if the player is visible to the local player (eye-to-eye trace).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:can_shoot(tick?: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:can_shoot(tick?: number): boolean
</code>

- Returns if the pawn can fire its active weapon. Optional `tick` defaults to the controller tickbase.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:inaccuracy(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:inaccuracy(): number | nil
</code>

- Returns weapon inaccuracy. Works on a pawn (active weapon) or a weapon entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:spread(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:spread(): number | nil
</code>

- Returns weapon spread. Works on a pawn or weapon entity.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:weapon_type(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:weapon_type(): number | nil
</code>

- Returns `EWeaponType` (knife, pistol, rifle, …).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:def_index(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:def_index(): number | nil
</code>

- Returns the item definition index.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:max_speed(): number | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:max_speed(): number | nil
</code>

- Returns weapon max speed, or pawn max speed if not a weapon.

---

## Schema

Read / write schema fields by name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:get(field: string, ...): any | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:get(field: string, ...): any | nil
</code>

- Returns a schema field value, or `nil` if missing / unsupported.
- Prefer `"ClassName->field"` (e.g. `"C_BaseEntity->m_iHealth"`). Bare names only resolve when the field is declared on the entity's own class.
- Extra string args follow pointer fields (e.g. `ent:get("C_BaseEntity->m_pCollision", "m_vecMins")`).
- Vectors / angles return `{ x, y, z }`. Colors return `{ r, g, b, a }`. Pointers / handles return numbers.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### entity:set(field: string, ..., value: any): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
entity:set(field: string, ..., value: any): boolean
</code>

- Sets a schema field. Last argument is the value. Returns `true` on success.
- Same naming rules as `get`. Use `"ClassName->field"` for inherited fields.
- Vector values accept `{ x, y, z }` or `{ 1, 2, 3 }`.

```lua
local me = secret.game.local_player()
if me and me:valid() then
    print(me:get("C_BaseEntity->m_iHealth"))
    me:set("C_BaseEntity->m_iHealth", 50)
    PrintTable(me:get("C_BaseEntity->m_pCollision", "m_vecMins"))
end
```

```lua
local me = secret.game.local_player()
if me and me:valid() then
    print(me:name(), me:money(), me:weapon_name())
end
```

<div hidden>

```ts

```

</div>
