**Title:** OAuth 2.0 — Delegated Authorization

**Idea:** OAuth 2.0 is a token-based authorization framework with three parties: the user (resource owner), the client application, and the authorization server. The user grants a specific scope of access to the client without sharing credentials. The client receives a short-lived access token, not the user's password.

**Why it matters:** OAuth allows fine-grained, revocable, scoped access — essential for any integration that touches user data on behalf of a third party.

**Trade-offs:** More complex to implement than API keys; requires an authorization server infrastructure.

**Connections:**

- [[OpenID Connect — Identity on Top of OAuth]]
- [[API Keys — Simple Stateless Authentication]]
- [[Webhooks vs. Polling]]

## Tags
#security