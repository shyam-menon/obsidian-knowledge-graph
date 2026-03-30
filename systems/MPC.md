Title: MPC — Multi-Business-Model Partner Sales & Onboarding Platform

Idea: MPC (Managed Print Central) is HP's partner-facing platform covering the full journey from pre-quote to contract onboarding. A single platform supports three distinct business models — CMPS, PMPS (Resell/Agent), and MP Flex — each with its own pricing, workflow, and contract rules, but sharing common infrastructure for catalog, CRM, and auth.

Why it matters: Supporting multiple business models on one platform avoids duplicating infrastructure and maintenance burden. The key design challenge is isolating model-specific logic (pricing rules, onboarding workflows, deal formats) while sharing core services. MPC demonstrates how enterprise platforms can scale across market segments without forking.

---

tags: #mpc

---


## Connections:

- [[TMC]] — MPC hands off won deals to TMC for contract and fleet onboarding
- [[ITSM ServiceNow]] — MPC triggers opportunity creation and receives contract provisioning callbacks
- [[MSCC]] — MPC provisions customers and users into the customer portal
- [[Broker]] — Won deal data flows through DMS/Broker for SAP and ITSM onboarding
- [[Paladin]] — MPC uses Paladin for authentication and token management
- [[Enablement Service]] — MPC queries ES for billing model, cost center, and contract data

## Functions
[[_Index]]