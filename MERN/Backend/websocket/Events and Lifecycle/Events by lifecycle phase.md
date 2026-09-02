
## Events in each Lifecycle phase -
WebSocket events do not all occur only at the "open" stage. Instead, each event belongs to a specific, separate phase of the WebSocket connection lifecycle on both the client and server sides.


### my understanding -
1. open phase -> open event (aka connection event for server side),  message event
2. error (can be in connecting, open, closing phase) -> error event
3. closing phase -> close event


### The WebSocket Lifecycle Flow

The connection flows sequentially through distinct states, and events are triggered only when transitioning into or operating within those specific states:

```unset
   [ 1. CONNECTING ]  --> Handshake (HTTP Upgrade Request)
           │
     ┌─────┴──────────┐
     ▼ (Success)      ▼ (Failure)
[ 2. OPEN ]       [ 3. CLOSING / CLOSED ] 
     │                    ▲
     ├──► onmessage       │
     └──► onerror ────────┘
```

---

## Phase-by-Phase Breakdown of Events

### 1. The Handshake Phase (Connecting)

- State: `CONNECTING`
- What happens: The client sends an HTTP request asking to upgrade to the WebSocket protocol, and the server decides whether to accept it.
- Events fired: No successful communication events fire yet. If the handshake fails here (e.g., 401 Unauthorized or 502 Bad Gateway), the lifecycle bypasses the open stage completely and goes straight to the error and close states.

### 2. The Established Phase (Open)

- State: `OPEN`
- The `open` event: Fired exactly once the moment the handshake is successfully completed. It signals that a persistent, bidirectional pipe is ready for data.
- The `message` event: Fired continuously and dynamically throughout the lifetime of the connection. It triggers every single time the client or server receives a new frame of data (text, binary, or images). It reacts to live traffic.

### 3. The Error Phase (Can happen anytime)

- State: Can happen during `CONNECTING`, `OPEN`, or `CLOSING`.
- The `error` event: Fired whenever something breaks. If the network drops mid-stream, a protocol error occurs, or the server crashes while the connection is active, this event fires to allow your code to log or handle the failure.

### 4. The Termination Phase (Closing / Closed)

- State: `CLOSING` transitioning to `CLOSED`
- The `close` event: Fired exactly once at the very end of the lifecycle. This happens long after the initial "open" phase has ended, triggered either because a party called `socket.close()` or due to a network disruption. Once this fires, no more messages can be sent or received.

---

## Client-Side vs. Server-Side Mirroring

This behavioral lifecycle is virtually identical on both the client (e.g., native browser JavaScript `WebSocket` API) and the server (e.g., Node.js `ws` library).

|Event|Fired on Client Side When...|Fired on Server Side When...|
|---|---|---|
|`open` / `connection`|The browser receives the `101 Switching Protocols` response from the server.|The server successfully finishes upgrading the socket and registers the client.|
|`message`|Incoming data arrives from the server.|Incoming data arrives from the client.|
|`error`|A network drop or protocol failure is detected by the browser.|The underlying TCP socket errors out or received frames break protocol rules.|
|`close`|The connection finishes tearing down completely.|The server cleans up the socket memory and unregisters the client.|

---

If you need any code templates for your notes (like standard JavaScript client or Node.js server boilerplate), let me know which language you prefer and I can write them out cleanly for you.