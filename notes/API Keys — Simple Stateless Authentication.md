**Title:** API Keys — Simple Stateless Authentication

**Idea:** API keys are unique tokens issued to a client, passed in request headers or query parameters. They are simple to implement and require no OAuth flow, making them ideal for server-to-server integrations and developer tooling.

**Why it matters:** Speed of onboarding: developers can start calling an API in minutes. Best for scenarios where delegated user-level access is unnecessary.

**Trade-offs:** API keys are static, often long-lived, and if leaked are hard to scope or revoke selectively. They provide no user identity context.

**Connections:**

- [[OAuth 2.0 — Delegated Authorization]]
- [[OpenID Connect — Identity on Top of OAuth]]

## Tags
#security