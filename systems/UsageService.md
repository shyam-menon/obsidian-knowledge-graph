Title: Usage Service — Telemetry Processing Engine Driving Replenishment & Billing

Idea: Usage Service is the intelligence layer that transforms raw device telemetry — meter readings, supply levels, print counters from JAM and FM Audit — into three types of downstream actions: auto-replenishment orders (via Fulfillment Service), billing data (via Convergent Mediation), and operational dashboards (via DCC and FleetOps). Built as a microservices system (Usage Service 2.0) with a plug-in architecture for onboarding new business models.

Why it matters: Telemetry data is only as useful as what you do with it. Usage Service closes the loop between device state and business outcomes — supplies are ordered before devices run dry, billing reflects actual usage rather than estimates, and support teams see live fleet health. The plug-in architecture means new billing or replenishment models can be added without rewriting the core.

Connections:

- [[Device Connectivity]] — Usage Service receives raw telemetry from JAM, FM Audit, and other collectors
- [[Fulfillment Service]] — Usage Service triggers replenishment orders when supply thresholds are crossed
- [[Fleet Operations]] — Usage Service and FleetOps exchange device data and operational commands
- [[Enablement Service]] — Usage Service publishes processed data to ES for cross-system consumption
- [[Paladin]] — Usage Service uses Paladin for authentication and authorization

## Tags
#systems