**Title:** Query Parameter Conventions

**Idea:** Standardized query parameter patterns make APIs intuitive: use `?field=value` for filters with `&` as separator; use `?search=term` for global search; use `first`, `last`, `count` for collection navigation; use `?sort_by=desc(field)` for ordering; use `?fields=a,b` for partial responses.

**Why it matters:** Conventions reduce the learning curve for new integrators and prevent each team from inventing incompatible query schemes.

**Connections:**

- [[Pagination Strategies and Their Trade-offs]]
- [[Partial Response and Field Selection]]
- [[REST URL Design Conventions]]

## Tags
#api