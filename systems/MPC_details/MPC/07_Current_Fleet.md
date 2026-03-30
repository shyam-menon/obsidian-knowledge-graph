---
tags: [mpc, mpc/fleet]
---
# 07 — Current Fleet

Current Fleet is an **optional** feature that captures the customer's existing device estate. It is used for cost analysis and to seed the Proposed Fleet. It does not have to be used — partners can go directly to Proposed Fleet.

## Key Behaviours

### Import Methods

| Method | Notes |
|--------|-------|
| **Manual** | Add devices one by one via UI |
| **Excel template** | Download template, populate, upload. Mandatory fields: Make, Model, Local Device (Yes/No). No special characters. |
| **DCA (Device Collector Agent)** | Requires DCA to be set up for the customer and Device Connect software installed and running for **minimum 24 hours** before import |

### DCA Import Specifics
- Validation result per device: **Valid** (can be imported, may have warnings) or **Invalid** (excluded)
- Invalid devices can be exported to a spreadsheet for analysis
- DCA-imported devices: location defaults to **"Unnamed Location"** — must be corrected before advancing to pricing
- DCA-imported devices: **average Monthly Page Volume cannot be edited** (other fields can be)
- Refreshing DCA data resets values to what DCA is currently reporting

### Current Costs
After importing, the **Current Costs** tab shows cost summary per device model:
- **Annual Supplies** (toner — street prices)
- **Annual Maintenance** (long-life consumables)
- **Annual Repair** (break-fix; single cost over fixed term — editable)
- **Soft Costs** (IT/Help Desk, material procurement, supplies management)
  - Default: 10% uplift on hard costs
  - Editable per device; "Apply to all Engines" copies changes to all devices

### Moving Devices to Proposed Fleet
- Current Fleet devices do **not** auto-flow to Proposed Fleet on the first proposal
- Use: select devices → **Actions → Move to Proposed Fleet → Go**
- For subsequent Add-on proposals within the same opportunity, devices **auto-carry** from the first proposal's Proposed Fleet

## Related Features
- [[08_Proposed_Fleet]] — destination for moved devices; core fleet design
- [[04_Customer_Management]] — DCA is set up within the customer account (see [[15_Customer_Administration]])
- [[15_Customer_Administration]] — DCA configuration lives under customer account

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| DCA (Device Connect) | → MPC | Device discovery data; must run 24h minimum |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems