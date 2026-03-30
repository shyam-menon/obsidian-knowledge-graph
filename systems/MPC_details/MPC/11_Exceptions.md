---
tags: [mpc, mpc/exceptions]
---

# 11 — Exceptions

Exceptions are requests sent to HP for review when a proposal contains something outside standard parameters — either because the partner requests special treatment, or because the system detects a non-standard condition automatically.

## Key Behaviours

### Exception Types

**Manually initiated** (from Exceptions tab in proposal):

| Exception Type | Trigger |
|----------------|---------|
| Credit check | Partner requests credit review |
| Legal terms | Non-standard legal terms required |
| Multi-country | Deal spans multiple countries |
| Payment terms | Non-standard payment terms |
| SLA — Break Fix | Non-standard break-fix SLA |
| SLA — Preventive Maintenance | Non-standard PM SLA |
| SLA — Supplies Management | Non-standard supplies SLA |
| Special Pricing | Below-standard MPS click pricing |
| Non-automatic extension | Contract extension outside standard auto-renewal |
| Extend Proposal/Contract Validity | Extend beyond standard validity window |
| Fleet & SLA Optimisation | Changes to fleet or SLA after approval |
| Price Revision | Revise previously approved prices |
| Data Collector Not Required | Waive DCA requirement |

**System-generated** (triggered automatically):

| Condition | Exception |
|-----------|-----------|
| Unsupported device in Proposed Fleet | Unsupported device exception |
| New HW additional discount % entered (in pricing or Edit Device) | New Hardware discount exception |

### Submission Process

**Option A — Copy & Submit (recommended):**
1. Click **"Copy and Submit Exceptions to HP"**
2. Edit the copy name in the pop-up → click **Copy and Submit**
3. A **child copy** of the proposal is created and remains editable
4. The **original proposal** is frozen ("Pending HP Review")
5. If the exception is rejected, the copy retains all work done

**Option B — Submit only:**
1. Click **"Submit Exception to HP"**
2. The **entire proposal** is frozen pending HP review
3. No working copy — if rejected, work must be re-done

### Partner Justification Rules
- Required for each exception request
- Maximum **500 characters**
- Blocked special characters: `% # < > / \ ;` — MPC will warn if these are entered

### HP Response Statuses
| Status | Outcome |
|--------|---------|
| **HP Approved** | New Proposal number generated; linked to original; pricing may be updated |
| **HP Alternate Approved** | New Proposal number generated; alternative price approved; partner reviews alternative |
| **HP Rejected** | Proposal number unchanged; partner can edit and resubmit |

- On Approved or Alternate Approved: partner receives an email with the new Proposal number
- **Exception quote validity: 90 days from approval date** — proposal must be Won within this window

### Editing an Approved Proposal
- Click **"Move to In Progress"** to revert to editable state
- Status becomes **"Approved in Progress"** or **"Alternate In Progress"**
- Approved pricing is retained
- If devices/page count/quantity/term/billing model are changed → must **re-submit** to HP for additional approval
- This cycle can repeat multiple times
- For **HP Rejected** proposals: Move to In Progress restores full editing + option to resubmit

## Related Features
- [[10_Pricing]] — special pricing and HW discount exceptions originate from pricing changes
- [[08_Proposed_Fleet]] — unsupported devices and EOSL devices trigger exceptions
- [[12_Quote_OPG_Deals]] — approved HW exceptions trigger OPG generation for pMPS
- [[13_Documents_and_Win]] — Win tab notes if re-submission is needed; proposal must be Won within 90 days

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| HP Pricing Team | ↔ MPC | Exception review and approval/rejection |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
