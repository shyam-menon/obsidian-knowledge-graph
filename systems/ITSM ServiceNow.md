Title: ITSM ServiceNow — Asset & Contract Lifecycle Management with IMACD

Idea: ITSM (ServiceNow) is the central system of record for all hardware assets, software licenses, and contracts across MPS and MDS accounts. Every change to an asset or contract is modelled as an IMACD operation — Install, Move, Add, Change, or Delete — expressed as a catalogued service request that triggers automated workflows through SAP and downstream systems.

Why it matters: IMACD gives every asset change a formal structure: a vocabulary, a workflow, an audit trail, and an integration trigger. This means asset changes are never ad-hoc — they are always trackable, automatable, and reversible. The model is broadly applicable to any domain requiring structured IT asset lifecycle management at enterprise scale.

Connections:

- [[Broker]] — ITSM receives account and fleet data from Broker during onboarding
- [[TMC]] — TMC feeds deal and transition context into ITSM via Broker
- [[MSCC]] — ITSM broadcasts device and fleet data changes to DCC via SNS
- [[Enablement Service]] — ITSM publishes fleet updates to Enablement Service for cross-system consumption
- [[CARD]] — ITSM asset data contributes to CARD profitability reporting