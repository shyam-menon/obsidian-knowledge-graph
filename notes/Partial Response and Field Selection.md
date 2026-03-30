**Idea:** Clients can request only the specific fields they need using a `?fields=` query parameter. This reduces payload size, lowers bandwidth consumption, and speeds up rendering — especially on mobile networks.

**Why it matters:** Over-fetching is a common API inefficiency. Partial response is a lightweight alternative to GraphQL for scenarios where bandwidth or parsing overhead matters.

**Trade-offs:** Increases server-side complexity slightly (filtering fields before serialization); clients must know field names upfront.

**Connections:**

- [[Query Parameter Conventions]]
- [[Pagination Strategies and Their Trade-offs]]
- [[API Granularity — The Medium-Grained Sweet Spot]]

## Tags
#api