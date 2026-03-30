Title: MSCC— Customer Self-Service Portal for Fleet Management

Idea: MSCC ( formerly Device Control Center) is the customer-facing web portal where customers and partners manage their contracted print fleet. It provides a single interface for viewing real-time device status on maps, requesting break-fix service calls, ordering supplies, and managing fleet settings — aggregating data from multiple backend systems into a coherent, role-appropriate view.

Why it matters: Self-service portals reduce support overhead while improving customer satisfaction. MSCC demonstrates how a portal can serve as an abstraction layer — customers interact with one surface while the platform quietly coordinates ITSM, Usage Service, and Enablement Service behind the scenes. The customer never needs to know which backend system owns which data.

Connections:

- [[ITSM ServiceNow]] — DCC receives fleet and device data updates from ITSM via SNS events
- [[MPC]] — MPC provisions customers and users into DCC during contract onboarding
- [[UsageService]] — DCC queries Usage Service for device telemetry and supply levels
- [[Enablement Service]] — DCC queries ES for fleet, billing, and contract data via GraphQL
- [[Fleet Operations]] — FleetOps and DCC share fleet data bidirectionally for internal and customer views