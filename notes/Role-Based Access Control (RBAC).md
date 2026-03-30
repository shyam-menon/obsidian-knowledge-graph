**Title:** Role-Based Access Control (RBAC)

**Idea:** RBAC assigns permissions to roles (e.g., admin, read-only, billing manager) rather than to individual users. Users are then assigned to roles. This makes permission management scalable: adding a user means assigning a role, and changing permissions for a category of users means updating the role definition once.

**Why it matters:** Per-user permission management becomes unworkable as systems grow. RBAC abstracts that complexity, reduces configuration errors, and makes access auditing tractable.

**Trade-offs:** RBAC degrades over time as roles proliferate, overlap, and edge cases accumulate. When role definitions can no longer express the required logic, Attribute-Based Access Control (ABAC) is a natural next step — at the cost of significantly higher complexity.

**Connections:**

- [[Principle of Least Privilege]]
- [[Attribute-Based Access Control (ABAC)]]
- [[Authentication and Authorization are Independent Checks]]]
- [[Broken Object Level Authorization (BOLA)]]

## References
https://gemini.google.com/share/caedbe94480a