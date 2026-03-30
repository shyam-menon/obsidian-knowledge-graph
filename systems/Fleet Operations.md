Title: Fleet Operations — Internal Remote Device Management Console

Idea: Fleet Operations (FleetOps) is HP's internal tool for support teams to manage contracted devices without an on-site visit. From a single console, technicians can reboot devices, deploy firmware, set consumable thresholds, view incident history, and trigger alerts — by connecting to JAM/SDS for device access and the usage telemetry stack for live and historical data.

Why it matters: Remote device management cuts service cost and response time by eliminating unnecessary field visits. Centralising diagnostics, configuration, and alerting in one tool means support teams can resolve issues proactively — often before the customer notices — directly contributing to the uptime SLAs that define managed print contracts.

Connections:

- [[UsageService]] — FleetOps exchanges usage and telemetry data with Usage Service
- [[ITSM ServiceNow]] — FleetOps reads asset and contract context from ITSM; incidents are logged back
- [[Device Connectivity]] — FleetOps performs remote operations via JAM and SDS
- [[MSCC]] —  FleetOps and DCC share fleet data so internal and customer views stay in sync
- [[Enablement Service]] — FleetOps queries ES for fleet data via GraphQL

## Tags
#systems