---
tags: [mpc, mpc/opportunity]
---

# 05 — Opportunity Management

An Opportunity represents a business deal in progress. Once won, it becomes a contract. One customer can have many opportunities; one opportunity can have many proposals.

## Key Behaviours

### Creating an Opportunity
- Navigate to **Opportunities tab → Create Opportunity**
- Required: Opportunity Name + existing Customer (type to search, or use pen icon dropdown)
- Inline customer creation: tick "Add Customer Now?" → fill in Opportunity Name, Customer Name, postcode → creates both simultaneously
- After creation, user is automatically redirected to the Proposal tab

### Opportunity Status Flow
```
Active ──────────── (90 days inactive) ──→ Abandoned (auto)
  │                                              ↑
  ├──→ Lost      (manual, with reason)     Reactivate
  └──→ Abandon   (manual, with reason)     (any time)
```

- **Auto-abandon**: opportunities not Won within 90 days automatically move to Abandoned
- **Manual status change**: Opportunities tab → Existing Opportunities → filter to "All" → Actions → "Set Opportunity to Abandon"
- Status update pop-up requires selecting Lost or Abandon via radio button + a reason from a dropdown
- **Reactivate**: Actions → "Reactivate Opportunity" → confirm in pop-up

### Opportunity Filter
- Default view shows **Active** opportunities only
- Toggle the filter switch to **All** to see active + abandoned/lost

### Relationship Rules
- One opportunity → many proposals
- When **one proposal is Won**, all other proposals in the opportunity are **frozen**
- Only one Add-on proposal can be Won at a time (see [[06_Proposal_Management]])

## Related Features
- [[04_Customer_Management]] — customer is the parent entity
- [[06_Proposal_Management]] — proposals live inside an opportunity
- [[02_User_Roles]] — re-assignment of opportunity to another Sales Rep

## Integration Points
None at opportunity level — integration happens at proposal Win (see [[13_Documents_and_Win]]).

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems