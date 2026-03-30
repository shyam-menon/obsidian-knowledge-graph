---
tags: [mpc, mpc/proposal]
---
# 06 — Proposal Management

A Proposal is a version of an Opportunity that contains the proposed fleet and contract properties (billing model, term, pricing). Winning a proposal converts it into an HP MPS contract.

## Key Behaviours

### Creating a Proposal
- Navigate to **Proposal tab → Create Proposal**
- Required fields: Customer, Opportunity, **Program** (Managed Complete or Managed Page), **Contract Type** (New Business or Add-on), Proposal Description
- Won opportunities show as "Won – DD-MMM-YYYY" in the dropdown
- Add-on can only be selected if the opportunity is Won and has onboarded devices

### Proposal Types
| Program | Description |
|---------|-------------|
| **Managed Page (pMPS)** | Pay-per-page model |
| **Managed Complete (cMPS)** | Comprehensive managed service |
| **Managed Supplies** | Supplies-only managed service |

### Contract Types
| Type | Rules |
|------|-------|
| **New Business** | Fresh contract; sets coterminous flag |
| **Add-on** | Extends an existing won contract; Billing Model and Coterminous **cannot** be modified |

### Coterminous Setting (New Business only)
- **Coterminous** (ticked): every Add-on for this opportunity ends at the same date as the original proposal's end date
- **Non-Coterminous** (unticked): every Add-on runs for the same number of months as the original proposal's term
- Availability depends on country configuration

### Multiple Add-ons
- Multiple Add-ons can exist simultaneously in MPC but **only one can be Won at a time**
- Recommendation: create Add-ons one by one; do not have multiple In Progress Add-ons

### cMPS Customer Warning
- Creating a pMPS proposal against a customer set up for cMPS triggers a pop-up warning to update customer profile first

### Proposal Freeze on Win
- When one proposal is Won, **all other proposals in that opportunity are frozen**

### Proposal Details Tabs

| Tab | Purpose |
|-----|---------|
| **Summary** | Customer, opportunity, proposal details; Source ID/Source Customer Name |
| **Linked Proposals** | Parent/child proposals (from exception copy-and-submit flow) |
| **Activity Log** | Full audit trail with date and user; exportable |
| **Notes** | Free-text notes with date and creator; exportable |
| **Action** | Change opportunity status; re-assign to Sales Rep; Copy Proposal |

### Copy Proposal
- Creates a new proposal with a new Proposal ID
- Used before submitting exceptions (recommended) to maintain a working copy

## Related Features
- [[05_Opportunity_Management]] — proposal lives inside an opportunity
- [[07_Current_Fleet]] — optional current fleet feeds into proposal
- [[08_Proposed_Fleet]] — core fleet design at proposal level
- [[09_Software_Management]] — software solutions added at proposal level
- [[10_Pricing]] — billing model and pricing set at proposal level
- [[11_Exceptions]] — exception requests raised from proposal
- [[13_Documents_and_Win]] — document generation and win finalisation
- [[14_Onboarding]] — triggered after proposal win

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| TMC | ← MPC | Won deal information sent for contract onboarding |
| DART / Deal Configuration Service | ↔ MPC | Master data for PMPS/CMPS/MP Flex; TTSAP package creation |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
