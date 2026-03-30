**Title:** Webhooks

**Idea:** Webhooks are event-driven HTTP callbacks. Instead of a client repeatedly polling a server for updates, the server sends an HTTP POST to a pre-registered URL whenever a specific event occurs. The consumer registers a URL; the producer calls it.

**Key characteristics:**
- **Event-driven:** Triggered by events on the producer side, not by client requests
- **Push-based:** No persistent connection — a new HTTP request is made per event
- **Asynchronous:** The producer fires and moves on; the consumer processes at its own pace
- **No persistent connection:** Lightweight — no open socket to maintain
- **Configurable payloads:** The event payload is typically JSON describing what happened

**Trade-offs:**
- Efficient — eliminates polling overhead entirely
- Requires the consumer server to be publicly reachable; local development needs tunnelling (e.g. ngrok)
- No guaranteed delivery by default — failed deliveries require retry logic with exponential backoff on the producer side
- Security requires HMAC signature validation to prevent spoofed events — never trust an incoming webhook without verifying the signature
- Debugging is harder than polling: events arrive unpredictably and failures are asynchronous

**When to use:**
- Payment notifications (Stripe, PayPal)
- CI/CD triggers (GitHub push → build pipeline)
- Third-party integrations where you want to react to events in another system
- Any asynchronous event notification between services where polling would be wasteful

**Connections:**
- [[Webhooks vs. Polling]]
- [[REST]]
- [[Server-Sent Events (SSE)]]
- [[WebSockets]]
- [[API security 101]]

Up: [[API protocols 101]]

## Sources
https://blog.bytebytego.com/p/api-protocols-101-a-guide-to-choose

## Tags
#api
