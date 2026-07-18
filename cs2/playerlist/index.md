# playerlist
Check if players are Secret Service users.

---
## Secret users

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.is_secret_user(steamid64: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.is_secret_user(steamid64: string): boolean
</code>

- Returns if the given SteamID64 is a Secret user.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.get_secret_username(steamid64: string): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.get_secret_username(steamid64: string): string | nil
</code>

- Returns the Secret username for the given SteamID64.

```lua
secret.entities.for_each_controller(function(ctrl)
    local sid = ctrl:steam_id64()
    if sid and secret.playerlist.is_secret_user(sid) then
        print(ctrl:name(), secret.playerlist.get_secret_username(sid))
    end
end)
```

<div hidden>

```ts

```

</div>
