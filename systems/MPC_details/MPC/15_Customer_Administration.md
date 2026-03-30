---
tags: [mpc, mpc/customer]
---

# 15 — Customer Administration

Customer Administration is the management of all persistent details on a Customer record — contacts, addresses, locations, cost centres, and the Device Collection Agent setup. These details feed into proposals, onboarding, and downstream systems.

## Key Behaviours

### Account Information
- **Source ID**: HP internal identifier linking to an existing HP database customer record
- **Source Customer Name**: the customer name as it appears in the HP database
- If Source ID and Name are empty → a new customer is created in HP database at onboarding

### Main Contact Information
- Primary contact person for the customer
- Used in onboarding and contract documentation

### Addresses
- **Bill To Address**: where invoices are billed
- **Invoice To Address**: where invoices are sent
- **Multiple addresses** supported — all become available for selection in Proposal Pricing (see [[10_Pricing]])
- Address Line 1 and 2: 40 character maximum (country-dependent)

### Opportunities Tab
- Shows all opportunities associated with the customer
- Provides a view of the full deal history for that customer

### Locations
- Physical locations for the customer (sites, offices)
- Locations entered in Current Fleet or Proposed Fleet also appear here
- Cannot have duplicate location names for the same customer

### Cost Centres
- Customer cost centres can be configured here
- Used for billing and reporting allocation

### Device Collection Agent (DCA)
- The DCA is set up within the customer account
- Required for: discovery of current fleet devices (see [[07_Current_Fleet]]) and ongoing device telemetry
- DCA setup page shows the configuration and connection status of the Device Connect software

## Related Features
- [[04_Customer_Management]] — customer creation and Source ID/Name
- [[07_Current_Fleet]] — DCA used to import current fleet devices
- [[14_Onboarding]] — contacts and locations used during onboarding steps
- [[10_Pricing]] — addresses available for billing address selection in proposals

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| DCA (Device Connect) | ↔ MPC | Agent configuration; device discovery |
| ITSM | ← MPC | Customer record (via Source ID / Source Customer Name) |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
