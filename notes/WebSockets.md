**Title:** WebSockets

**Idea:** WebSockets establish a persistent, full-duplex TCP connection between client and server. Once the initial HTTP handshake upgrades to the WebSocket protocol, both sides can push messages to each other independently and at any time — no polling, no repeated handshakes.

**Key characteristics:**
- **Persistent connection:** Single long-lived connection replaces repeated HTTP requests
- **Full-duplex:** Client and server can send messages simultaneously and independently
- **Low latency:** No per-message HTTP overhead after the initial handshake
- **Event-driven:** Messages arrive as events; both sides react asynchronously
- **Binary and text support:** Can transmit both text frames and binary data

**Trade-offs:**
- Ideal for scenarios requiring real-time, bidirectional communication
- More complex to scale than HTTP: load balancers require sticky sessions or a pub/sub broker (e.g. Redis) to fan out messages across server instances
- Overkill when communication is only server → client; use SSE for that — it's simpler and built on plain HTTP
- Firewalls and proxies occasionally interfere with persistent WebSocket connections

**When to use:**
- Chat applications and collaborative editing
- Multiplayer games and live interactive dashboards
- Any use case requiring two-way real-time communication

**Connections:**
- [[Server-Sent Events (SSE)]]
- [[Bidirectional Streaming]]
- [[HTTP2 Multiplexing]]
- [[gRPC]]
- [[Webhooks vs. Polling]]

Up: [[API protocols 101]]

## Sources
https://blog.bytebytego.com/p/api-protocols-101-a-guide-to-choose

## Tags
#api
