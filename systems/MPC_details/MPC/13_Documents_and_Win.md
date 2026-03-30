---
tags: [mpc, mpc/win]
---

# 13 — Documents & Win

Document generation and the Win process are the final steps of the sales journey. Winning a proposal triggers contract creation in HP systems and kicks off the onboarding workflow.

## Key Behaviours

### Document Generation

**Generate Document button is active only when:**
- Devices have been added to the proposal
- Pricing has been selected and saved
- Proposal is **not** in "Pending HP Review" status

**Document types:**

| Document | Audience | Notes |
|----------|----------|-------|
| Proposal | Customer-facing | Reflects End Customer pricing |
| Contract | Partner rate sheet | Must be signed and uploaded before Win |

- Both documents are available in **local language** and **English**
- If customer lookup has not been performed, a **"Lookup Original MSID"** button appears below the Generate Document button

### Pre-Win Validation (Win Tab)
- The **Win tab** lists all missing required information before the proposal can be Won
- Each item is linked — click to navigate directly to the incomplete section
- Common blockers: missing billing address, unsigned contract, unresolved exception re-submission requirement
- If devices/quantities/term/billing model were changed on an approved proposal → Win tab will note that re-submission to HP is required

### Winning the Proposal
1. Complete all items flagged in the Win tab
2. **Upload the signed contract** (mandatory)
3. Click **"Win Proposal"**
4. Confirmation message displayed

### Post-Win Notifications

| Recipient | From | Subject |
|-----------|------|---------|
| Account Manager assigned to customer | MPCInfo@hp.com | "New Customer Onboarding Task has been Assigned" |
| Deal submitter + Deal Win Notification recipients | MPCInfo@hp.com | Deal Confirmation for Customer (Partner) — includes OPG number |

Deal Win Notification recipients are configured in [[16_Partner_Settings]].

### Post-Win System Effects
- All other proposals in the opportunity are **frozen**
- Won deal information is sent to **TMC** to trigger the contract onboarding workflow
- Quote OPGs (if any) transition from **Quoted → Won** status in Eclipse (see [[12_Quote_OPG_Deals]])
- Onboarding task becomes available to the Account Manager (see [[14_Onboarding]])

## Related Features
- [[06_Proposal_Management]] — proposal must be fully built before documents can be generated
- [[11_Exceptions]] — exception status can block the Win tab (re-submission required)
- [[12_Quote_OPG_Deals]] — OPG number included in win confirmation email; OPG status changes on win
- [[14_Onboarding]] — immediately follows a successful win
- [[16_Partner_Settings]] — deal win notification recipients

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| TMC | ← MPC | Won deal package sent for contract onboarding |
| Eclipse | ← MPC | Signal to convert Quoted OPGs to Won OPGs |
| DART / Deal Config Service | ← MPC | TTSAP package creation |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
