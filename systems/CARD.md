Title: CARD — Deal Profitability & Installed Base Financial Reporting

Idea: CARD (Customer Account Reporting Database) is the financial intelligence system for MPS and MDS contracts. It ingests revenue, cost, and usage data from SAP, ITSM, K2, and DART on a monthly basis to produce P&L views per deal — broken down by hardware, supplies, services, and lease — across EMEA, AMS, and APJ regions. It also tracks TCV-to-revenue conversion and technician time.

Why it matters: Without a unified profitability view, account managers make renewal and margin recovery decisions based on partial data from siloed systems. CARD creates a single source of truth for deal financial health, enabling proactive margin management, contract renewal planning, and forecasting before contracts expire.

Connections:

- [[DMS]] — DMS sends MP Flex deal details to CARD for profitability tracking
- [[ITSM ServiceNow]] — ITSM asset and contract data informs CARD's installed base calculations
- [[MPC]] — MPC deal data (via DART) flows into CARD as the signed deal log
- [[Paladin]] — CARD web application uses Paladin for authentication

## Tags
#systems