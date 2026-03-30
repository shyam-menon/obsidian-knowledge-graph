**Title:** Pagination Strategies and Their Trade-offs

**Idea:** Four main pagination patterns exist: (1) Offset/Limit — simple but slow on large datasets due to DB scans; (2) Keyset — anchors on the last seen value, scales well; (3) Fixed Pages — `?page=N`, easy but rigid; (4) Flexible Pages — `?page=N&page_size=M`, adds client control. Choice depends on data size and performance needs.

**Why it matters:** Incorrect pagination choice causes performance degradation at scale and poor UX (e.g., data skipping or duplication when records are inserted mid-pagination).

**Trade-offs:** Offset pagination is easiest to implement but becomes increasingly slow past millions of records. Keyset is more performant but requires a sortable, stable key.

**Connections:**

- [[Query Parameter Conventions]]
- [[Partial Response and Field Selection]]
- [[Bulk Data Transfer Pattern]]

## Tags
#api