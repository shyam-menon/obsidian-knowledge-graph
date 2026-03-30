---
tags: [mpc, mpc/integrations]
---

# 17 — Integrations

This note maps MPC's external integration points — which systems MPC connects to, the direction of data flow, and when each integration is triggered during the user journey.

## Integration Map

### DCC (Device Control Center)
- **When**: During [[14_Onboarding]] (DCC Account Setup step)
- **What flows**:
  - MPC customer **addresses** → DCC (address linkage)
  - MPC customer **contacts** → DCC (contact linkage)
  - DCC account is **created** and linked to the MPC customer record
- **Purpose**: Enables the customer to manage their fleet through DCC post-onboarding

### TMC (Transition Management Central)
- **When**: After [[13_Documents_and_Win]] (proposal is Won)
- **What flows**: Won deal information package sent to TMC
- **Purpose**: TMC orchestrates the contract onboarding workflow → ITSM + SAP record creation

### Eclipse / OPG System
- **When**: After an exception is approved with New HW (see [[12_Quote_OPG_Deals]])
- **What flows**: OPG deal creation request → Eclipse returns deal number, status, validity dates
- **Purpose**: Enables partner to order hardware through distribution at approved prices via PriceHub

### MDM (Master Data Management)
- **When**: During [[04_Customer_Management]] (customer lookup)
- **What flows**: Customer lookup query; "Request add to MDM" if not found
- **Purpose**: Ensures customer records are aligned with HP's master data before contract creation

### DCA / Device Connect
- **When**: During [[07_Current_Fleet]] (current fleet import) and [[15_Customer_Administration]] (DCA setup)
- **What flows**: Device discovery data → MPC; must run for minimum 24 hours before import is possible
- **Purpose**: Automated discovery of customer's installed device estate

### DART / Deal Configuration Service
- **When**: During quoting (master data) and on Win (TTSAP package creation)
- **What flows**:
  - → MPC: Master data for PMPS/CMPS (DART) and MP Flex (Deal Config Service) deals
  - ← MPC: TTSAP package created on win for downstream contract processing
- **Purpose**: Source of truth for deal configuration and downstream billing setup

### PriceHub
- **When**: OPG creation for hardware/supplies distributor ordering
- **What flows**: OPG pricing data; distributor ordering capability
- **Purpose**: Partners use PriceHub to order hardware/supplies from distributors against approved OPGs

### HP Dynamics / Apollo
- **When**: Deal management and sales process
- **What flows**: Deal and opportunity data
- **Purpose**: CRM system integration for deal tracking

### MS4 / SAP
- **When**: Post-win contract processing (via TMC/Broker)
- **What flows**: Contract and billing data
- **Purpose**: Billing and contract record creation in HP finance systems

### System Email (mpcinfo@hp.com)
Automated notification emails sent by MPC:

| Trigger | Recipients | Subject |
|---------|------------|---------|
| New user added | New user | Registration link |
| Quote re-assigned | New assignee | "New quote for customer 'XXX' has been assigned to you" |
| Proposal Won | Account Manager | "New Customer Onboarding Task has been Assigned" |
| Proposal Won | Deal submitter + win recipients | Deal Confirmation (includes OPG number) |
| Exception approved | Partner | New Proposal number notification |
| OPG generated | Partner + Deal recipients | Deal description, number, status, end date |
| OPG expiry (7 days prior) | Partner | Expiration alert |

### Support
- Partner support: `mssupport@hp.com` / `www.mssupport.hp.com`

## Related Features
- [[04_Customer_Management]] — MDM lookup
- [[07_Current_Fleet]] — DCA import
- [[12_Quote_OPG_Deals]] — Eclipse OPG integration
- [[13_Documents_and_Win]] — TMC and DART integration triggered on Win
- [[14_Onboarding]] — DCC account linkage
- [[15_Customer_Administration]] — DCA setup

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
