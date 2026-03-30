**Title:** Broken Object Level Authorization (BOLA)

**Idea:** BOLA occurs when an API authenticates a user but does not verify whether that user is authorized to access the specific object they are requesting. An attacker exploits this by manipulating resource identifiers (e.g., changing a user ID in a URL) to access another user's data. It consistently ranks as one of the most common API vulnerabilities.

**Why it matters:** Standard authentication flows will not surface this vulnerability — it only appears when per-resource authorization checks are absent. No amount of credential strength prevents it.

**Trade-offs:** Per-resource authorization checks add computational overhead and require careful design, but the security cost of omitting them far exceeds the engineering cost.

**Connections:**

- [[Authentication and Authorization are Independent Checks]]
- [[Role-Based Access Control (RBAC)]]
- [[Principle of Least Privilege]]