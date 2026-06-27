# playerlist
Manages players in your current game session.

---
## Friends

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.add_friend(steamid64: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.add_friend(steamid64: string)
</code>

- Adds a specified SteamID64 to the friend list.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.remove_friend(steamid64: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.remove_friend(steamid64: string)
</code>

- Removes a specified SteamID64 from the friend list.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.is_friend(steamid64: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.is_friend(steamid64: string): boolean
</code>

- Checks if the specified SteamID64 is in the friend list and returns `true` if the player is a friend, otherwise `false`.

---
## Priority

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.add_priority(steamid64: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.add_priority(steamid64: string)
</code>

- Adds a specified SteamID64 to the priority list.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.remove_priority(steamid64: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.remove_priority(steamid64: string)
</code>

- Removes a specified SteamID64 from the priority list.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.is_priority(steamid64: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.is_priority(steamid64: string): boolean
</code>

- Checks if the specified SteamID64 is in the priority list and returns `true` if the player is on the priority list, otherwise `false`.

---
## Secret user

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.is_secret_user(steamid64: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.is_secret_user(steamid64: string): boolean
</code>

- Returns `true` if the specified SteamID64 is a secret user (anon mode off), otherwise `false`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### playerlist.get_secret_username(steamid64: string): string | nil

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
playerlist.get_secret_username(steamid64: string): string | nil
</code>

- Returns the secret username for the specified SteamID64. Returns `nil` if the user is not connected or is anonymous.
<div hidden>

```ts

```

</div>
