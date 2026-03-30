---
tags: [mpc, mpc/customer]
---
# 04 — Customer Management

The Customer is the **top-level entity** in MPC. Everything (Opportunities, Proposals, Contracts) hangs off a Customer record. Getting customer details right is critical because they drive what appears in the HP database on contract win.

## Key Behaviours

### Creating a Customer
- Navigate to **Customers tab → Create Customer**
- Required: Customer Name + valid postcode (format must match the partner's registered country)
- After creation, user is automatically redirected to the Opportunity tab
- Alternative: create a customer inline during Opportunity creation (see [[05_Opportunity_Management]])

### Source ID and Source Customer Name
- These fields link the MPC customer to an existing record in the HP database
- If populated → the contract on win is created under that existing HP customer record
- If empty → **a new customer record is created** in the HP database at onboarding time
- Source ID is HP-internal; Source Customer Name is visible to partners in Proposal Details

### MDM Lookup
- Some flows require a customer lookup against MDM (Master Data Management)
- If customer is not found: "Request customer add to MDM" action is available
- The **Lookup Original MSID** button appears in proposal Documents when customer lookup has not been performed

### Address Constraints
- Address Line 1 and Address Line 2: **40 character maximum** (may differ by country)
- Multiple Bill To and Invoice To addresses are supported
- Addresses set here are available when selecting billing addresses in Proposal Pricing

### cMPS vs pMPS Customers
- If a customer was created for a **cMPS (Managed Component)** deal and a pMPS proposal is created against them, MPC shows a **pop-up warning** prompting the user to update the customer profile before proceeding

## Related Features
- [[05_Opportunity_Management]] — customer is the parent of all opportunities
- [[06_Proposal_Management]] — Source ID/Name appear in Proposal Details
- [[14_Onboarding]] — customer info used during onboarding steps
- [[15_Customer_Administration]] — customer account management (contacts, locations, DCA)
- [[17_Integrations]] — MDM lookup, ITSM customer record creation on win

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| MDM | ↔ MPC | Customer lookup / request to add |
| ITSM (ServiceNow) | ← MPC | New customer record created on onboarding if Source ID empty |
| DCC | ← MPC | Customer address and contact linkage during onboarding |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
