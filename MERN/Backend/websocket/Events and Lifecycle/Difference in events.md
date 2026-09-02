
Because both sides are part of the connection, both sides need to handle events. However, they use different event names because their **roles and perspectives** are different.


**Client Side vs. Server Side Roles**

- **The Client** initiates the phone call. It reaches out to one specific destination (the server).
    
- **The Server** is like a call center host. It stays running, waiting to receive phone calls from hundreds or thousands of clients at the same time.
    

---

## Difference in events at client and server -

### my understanding -
mainly client focused h

1. open -
	client - m ara hu,   server - ek client ara h
2. close -
	client - m ara hu,   server - ek client ara h
3. error -
	client - merepe kuch error h,   server - is client p error h
4. message -
	client - server se message aya,   server - client se message aya



### **1. Connecting: `open` (Client) vs. `connection` (Server)**

Why does the client listen for `open` while the server listens for `connection`?

- **Client: `open` event**
    
    - **Perspective:** _"My connection attempt to the server succeeded!"_
        
    - **What happens:** The client creates a new socket (`new WebSocket('ws://...')`). Once the handshake passes and the tunnel is ready, the client triggers `open`. It knows _which_ server it connected to because it initiated the request.
        
    - **Common use:** Enabling UI elements, showing a "Connected" status indicator, or immediately sending an authentication token or initial request.
        
- **Server: `connection` event**
    
    - **Perspective:** _"A brand new client just called in!"_
        
    - **What happens:** The server doesn't just open a connection for itself; it creates a brand new, unique socket instance _specifically for that incoming user_. The event callback receives this specific client's `socket` as an argument (`wss.on('connection', (socket) => ...)`).
        
    - **Common use:** Saving this client's unique socket into an array or database of connected users, logging their IP/session, or sending them a welcome message.
        

---

### **2. Closing: `close` (Both Client & Server)**

Why do both sides have a `close` event?

Because either side can hang up the phone, or the wire can get cut (e.g., losing Wi-Fi). Both sides need to know when the link is broken so they can clean up.

- **Client: `close` event**
    
    - **Perspective:** _"I am no longer connected to the server."_
        
    - **Why it matters:** The browser needs to know the tunnel dropped so it can update the UI (e.g., show "Reconnecting..."), stop sending messages, or attempt to automatically reconnect.
        
- **Server: `close` event**
    
    - **Perspective:** _"This specific client disconnected or dropped off."_
        
    - **Why it matters:** The server must free up memory. It removes that specific client's socket from its list of active users, updates their online status to "offline," and stops trying to broadcast messages to them.

---

### 3. `message`: Receiving Data

Because WebSockets are **full-duplex**, both the client and the server can send and receive messages at any time without waiting for a request-response cycle.

- **Client: `message` event**
    
    - **Perspective:** _"The server just pushed new data to me!"_
        
    - **How it works:** Fires whenever a frame arrives from the backend. The browser receives the raw payload in `event.data`.
        
    - **Common use:** Parsing incoming JSON to update UI components in real time (e.g., live scoreboards, chat feeds, or price tickers).
        
- **Server: `message` event**
    
    - **Perspective:** _"This specific connected client just sent data to the backend!"_
        
    - **How it works:** Unlike the client (which has one connection to one server), the server attaches the `message` listener to the **individual client socket instance** (`socket.on('message', ...)`).
        
    - **Common use:** Validating client input, saving messages to a database, or broadcasting/unicasting the data out to other active sockets.
        

---

### 4. `error`: Handling Failures

Errors can happen asynchronously on either side due to network drops, malformed data frames, or unhandled exceptions.

- **Client: `error` event**
    
    - **Perspective:** _"Something went wrong with my connection attempt or network socket!"_
        
    - **How it works:** Triggers when the connection fails during the handshake or drops unexpectedly. Note that browser security policies often obscure error details, so the event object may not specify _why_ it failed—only that an error occurred.
        
    - **Common use:** Showing an alert or banner in the UI ("Connection error, retrying...").
        
- **Server: `error` event**
    
    - **Perspective:** _"An error occurred on a specific client's socket connection!"_
        
    - **How it works:** Triggers if a client sends invalid frames, disconnects abruptly without a clean TCP FIN packet, or encounters a socket-level failure.
        
    - **Common use:** Logging exception details to server logs, metrics tools, or preventing server crashes by handling the error gracefully.

