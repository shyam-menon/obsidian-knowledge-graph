**Title:** Attribute-Based Access Control (ABAC)

**Idea:** ABAC evaluates authorization decisions based on a combination of three factors: the caller's identity, the specific resource being accessed, and contextual attributes (time, location, device, etc.). It is more expressive than RBAC but significantly more complex to implement and maintain.

**Why it matters:** RBAC cannot represent fine-grained, context-sensitive permissions (e.g., "a user can edit this document only if they are its owner AND the request comes from a trusted network"). ABAC fills that gap when RBAC's expressiveness is exhausted.

**Trade-offs:** Higher expressiveness comes with higher operational complexity. Policy logic can become difficult to audit and reason about. ABAC is appropriate when RBAC has demonstrably broken down, not as a default starting point.

**Connections:**

- [[Role-Based Access Control (RBAC)]]
- [[Principle of Least Privilege]]
- [[Authentication and Authorization are Independent Checks]]

## References
https://gemini.google.com/share/caedbe94480a