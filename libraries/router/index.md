# router
Allows for communication across networks via Socket IO.\
Essentially allowing you to communicate to whatever instances you have open from a master controller.\
Its essentially just a chat-room where you manage the clients.

!!!Security & Locks
If you feel that security-wise your controller isn't properly secure.\
We suggest giving libsodium a shot at asymmetric encryption & signatures.
!!!

!!!danger Dev-Locked
Due to the nature of this library and its implications...\
We have placed a lock on this section, you can only use this with developer access.
!!!

!!!danger Implementation
Currently this system is not using backend infrastructure,\
therefore an alternative has been made to accomodate on your own system.
!!!

---
## Example
```lua
-- connect to backend hosted on your own network.
local handle = router.spawn("http://127.0.0.1:8000")

function handle:open()
    print("Connected!")

    -- list all clients active on the network
    for k, v in pairs(self.clients) do
        print(k, v)
    end

    -- destroy after x amount of seconds
    timer.Simple(5, function()
        handle:destruct()
    end)
end

function handle:error(...)
    print("Error: ", ...)
end

function handle:close(...)
    print("Close: ", ...)
end

function handle:operator(from, op, data)
    -- We received a message from someone
    print("Operator: ", from, op, data)
end

-- connect to network
handle:connect()
```

---

## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### router.spawn(address: string, headers?: {[index: string]: string}): router.handle

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
router.spawn(address: string, headers?: {[index: string]: string}): router.handle
</code>

- Creates a new router handle.
- By providing a "unique" it will maintain that as it's unique identifier when connecting.
- Keep in mind these "unique" values must always be "unique" for connection stability.

---

## Handle

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:connect()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:connect()
</code>

- Attempts to connect to the router network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:disconnect()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:disconnect()
</code>

- Disconnects from the router network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:destruct()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:destruct()
</code>

- Disconnects & destroys any active instances of Socket IO.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:is_connected(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:is_connected(): boolean
</code>

- If the router client is currently connected to a network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:broadcast(op: string, t: {[index: string | number]: any})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:broadcast(op: string, t: {[index: string | number]: any})
</code>

- Sends an operation to all clients on the network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:omit(clients: string[] | router.client[], op: string, t: {[index: string | number]: any})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:omit(clients: string[] | router.client[], op: string, t: {[index: string | number]: any})
</code>

- Sends a message to all clients on the network, except for those listed.
- You can supply either the unique IDs or the clients themselves.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:at(clients: string[] | router.client[], op: string, t: {[index: string | number]: any})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:at(clients: string[] | router.client[], op: string, t: {[index: string | number]: any})
</code>

- Sends a message to all clients on the network, only for those listed.
- You can supply either the unique IDs or the clients themselves.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:datastore(key: string, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:datastore(key: string, value: string)
</code>

- Sends & stores a key and value on the client for all clients to view.
- On other clients they can access it via `client.datastore`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle.clients: router.client[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle.clients: router.client[]
</code>

- A list of connected clients on the network.

---
These are callbacks you can override on the class itself.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:open()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:open()
</code>

- Called when a connection has been made.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:close(code: number, reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:close(code: number, reason: string)
</code>

- Called when a connection has been closed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:error(code: number, reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:error(code: number, reason: string)
</code>

- Called when an internal error from Socket IO occures.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:connected(client: router.client)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:connected(client: router.client)
</code>

- Called when another router client has connected to the network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:disconnected(client: router.client)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:disconnected(client: router.client)
</code>

- Called when another router client has disconnected from the network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:message(payload: string, is_binary: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:message(payload: string, is_binary: boolean)
</code>

- Called when a message has been received.
- Do note this is for internal use and debugging only.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### handle:operator(from: router.client, op: string, data: {[index: string | number]: any})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
handle:operator(from: router.client, op: string, data: {[index: string | number]: any})
</code>

- Called when an operation has been received from send, broadcast, omit or at

---

## Client
The client themselves that you see from your router's perspective.\
You can target these clients and send messages to them.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client:fullname(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client:fullname(): string
</code>

- Retrieves the full name of the client (includes name, unique and ip)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client:uniquename(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client:uniquename(): string
</code>

- Retrieves the unique name of the client (inlcudes unique and ip)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client:alive(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client:alive(): boolean
</code>

- Returns if the client is currently connected and on your list of clients

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client:send(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client:send(op: string, t: {[index: string | number]: any})
</code>

- Sends an operation to this specific client on the network.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client.name: string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client.name: string
</code>

- The name the client associates by.
- This is not to be made use of as an identifier.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client.game: string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client.game: string
</code>

- The game the client associates by.
- This is not to be made use of as an identifier.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client.unique: string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client.unique: string
</code>

- The unique ID the client associates by.
- This is used internally for targeting.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client.unique: string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client.ip: string
</code>

- The IP address the client associates by.
- This is not to be made use of as an identifier.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client.datastore: {[index: string]: string}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client.datastore: {[index: string]: string}
</code>

- A list of persistant data that exists per-client.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### client.router: router.handle

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
client.router: router.handle
</code>

- The associated router handler.
<div hidden>

```ts

```

</div>
