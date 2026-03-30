**Title:** REST (Representational State Transfer)

**Idea:** REST is a stateless architectural style for APIs that uses HTTP verbs and resource-based URLs. Each request is self-contained — the server holds no session state between calls. Resources are identified by URLs; actions on them are expressed via HTTP methods.

**Key characteristics:**
- **Stateless:** Every request contains all information needed to process it
- **Uniform interface:** Resources identified by URLs, manipulated via standard HTTP verbs
- **Cacheable:** Responses can declare themselves cacheable to improve performance
- **Client-server separation:** UI and data storage evolve independently
- **Layered system:** Intermediaries (proxies, gateways) can sit between client and server transparently

**Trade-offs:**
- Simple to implement and widely understood — the default choice for most APIs
- Excellent tooling, browser support, and developer familiarity
- Over-fetching (getting more data than needed) and under-fetching (needing multiple requests) are inherent weaknesses — addressed by GraphQL
- Not suited for real-time or bidirectional communication — use WebSockets for that
- No built-in contract enforcement — relies on documentation conventions

**When to use:**
- Public APIs and CRUD services
- Browser-to-server communication
- Any scenario where simplicity and interoperability matter more than raw performance

**Connections:**
- [[gRPC]]
- [[GraphQL]]
- [[HTTP Method Semantics]]
- [[REST URL Design Conventions]]
- [[API Versioning Strategy]]
- [[HTTP Error Codes as a Shared Contract]]
- [[Webhooks vs. Polling]]
- [[SOAP]]

Up: [[API protocols 101]]

## Sources
https://blog.bytebytego.com/p/api-protocols-101-a-guide-to-choose

## Tags
#api
