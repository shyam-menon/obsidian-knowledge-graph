Title: Enablement Service — GraphQL Data Federation Layer

Idea: Enablement Service (ES) solves the N×M integration problem: instead of every application building its own connection to every data source (ITSM, K2, Usage Service), ES exposes a single GraphQL API that federates them all. Hasura + PostgreSQL caching handles ~1 million queries per day, and AWS Glue ETL preloads data into the cache so queries return quickly without hitting source systems on every request.

Why it matters: In complex ecosystems, data integration complexity grows quadratically if left unchecked. A federation layer reduces this to linear: each app talks only to ES, and each source publishes only to ES. Caching at the federation layer also isolates downstream systems from read traffic spikes. The combination of GraphQL (flexible querying) + Hasura (auto-generated APIs) + ETL preloading (performance) is a reusable pattern for any data-heavy platform.

Connections:

- [[ITSM ServiceNow]] — ITSM publishes fleet and asset data changes to ES via SNS
- [[UsageService]] — Usage Service publishes processed telemetry data to ES
- [[Fleet Operations]] — FleetOps queries ES for fleet data via GraphQL
- [[MSCC]] — MSCC queries ES for device, billing, and contract data for the customer portal
- [[MPC]] — MPC queries ES for cost center, billing model, and contract account information
- [[Paladin]] — ES uses Paladin for authentication and authorization on all requests

## Tags
#systems