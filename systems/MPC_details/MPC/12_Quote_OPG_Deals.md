---
tags: [mpc, mpc/opg]
---

# 12 — Quote OPG Deals

OPGs (Opportunity Pricing Groups) are pricing deals created in Eclipse that allow partners to order hardware through distribution at approved prices. MPC triggers OPG creation when a special pricing exception is approved and contains New Hardware.

## Key Behaviours

### When OPGs Are Generated
- Triggered when an exception returns **HP Approved** or **HP Alternate Approved** AND the exception contains **New HW & Accessories**
- For **pMPS deals only** — other exception types (no HW component) do not trigger OPGs
- The "Request Quote Deal(s)" button appears on the proposal:
  - **Active** (green): customer lookup is complete
  - **Inactive** (greyed, with tooltip): customer lookup not yet performed — must complete first

### OPG Lifecycle
```
Exception Approved (with HW) → [Partner clicks "Request Quote Deal(s)"]
  → OPGs created in Eclipse with status: Quoted
  → [Proposal is Won]
  → OPGs converted to status: Won
```

### Deal Confirmation Email
On OPG generation, Partner + Deal recipients receive an email containing:
- Deal description
- Deal number
- Status
- Deal End date

Deal recipients are configured at: **Account → Partner Details → Company → Deal Notifications** (see [[16_Partner_Settings]])

### Viewing OPGs
- View in MPC via the **"Display Eclipse Deal"** section — shows same details as the confirmation email

### Expiration Handling
- **7 days before** the Quote Validity End date → expiration alert email sent to partner
- If partner lets the deal **expire** then resubmits a new exception → **new OPG numbers** generated
- If partner acts **before expiry** → same OPG numbers retained, with a new version and updated pricing/SKUs

### Re-Submission Behaviour
- Partner can resubmit a special price exception even after triggering Quote OPGs
- On new HP Approval → partner clicks "Request Quote Deal(s)" again
- New Quote OPGs retain the **same number** as previous ones but with a **new version**
- New pricing and any new SKUs are applied

### Add-on OPG Behaviour
- If the **original pMPS deal had no New HW** but the **Add-on does** → MPC has no pre-existing Won OPG and will allow Quoted OPG generation for the Add-on

### Core Distributor OPGs
- Selecting a Core Hardware Distributor for A4 products triggers **Core Special Price OPGs** via MPC/Eclipse (see [[10_Pricing]])

## Related Features
- [[11_Exceptions]] — OPGs only generated when exception is approved and contains HW
- [[10_Pricing]] — distributor selection affects OPG type; approved exception pricing reflected in OPG
- [[16_Partner_Settings]] — deal notification recipients configured here
- [[13_Documents_and_Win]] — OPG number included in win notification email

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| Eclipse | ← MPC | OPG deal creation request |
| Eclipse | → MPC | OPG deal status, deal number, validity dates |
| PriceHub | ↔ Eclipse/MPC | Distributor ordering against OPG |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems