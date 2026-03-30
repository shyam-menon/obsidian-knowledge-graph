---
tags: [mpc, mpc/access]
---

# 01 — Access & Authentication

MPC access is controlled through HP Account ID (HPID). All partner users must register via an invitation email before they can use the portal.

## Key Behaviours

- New users receive a registration email from `mpcinfo@hp.com` with a registration link and a return link
- The registration link must be used for **initial account setup** before the return link is valid
- **Returning users**: enter HPID username → password → Sign In
- **First-time HPID users**: must create an HP Account ID first ("No HP account? Let's change that"), providing First Name, Last Name, Email, and Password
- On first MPC access, user must **accept the Terms of Use** — failure to accept results in "Authorization Failed" and registration does not complete
- Portal URL: `https://mpc-pro.ext.hp.com/`

## Related Features
- [[02_User_Roles]] — once authenticated, access is governed by role assignment
- [[16_Partner_Settings]] — Manage Users / Add User for provisioning new accounts

## Integration Points
| System               | Direction | What flows                           |
| -------------------- | --------- | ------------------------------------ |
| HP Account ID (HPID) | ← MPC     | Authentication credential validation |
| Paladin              | ← MPC     | Authorization/token management       |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems