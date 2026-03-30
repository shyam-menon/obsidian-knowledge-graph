Title: Broker — Durable Workflow Orchestration Across Enterprise Systems

Idea: Broker is a workflow management service built on Temporal, an open-source durable workflow engine. It acts as the central orchestrator between TMC, ITSM, MPC, and SAP — ensuring each onboarding step (account creation, fleet push, contract setup) completes reliably. If a downstream system is temporarily unavailable, Temporal resumes the workflow exactly where it left off.

Why it matters: Enterprise integrations between multiple systems fail silently and partially. A durable workflow engine guarantees that workflows either complete fully or resume correctly — there is no silent data loss or stuck half-onboarded account. Temporal also provides visibility into in-flight workflows, making debugging and auditing straightforward.

Connections:

- [[TMC]] — Broker receives deal and transition data from TMC to orchestrate
- [[ITSM ServiceNow]] — Broker pushes account, fleet, device, and contract data into ITSM
- [[DMS]] — DMS feeds MP Flex deal packages that Broker processes for onboarding
- [[Paladin]] — Broker uses Paladin for service-to-service authentication

## Tags
#systems