**Title:** Authentication vs. Authorization Are Independent Checks

**Idea:** Authentication verifies identity ("who are you?"), while authorization verifies permission ("what can you do?"). These are separate enforcement points. A caller can be fully authenticated but still unauthorized to access a specific resource. Conflating them is one of the most common sources of API security gaps.

**Why it matters:** Nearly all significant API breaches involve this gap. Designing systems with both checks as explicit, independent layers prevents an entire class of vulnerabilities.

**Connections:**

- [[Broken object level authorization (BOLA)]]
- [[Role-Based Access Control (RBAC)]]
- [[HTTPS Secures the Channel, Not the Caller]]
- [[API Keys as Long Passwords]]

## Tags
#security