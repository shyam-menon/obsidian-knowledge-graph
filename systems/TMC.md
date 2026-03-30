Title: TMC — Post-Sale Contract & Fleet Onboarding System

Idea: TMC (Transition Management Central) takes ownership after a deal is won. It manages the structured process of onboarding contracts, accounts, devices, and sites into the service delivery ecosystem. It is the formal handoff point between the sales world (deals and quotes) and the operational world (assets, billing, and service delivery).

Why it matters: The sales-to-operations handoff is one of the highest-risk moments in enterprise service delivery — incomplete or incorrect data here causes billing errors, missed SLAs, and customer dissatisfaction. TMC formalizes this handoff with tracked workflows, Master Agreement management, and downstream triggers to ITSM and SAP via Broker.

Connections:

- [[MPC]] — TMC receives won deal information from MPC to initiate onboarding
- [[Broker]] — TMC delegates system-to-system orchestration (ITSM, SAP) to Broker
- [[ITSM ServiceNow]] — TMC feeds contract and account data into ITSM for asset management
- [[DMS]] — DMS generates the TTSAP package that TMC uses for MP Flex onboarding

## Tags
#systems