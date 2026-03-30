**Title:** OpenID Connect — Identity on Top of OAuth

**Idea:** OpenID Connect (OIDC) is a thin identity layer built on top of OAuth 2.0. While OAuth answers "what can this client access?", OIDC also answers "who is this user?" by adding an ID token (JWT) alongside the access token.

**Why it matters:** Needed whenever your integration requires both authorization (what the user can do) and authentication (who the user is) — common in SSO scenarios and consumer-facing apps.

**Connections:**

- [[OAuth 2.0 — Delegated Authorization]]
- [[API Keys — Simple Stateless Authentication]]

## Tags
#security