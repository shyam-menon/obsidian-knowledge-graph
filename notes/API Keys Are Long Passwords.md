**Title:** API Keys as Long Passwords

**Idea:** API keys are functionally long, opaque passwords. They authenticate a caller but carry no built-in expiry or scope. If leaked (via public repos, logs, or environment variables), they grant full access to whoever holds them. They must be stored securely, rotated periodically, and always paired with proper authorization checks.

**Why it matters:** API key leaks are common and often silent. Treating them as passwords — with the same hygiene requirements — significantly reduces exposure windows.

**Trade-offs:** API keys are simple to implement but weak in isolation. OAuth 2.0 and JWT provide scoped access and expiry, adding complexity but solving problems API keys cannot.

**Connections:**

- [[Authentication and Authorization are Independent Checks]]
- [[JWT and OAuth 2.0 for Scoped Access]]
- [[Principle of Least Privilege]]

## Tags
#security