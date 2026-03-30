---
tags: [mpc, mpc/onboarding]
---

# 14 — Onboarding

Onboarding is the post-win process of activating the contract in downstream systems. It is triggered after a proposal is Won and is managed by the Account Manager. It connects the MPC customer record to DCC, activates devices, and sets up software solutions.

## Key Behaviours

### Trigger
- After a proposal is Won, the **Account Manager** assigned to the customer receives an email notification:
  - From: `MPCInfo@hp.com`
  - Subject: "New Customer Onboarding Task has been Assigned"
- A **Send Reminder** link is available in the Onboarding tab to re-send the notification if needed

### Onboarding Steps (in order)

| Step | Description |
|------|-------------|
| **1. Contacts** | Add/verify contact people for the customer. Contacts can be deleted. |
| **2. Locations** | Add/verify physical locations for the customer. |
| **3. Customer Information** | Verify customer details used in the contract (company name, billing info) |
| **4. Data Collector Setup** | Configure the Device Collection Agent (DCA) for the customer if required |
| **5. DCC Account Setup** | Create and link the customer's DCC (Device Control Center) account |
| **6. Device Onboarding** | Activate each device under the contract |
| **7. Software Onboarding** | Complete solution-level onboarding for software solutions |

### DCC Account Setup
- Creates a DCC account linked to the MPC customer
- **MPC → DCC address linkage**: MPC addresses are mapped to DCC
- **MPC → DCC contact linkage**: MPC contacts are mapped to DCC
- Shipping labels are generated as part of this process

### Device Onboarding
- Each device in the Proposed Fleet is activated in downstream systems
- Device-level activation

### Software Onboarding
- Each software solution in the proposal is activated
- Requires completing "Software Solution Onboarding Details" per solution

## Related Features
- [[04_Customer_Management]] — customer info used during onboarding
- [[15_Customer_Administration]] — contacts, locations, and DCA setup managed in customer account
- [[13_Documents_and_Win]] — win triggers onboarding task
- [[17_Integrations]] — DCC account linkage; TMC receives won deal for onboarding workflow
- [[02_User_Roles]] — Account Manager role receives the onboarding task

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| DCC | ← MPC | Customer account creation; address + contact linkage |
| TMC | ← MPC | Won deal information initiates onboarding workflow |
| ITSM (ServiceNow) | ← TMC/MPC | Contract and asset records created |
| DCA / Device Connect | ↔ MPC | Data collector configured for ongoing telemetry |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
