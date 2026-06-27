# net
Network manipulation and exploitation.

---
## Packets & choking

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.bsendpacket(state: boolean?): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.bsendpacket(state: boolean?): boolean
</code>

- Controls whether the Source engine sends movement packets. Returns the previous state. Omit the argument to only read the current state.

```lua
local was = secret.net.bsendpacket(false) -- stop sending packets
secret.net.bsendpacket(was)               -- restore
local current = secret.net.bsendpacket()  -- read only
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.choked(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.choked(): number
</code>

- Number of movement commands currently choked (not yet sent).

```lua
local n = secret.net.choked()
print("Choked commands:", n)
```

---
## CVars & disconnect

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.setcvar(cvar: string, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.setcvar(cvar: string, value: string)
</code>

- Allows you to set a network variable (cvar) to a specified value.

```lua
secret.net.setcvar("name", "secretservice agent")
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.disconnect(reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.disconnect(reason: string)
</code>

- Allows you to disconnect from a server with a custom disconnect reason.

```lua
secret.net.disconnect("Leaving")
```

---
## Commands

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.stringcmd(cmd: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.stringcmd(cmd: string)
</code>

- Allows to send a string command from the client to the server.

```lua
secret.net.stringcmd("retry")
```

---
## Source net messages

Low-level API for building and sending Source engine net messages directly.\
Use this when you need full control over message layout, bit widths, or message types that the high-level helpers do not cover.

Most messages follow the same layout: set the message type for `transmit`, write the 6-bit header with `write_uint`, then write the payload.

**String command** (`string_cmd`)

```lua
local buf = secret.net.packet(4096)
buf:set_type(secret.net.msg.string_cmd)
buf:write_uint(secret.net.msg.string_cmd, secret.net.header_bits)
buf:write_str("status")
local ok = buf:transmit() -- false if not connected
```

**Set convar** (`set_convar`) — low-level equivalent of `net.setcvar`

```lua
local buf = secret.net.packet(4096)
buf:set_type(secret.net.msg.set_convar)
buf:write_uint(secret.net.msg.set_convar, secret.net.header_bits)
buf:write_u8(1)              -- number of cvars being sent
buf:write_str("name")
buf:write_str("My New Name")
buf:transmit()
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.packet(capacity: number, msg_type?: number): net.packet

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.packet(capacity: number, msg_type?: number): net.packet
</code>

- Creates a writable net message buffer.
- `capacity` must be between `4` and `65536`. The buffer is rounded up to at least 4 bytes and aligned to a 4-byte boundary.
- Optional `msg_type` sets the initial message type (same values as `secret.net.msg.*`). Defaults to `nop` if omitted. You can change it later with `set_type`.

```lua
local buf = secret.net.packet(4096)                              -- buffer only
local buf = secret.net.packet(4096, secret.net.msg.string_cmd) -- with preset type
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.header_bits: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.header_bits: number
</code>

- Standard Source net message header size in bits. Currently `6`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.msg: table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.msg: table
</code>

- Message type IDs for `set_type`, the on-wire header in `write_uint`, and the optional second argument to `net.packet`.

**Generic**

| Key | Description |
| --- | --- |
| `nop` | No operation |
| `disconnect` | Disconnect |
| `file` | File transfer |
| `tick` | Tick |
| `string_cmd` | Client string command |
| `set_convar` | Set console variable |
| `signon_state` | Sign-on state |

**Server → client (`svc_*`)**

| Key | Description |
| --- | --- |
| `svc_print` | Console print |
| `svc_server_info` | Server info |
| `svc_send_table` | Send datatable |
| `svc_class_info` | Class info |
| `svc_set_pause` | Set pause |
| `svc_create_string_table` | Create string table |
| `svc_update_string_table` | Update string table |
| `svc_voice_init` | Voice init |
| `svc_voice_data` | Voice data |
| `svc_sounds` | Sound list |
| `svc_set_view` | Set view entity |
| `svc_fix_angle` | Fix angle |
| `svc_crosshair_angle` | Crosshair angle |
| `svc_bsp_decal` | BSP decal |
| `svc_user_message` | User message |
| `svc_entity_message` | Entity message |
| `svc_game_event` | Game event |
| `svc_packet_entities` | Packet entities |
| `svc_temp_entities` | Temp entities |
| `svc_prefetch` | Prefetch |
| `svc_menu` | Menu |
| `svc_game_event_list` | Game event list |
| `svc_get_cvar_value` | Get cvar value |
| `svc_cmd_key_values` | Command key values |
| `svc_gmod_server_to_client` | GMod server → client |

**Client → server (`clc_*`)**

| Key | Description |
| --- | --- |
| `clc_client_info` | Client info |
| `clc_move` | Movement |
| `clc_voice_data` | Voice data |
| `clc_baseline_ack` | Baseline ack |
| `clc_listen_events` | Listen events |
| `clc_respond_cvar_value` | Respond cvar value |
| `clc_file_crc_check` | File CRC check |
| `clc_save_replay` | Save replay |
| `clc_cmd_key_values` | Command key values |
| `clc_file_md5_check` | File MD5 check |
| `clc_gmod_client_to_server` | GMod client → server |

---
## Packet

Methods on a `net.packet` returned by `secret.net.packet`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_uint(value: number, bits: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_uint(value: number, bits: number)
</code>

- Writes an unsigned integer using an arbitrary bit width.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_u8(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_u8(value: number)
</code>

- Writes a single byte (`0`–`255`).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_i16(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_i16(value: number)
</code>

- Writes a signed 16-bit integer.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_i32(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_i32(value: number)
</code>

- Writes a signed 32-bit integer.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_str(str: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_str(str: string)
</code>

- Writes a null-terminated string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_ubit(value: number, bits: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_ubit(value: number, bits: number)
</code>

- Writes an unsigned bit field.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_u32(value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_u32(value: number)
</code>

- Writes a 32-bit word.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:seek_bit(bit: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:seek_bit(bit: number)
</code>

- Seeks the write cursor to a bit position.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:write_raw(data: string, bits: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:write_raw(data: string, bits: number)
</code>

- Writes raw bits from a Lua string.
- Errors if `bits` is negative or exceeds the length of `data`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:data_ptr(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:data_ptr(): number
</code>

- Returns the buffer base pointer as a number.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:set_type(id: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:set_type(id: number)
</code>

- Sets the message type used when transmitting. Use a value from `secret.net.msg`.\
  This is separate from the on-wire header - you still need `write_uint(id, secret.net.header_bits)` in the buffer for most message types.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:transmit(reliable?: boolean): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:transmit(reliable?: boolean): boolean
</code>

- Sends the message over the active net channel.
- `reliable` defaults to `true`.
- Returns `false` if there is no active connection.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### packet:bits_left(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
packet:bits_left(): number
</code>

- Returns the number of writable bits remaining in the buffer.

---
## Blocking

Block outgoing net messages before they are sent, or incoming net messages before their `net.Receive` handler runs.

| `writestring` | `incoming` | Blocks |
|---|---|---|
| `false` | `false` (default) | Outgoing `net.Start` for the channel name |
| `true` | `false` | Outgoing messages that call `net.WriteString` containing the substring |
| `false` | `true` | Incoming `net.Receive` for the channel name |

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.block(cmd: string, writestring: boolean, incoming?: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.block(cmd: string, writestring: boolean, incoming?: boolean)
</code>

- Blocks a net channel or substring rule.
- Set `incoming` to `true` to block incoming `net.Receive` handlers for `cmd`.
- When `incoming` is omitted or `false`, blocking applies to outgoing traffic only.

```lua
-- outgoing
secret.net.block("anticheat_ban", false) -- blocks net.Start for this channel
secret.net.block("bad_payload", true)    -- blocks net.WriteString containing this text

-- incoming
secret.net.block("anticheat_notify", false, true) -- blocks net.Receive for this channel
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.unblock(cmd: string, writestring: boolean, incoming?: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.unblock(cmd: string, writestring: boolean, incoming?: boolean)
</code>

- Removes a block rule created with `net.block`.
- Pass the same `writestring` and `incoming` values you used when blocking.

```lua
secret.net.unblock("anticheat_ban", false)            -- unblocks outgoing net.Start
secret.net.unblock("bad_payload", true)               -- unblocks outgoing net.WriteString
secret.net.unblock("anticheat_notify", false, true)  -- unblocks incoming net.Receive
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### secret.blocker on net.Receive

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
secret.blocker.add("net.Receive", id, function(channel) return true end)
</code>

- Lua blocker listeners can also drop incoming messages.
- Return `true` from the callback to block the message (same effect as `net.block(channel, false, true)`).

```lua
secret.blocker.add("net.Receive", "block_notify", function(channel)
    if channel == "anticheat_notify" then
        return true
    end
end)
```

---
## Time & latency

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.get_latency(flow: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.get_latency(flow: number): number
</code>

- Returns the current network latency for the specified direction.
- `flow` must be `0` (outgoing) or `1` (incoming). Any invalid value defaults to `0`.

```lua
local latency_out = secret.net.get_latency(0) -- gets outgoing latency
local latency_in = secret.net.get_latency(1) -- gets incoming latency
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### net.server_time(offset: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
net.server_time(offset: number): number
</code>

- Returns the predicted server time based on the local player’s `tickbase`.
- If offset is provided, it shifts the tickbase by that amount.

```lua
-- get current predicted server time
local time = secret.net.server_time()

-- get server time 2 ticks ahead
local future = secret.net.server_time(2)

print("current:", time, "future:", future)
```
<div hidden>

```ts

```

</div>
