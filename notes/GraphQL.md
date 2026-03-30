**Title:** GraphQL

**Idea:** GraphQL is a query language and runtime for APIs that lets clients specify exactly the data they need in a single request. Instead of multiple fixed endpoints, it exposes a single endpoint backed by a strongly typed schema. The client shapes the response.

**Key characteristics:**
- **Single endpoint:** All queries and mutations go through one URL
- **Client-driven queries:** The client declares what fields it wants — no more, no less
- **Strongly typed schema:** The schema is the contract; it self-documents the API
- **Subscriptions:** Native support for real-time updates via persistent connections
- **Introspection:** Clients can query the schema itself to discover available types and fields

**Trade-offs:**
- Eliminates over-fetching and under-fetching — a single query replaces multiple REST calls
- Excellent for complex frontends with varied data requirements (e.g. mobile vs. desktop needing different fields)
- More complex to set up than REST — requires schema design, resolver logic, and a GraphQL server
- Query complexity attacks: deeply nested or expensive queries can overload the server without depth/cost limits
- Caching is harder than REST (no URL-based cache keys by default)

**When to use:**
- Complex frontends where different views need different data shapes
- Mobile clients where bandwidth efficiency matters
- When collapsing multiple REST round-trips into one query provides measurable gains
- Not ideal for simple CRUD APIs where REST is sufficient

**Connections:**
- [[REST]]
- [[gRPC]]
- [[Partial Response and Field Selection]]
- [[API Granularity — The Medium-Grained Sweet Spot]]
- [[Pagination Strategies and Their Trade-offs]]

Up: [[API protocols 101]]

## Sources
https://blog.bytebytego.com/p/api-protocols-101-a-guide-to-choose

## Tags
#api
