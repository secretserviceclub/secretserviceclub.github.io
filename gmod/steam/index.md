# steam
Modifications & tools to the Steam client.

---
## Invites

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.invite_friend(steamid64: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.invite_friend(steamid64: string)
</code>

- Sends a game invite to the specified SteamID64.

---
## Name

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.set_name(name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.set_name(name: string)
</code>

- Allows you to set **your steam name** to a specified one.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.get_name(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.get_name(): string
</code>

- Gets the current steam name of your account

---
## IDs

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.get_id64(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.get_id64(): string
</code>

- Gets the SteamID64 of your account

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.get_id3(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.get_id3(): string
</code>

- Gets the SteamID3 of your account

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.get_id(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.get_id(): string
</code>

- Gets the SteamID of your account

---
## Achievements

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.award_achievement(achievement_id: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.award_achievement(achievement_id: number)
</code>

- Awards the specified achievement id.

```lua
secret.steam.award_achievement(10) -- unlock the garry achievement, you can also spam this.
```

---
## Presence

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### steam.set_presence(type: string, value?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
steam.set_presence(type?: string, value?: string)
</code>

- Changes the game activity on your profile.
- Not providing anything for `type` clears all presence.

```lua
-- Generic allows you to modify things freely without localizations
-- use https://steamcommunity.com/dev/testrichpresence to test it out!
steam.set_presence("steam_display", "#Status_Generic")
steam.set_presence("status", "daz is cool")
steam.set_presence("generic", "daz is cool")
steam.set_presence("connect", "+connect 0.0.0.0:10000")
```

<div hidden>

```ts

```

</div>
