
A **ghost connection** (also known as a dead, stale, or half-open connection) occurs when a client unexpectedly disconnects—such as losing network coverage, closing a laptop lid, or switching Wi-Fi networks—without sending a proper TCP closure handshake (`FIN` packet) to the server.

Because no explicit teardown signal is received, the server assumes the client is still connected and keeps the socket alive. Holding on to thousands of these phantom connections slowly degrades and eventually crashes the server for a few key reasons:
1. Memory Exhaustion (RAM)
2. File Descriptor Limit (OS-Level Bottleneck) - Every ghost connection permanently holds onto its assigned File Descriptor.
3. CPU Spikes & Wasted Processing -
   - **Broadcasting Overhead:** When the server attempts to broadcast an event (like a live score update or message) to all connected clients, it iterates over a list containing thousands of dead sockets. It wastes precious CPU cycles attempting to serialize and write data into closed TCP buffers.


### How Real-World Servers Prevent This: Heartbeats (Ping/Pong)

To stop ghost connections from silently killing the server, real-time engines implement a periodic **Ping/Pong heartbeat protocol**:

1. **Periodic Ping:** The server sends a lightweight `ping` frame to every connected socket every 30 seconds.
    
2. **Pong Response:** Healthy clients automatically reply with a `pong` frame.
    
3. **Dead Socket Pruning:** If a client fails to respond with a `pong` within a set timeout window, the server explicitly marks the connection as dead, invokes `socket.terminate()`, and cleans up all associated memory and File Descriptors.
