

![[websocket infographic notebook llm.png]]




- websocket is a modern application layer protocols built on top of HTTP expand it past ==simple request-and-response web browsing into **real-time streaming, bi-directional communication.**==
- like http is 1 req-res cycle and for realtime we came with polling ( means each cycle k bad new cycle start so updated data aye -- and feels like real time ) but it had latency so we totally removed the idea of closing the req-res cycle and so now anyone can send data anytime (client and server) making it really real time and we named it as websocket
- Websocket handshake -
  client http normal request karta h + `upgrade` karne ki request karta h --> to `websocket`,
  server responds with `101 switching protocols` and done.
- like http - ws, https - wss
- what is the upgrade -
  each http request contains tcp handshake with each req
  http request needs full heavy header with each req.
  websocket request is opened one time and is a full duplex connection ( no header each time )
- WebSocket protocol connection banane ke liye shuruat me **HTTP protocol** ka hi use karta hai. Jab server haan bol deta hai, tabhi wo line line normal HTTP se badalkar "WebSocket TCP pipe" banti hai.
- MAST LINE --> websockets are events driven and not request driven. ( as the tunnel stays open throughout )
- The moment that HTTP `101` response is sent and received, **the HTTP protocol is completely turned off** for this connection.
  The underlying TCP connection is **never closed**. Instead, both sides switch their software drivers from "HTTP mode" to "WebSocket mode." The TCP pipeline remains wide open, transforming into a **full-duplex tunnel**.
- websocket are for clients (browser) to talk to a server



---