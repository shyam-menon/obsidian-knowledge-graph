**Title:** Server-Sent Events (SSE)

**Idea:** SSE is an HTTP-based mechanism for servers to push a continuous stream of events to a browser or client over a single long-lived connection. Communication is strictly unidirectional: server → client only. The client opens one connection and listens; the server sends events whenever they occur.

**Key characteristics:**
- **Unidirectional:** Server pushes, client only receives — no client-to-server messaging on the same connection
- **Plain HTTP:** No protocol upgrade required — works over standard HTTP/1.1 or HTTP/2
- **Automatic reconnection:** The browser's native EventSource API reconnects automatically if the connection drops
- **Text only:** Messages are UTF-8 text; binary data requires base64 encoding
- **Event IDs:** Supports last-event-id headers so clients can resume from where they left off after reconnect

**Trade-offs:**
- Much simpler than WebSockets for server-push use cases — no special server infrastructure needed
- Works naturally with HTTP/2 multiplexing (multiple SSE streams over one connection)
- Cannot send messages from client to server over the same connection — requires a separate HTTP request for that
- Not suitable for bidirectional real-time communication — use WebSockets for that

**When to use:**
- Live feeds, news tickers, stock price updates
- Notification systems and progress indicators
- Log streaming and build output
- Any scenario where the server pushes updates but the client only listens

**Connections:**
- [[WebSockets]]
- [[Bidirectional Streaming]]
- [[HTTP2 Multiplexing]]
- [[Webhooks vs. Polling]]
- [[Webhooks]]

Up: [[API protocols 101]]

## Sources
https://blog.bytebytego.com/p/api-protocols-101-a-guide-to-choose

## Tags
#api
