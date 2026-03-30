---
tags: [mpc, mpc/users]
---

# 02 — User Roles

MPC has three partner portal roles that control what a user can see and do within the platform.

## Key Behaviours

| Role | Scope |
|------|-------|
| **Administrator** | Full access to all customers and opportunities |
| **Sales Representative** | Access to their own customers and opportunities |
| **Account Manager** | Access only to customers where they are the assigned Account Manager |

- A **quote can be re-assigned** to another user — but only to a user with the **Sales Representative** role
- The original creator of a quote **retains access** if they hold the Administrator role
- On re-assignment, a notification email is triggered to the new user:
  - From: `MPCInfo@hp.com`
  - Subject: "New quote for customer 'XXX' has been assigned to you"
- After a proposal is **Won**, the assigned Account Manager receives an onboarding task notification (see [[14_Onboarding]])

## Related Features
- [[01_Access_and_Auth]] — registration and HPID setup
- [[16_Partner_Settings]] — user provisioning (Manage Users / Add User)
- [[05_Opportunity_Management]] — re-assignment happens at opportunity/proposal level
- [[14_Onboarding]] — AM receives post-win onboarding task

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| Paladin | ← MPC | Role-based access enforcement |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems