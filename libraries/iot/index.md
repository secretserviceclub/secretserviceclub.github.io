# iot
IOT is a communication system to the internet.\
You can use this to create secure connections to external backends you create.

!!!warning Concerns of Usage
These functions are not made for performing actions with malicious intent.\
Please use these functions simply for I/O & communication.
!!!

---
## Enums

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.method: {[index: string]: string}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.method: {[index: string]: string}
</code>

- Contains a list of method procedures for HTTP/HTTPS

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.status: {[index: string | number]: string | number}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.status: {[index: string | number]: string | number}
</code>

- Contains a list of status codes for HTTP/HTTPS

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.opcode: {[index: string | number]: string | number}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.opcode: {[index: string | number]: string | number}
</code>

- Contains a list of opcode procedures for sockets

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.closure: {[index: string | number]: string | number}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.closure: {[index: string | number]: string | number}
</code>

- Contains a list of closure procedures for sockets
- These are usually needed when dealing with<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.closure.close
</code>cases

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.http(url: string, callback?: function(response: http_response), options?: http_options)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.http(url: string, callback?: function(response: http_response), options?: http_options)
</code>

- Makes an HTTP/HTTPS request to an address or domain.
- This function is asynchronous, meaning this will not "freeze" Lua.
- The interface types<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
http_options
</code>&<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
http_response
</code>can be seen here:

+++ http_options
```ts
body?: string
method?: string
headers?: {[index: string]: string}
parameters?: {[index: string]: string}
progress?: function(dl_total: number, dl_now: number, up_total: number, up_now: number): boolean?
```
+++ http_response
```ts
headers: {[index: string]: string}
body: string
status: number
reason: string
url: string
```
+++

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.stream(url: string, callback?: function(response: http_response), options?: http_options)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.stream(url: string, callback?: function(response: http_response), options?: http_options)
</code>

- Similar to<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.http
</code>except allows multiple returns from segments of encoded chunks.
- When receiving chunks, all responses will have a `100` status code for continuing.
- Once finished, the status code will either be `200` or a different value if it errored.
- Returning `false` inside the callback will cancel the stream.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.socket(url: string, options?: socket_options): socket_class

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.socket(url: string, headers?: {[index: string]: string}): socket_class
</code>

- Creates a socket object which is connected to an address or domain.
- Upon creation, the socket isn't activated until you invoke it to do so.
- Sockets work by reference, so if there is no-longer a use in lua, it will destroy itself.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### iot.serve(port: number): serve_class

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.serve(port: number): serve_class
</code>

- Creates an HTTP server for requests, similar to express/deno.
- Do note that the server doesn't actually start until you invoke<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:start()
</code>
- Unlike client sockets, if the object gets GC'ed, it won't cleanup the callbacks or invoke a destructor.
- If you "lose" the handle object, you can retrieve it back by simply calling the function again and its exact port number.

---
## Serve
These are interface & function definitions for how we handle `serve_class`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:start(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:start(): boolean
</code>

- Attempts to allocate a port for HTTP connections.
- If this fails it will return `false`.
- Usually a failure indicates a port is already in-use.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:stop()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:stop()
</code>

- De-allocates and stops serving under the allocated port.
- This doesn't actually destroy the object.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:active(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:active(): boolean
</code>

- Checks if the current serve is active on its port.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:port(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:port(): number
</code>

- Gets the current port the serve is on.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:handlers(): {method: string, path: string, callback: function}[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:handlers(): {method: string, path: string, callback: function}[]
</code>

- Gets all handlers associated with the serve.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:sockets(path: string): serve_socket[]

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:sockets(path: string): serve_socket[]
</code>

- Gets all sockets associated with the serve.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:upgrade(): serve_socket

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:upgrade(): serve_socket
</code>

- Upgrades a connection into a socket.
- Must be used inside of a HTTP request.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:socket(path: string, callback: function(connection: serve_socket, opcode: number, data: string | number, extra: string))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:socket(path: string, callback: function(connection: serve_socket, opcode: number, data: string | number, extra: string))
</code>

- Adds a callback for a certain path for socket-based messages.
- Do note that the path must be the same to the socket you upgraded in.
- Opcodes can be seen under<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
iot.opcode
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:any(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:any(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Any is a form of method that allows all types of methods to be seen in callback under the path.
- You can check the method by seeing `req.method`
- If you set the path to `any` it will also act as a any filter, allowing you to process paths individually.
- Do note this is **first-order** making it called first before any other methods

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:get(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:get(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Adds a callback for a certain path under "GET" requests
- The GET method requests a representation of the specified resource.
- Requests using GET should only retrieve data and should not contain a request content.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:post(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:post(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Adds a callback for a certain path under "POST" requests
- The HEAD method asks for a response identical to a GET request, but without a response body.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:head(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:head(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Adds a callback for a certain path under "HEAD" requests
- The POST method submits an entity to the specified resource, often causing a change in state or side effects on the server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:put(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:put(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Adds a callback for a certain path under "PUT" requests
- The PUT method replaces all current representations of the target resource with the request content.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:delete(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:delete(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Adds a callback for a certain path under "DELETE" requests
- The DELETE method deletes the specified resource.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve:options(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve:options(path: string, callback: function(req: { method: string, path: string, query: string, body: string, headers: table}))
</code>

- Adds a callback for a certain path under "OPTIONS" requests
- The OPTIONS method describes the communication options for the target resource.

---
## Serve Socket
These are interface & function definitions for how we handle `serve_socket`

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve_socket:id(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve_socket:id(): string
</code>

- Gets the socket's unique ID.
- Useful if you need to manually track them.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve_socket:disconnect(code?: string | number, reason?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve_socket:disconnect(code?: string | number, reason?: string)
</code>

- Forces a socket to disconnect.
- By providing a string in the code parameter, it will become a reason with normal closure.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve_socket:text(payload: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve_socket:text(payload: string)
</code>

- Sends a text-based payload.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve_socket:binary(payload: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve_socket:binary(payload: string)
</code>

- Sends a binary-based payload.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve_socket:ping(payload?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve_socket:ping(payload?: string)
</code>

- Sends a ping payload, typically used to keep connections alive.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### serve_socket:pong(payload?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
serve_socket:pong(payload?: string)
</code>

- Sends a pong payload, typically used to keep connections alive.

---
## Socket
These are interface & function definitions for how we handle `socket_class`

### Functions
<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:connect()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:connect()
</code>

- Attempt to connect the socket to the constructed URL from creation.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:disconnect(reason?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:disconnect(reason?: string)
</code>

- Disconnects from a socket server with a message if needed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:text(payload: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:text(payload: string)
</code>

- Send a payload message to the socket server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:utf8(payload: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:utf8(payload: string)
</code>

- Send a payload message to the socket server in UTF8 format.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:binary(payload: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:binary(payload: string)
</code>

- Send a payload message to the socket server in binary format.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:close(reason?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:close(reason?: string)
</code>

- Closes the socket connection, this usually also sends a message.
- If you want to re-open the connection, simply run <code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">socket.connect()</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:ping(reason?: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:ping(message?: string)
</code>

- Sends a ping payload to the socket server.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:get_url(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:get_url(): string
</code>

- Gets the current full connection URL.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:get_host(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:get_host(): string
</code>

- Gets the current host from the URL.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:get_port(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:get_port(): string
</code>

- Gets the current port from the URL.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:get_path(): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:get_path(): string
</code>

- Gets the current path from the URL.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:headers_add(key: string, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:headers_add(key: string, value: string)
</code>

- Adds a header to the list of headers to be sent on connection.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:headers_remove(key: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:headers_remove(key: string)
</code>

- Removes a header from the list of headers to be sent on connection.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:headers_get(key: string): string?

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:headers_get(key: string): string?
</code>

- Gets a header by the key-name.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:headers_all(key: string): {[index: string]: string}

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:headers_all(key: string): {[index: string]: string}
</code>

- Gets a list of all headers applied.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:is_open(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:is_open(): boolean
</code>

- If the socket is currently connected.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:is_connecting(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:is_connecting(): boolean
</code>

- If the socket is currently connecting.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:is_closing(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:is_closing(): boolean
</code>

- If the socket is currently closing.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:is_closed(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:is_closed(): boolean
</code>

- If the socket is currently closed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### socket:is_tls(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
socket:is_tls(): boolean
</code>

- If the socket is using TLS as it's connection layer.

### Events
This internally uses the **Signal** library for C++ communication.\
These can be accessed for example by: <code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">socket_class.add(...)</code>
[!ref Signal](/libraries/signal/#library-functions)

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### open()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
open()
</code>

- Called when the socket engine has made a successful connection.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### error(code: number, reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
error(code: number, reason: string)
</code>

- Called if there was a connection failure.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### close(status: number, reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
close(status: number, reason: string)
</code>

- Called when the connection closes, this can contain an error reason.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### message(payload: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
message(payload: string, is_binary: boolean)
</code>

- Called when a message has been received.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ping(reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ping(message: string)
</code>

- Called when the socket server sent a ping.
- This can be used as an "isalive" status refresh.
- However this is managed internally by interstellar.
  
<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### pong(reason: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
pong(message: string)
</code>

- Called when the socket server sent a pong.
- This can be used as an "isalive" status refresh.
<div hidden>

```ts

```

</div>
