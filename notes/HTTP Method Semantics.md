**Title:** HTTP Method Semantics

**Idea:** Each HTTP method carries a specific, standardized meaning: `GET` retrieves without side effects; `POST` creates and returns a Location header; `PUT` replaces fully (idempotent); `PATCH` updates partially; `DELETE` removes and returns 204. Using methods for their intended purpose makes APIs predictable and cacheable.

**Why it matters:** Misusing methods (e.g., using GET to delete data, or POST for updates) breaks caching, security assumptions, and client expectations — especially in frameworks that auto-generate behavior from method types.

**Trade-offs:** `PUT` vs. `PATCH` is commonly confused; `PUT` replaces the entire resource while `PATCH` only modifies specified fields.

**Connections:**

- [[REST URL Design Conventions]]
- [[HTTP Error Codes as a Shared Contract]]
- [[Idempotency in API Design]]