---
tags: [mpc, mpc/settings]
---

# 16 — Partner Settings

Partner Settings covers user-level preferences, company-level configuration, deal notification setup, and user management. These settings affect behaviour across the platform and determine who receives automated notifications.

## Key Behaviours

### User Preferences
- Per-user settings (e.g., defaults, display preferences)
- Configurable by each individual user

### Company Details
- Partner-level configuration
- Includes the Preferred Premier Hardware Distributor for A3 products (set at partner setup time — affects pricing, see [[10_Pricing]])

### Deal Notifications
- **Deal Win Notifications**: list of recipients who receive the post-win deal confirmation email (including OPG number)
  - Path: **Account → Partner Details → Company → Deal Notifications**
- **Quote OPG Deal notifications**: same recipient list receives OPG confirmation on deal generation (see [[12_Quote_OPG_Deals]])
- Deal notification recipients are **in addition to** the deal submitter (who always receives the win email)

### Manage Users
- Admin function to view and manage all users in the partner organisation
- Shows users and their assigned roles

### Add User
- Add a new user to the MPC partner portal
- Triggers a registration email to the new user from `mpcinfo@hp.com` (see [[01_Access_and_Auth]])
- Role must be assigned: Administrator, Sales Representative, or Account Manager

## Related Features
- [[01_Access_and_Auth]] — Add User triggers the registration email flow
- [[02_User_Roles]] — roles assigned here determine what users can see and do
- [[12_Quote_OPG_Deals]] — deal notification recipients receive OPG confirmation emails
- [[13_Documents_and_Win]] — deal win notification recipients receive post-win emails
- [[10_Pricing]] — Preferred Premier Distributor configured here affects A3 hardware pricing

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| HP Account ID (HPID) | ← MPC | Registration email triggered on Add User |
| Paladin | ← MPC | Role assignments enforced at auth layer |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems