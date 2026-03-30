Title: Paladin — Centralised Authentication & Authorization as a Service

Idea: Paladin is a shared authentication and authorization fabric for the entire CBA ecosystem. Built on Apigee Edge Cloud as the API gateway, it enforces fine-grained access policies across all applications. Each app integrates with Paladin with minimal effort — Paladin handles token issuance via HP ID, policy evaluation, user lifecycle (including auto-revoke on departure), and provides a self-service request workflow for access. Implements a Zero Trust security model.

Why it matters: Building auth independently per application is expensive, inconsistent, and a security risk. A shared auth fabric means every service enforces the same policies, and revoking a user's access happens once and propagates instantly across all systems. The minimal-integration-effort design lowers the barrier for new services to adopt proper security from day one rather than bolting it on later.

Connections:

- [[MPC]] — MPC uses Paladin for partner user authentication and token management
- [[Enablement Service]] — ES enforces Paladin-issued tokens on all GraphQL requests
- [[UsageService]] — Usage Service authenticates service-to-service calls via Paladin
- [[MSCC]] — DCC uses Paladin (STS) for customer session token management
- [[Fleet Operations]] — FleetOps uses Paladin for role-based access across 7 user roles
- [[CARD]] — CARD web application authenticates users via Paladin

## Tags
#systems