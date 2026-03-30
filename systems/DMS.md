
Title: DMS — Deal Packaging Adapter for MP Flex Business Model

Idea: DMS (Deal Management Service) is a purpose-built adapter service that converts won MP Flex deals from MPC into the TTSAP package format required for TMC onboarding. It acts as a translation layer between the legacy deal management format of one business model and the modern CBA-TMC onboarding workflow.

Why it matters: When a platform evolves incrementally, not all upstream systems can be refactored at once. DMS is a classic anti-corruption layer — it absorbs the format differences of one specific business model so the core onboarding pipeline (TMC → Broker → ITSM) stays clean and model-agnostic. This pattern is reusable wherever legacy data formats must be translated without touching the consuming system.

Connections:

- [[MPC]] — DMS receives MP Flex won deal data from MPC
- [[TMC]] — DMS outputs a TTSAP package that TMC uses to initiate onboarding
- [[CARD]] — DMS sends MP Flex deal details to CARD for profitability tracking
- [[Broker]] — Broker orchestrates the downstream steps after DMS hands off the package

## Tags
#systems