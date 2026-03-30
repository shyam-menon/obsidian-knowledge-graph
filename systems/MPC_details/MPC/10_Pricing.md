---
tags: [mpc, mpc/pricing]
---

# 10 — Pricing

Pricing in MPC covers billing model selection, contract terms, the MPS device pricing table, hardware and accessories pricing, software pricing, and billing address configuration. All pricing feeds into the Pricing Summary which is included in generated documents.

## Key Behaviours

### Billing Information
- Under the **Billing Information tab**, select Bill To Address and Invoice To Address from addresses defined in Customer Details
- Multiple addresses can be selected if multiple exist
- Must be saved before documents can be generated

### Billing Model & Terms

**Billing Models** (availability varies by region/country):

| Model | Description |
|-------|-------------|
| Base + Click | Fixed base charge + per-click charge |
| Pay Per Click (PPC) | Pure per-click charge |
| Level Pay | Fixed monthly payment regardless of volume |
| Base + Supplies | Base charge covering supplies only |

- For **Add-on proposals**: Billing Model cannot be modified (inherits from original)
- Change billing model by selecting option and clicking Save in that section

**Proposal Terms**:

| Setting | Options |
|---------|---------|
| Payment Terms | Monthly or Quarterly |
| Contract Term Length | 12–60 months |
| Pricing Strategy | Account Series or Location Series |
| Proposal Validity Date | Until when prices are valid; included in the contract document |

### Pricing Summary
- Updates automatically as devices are added and pricing is entered
- Toggle between **Annual** and **Total** views
- Exportable via Export button
- Includes: MPS pricing, hardware, accessories, software

### MPS Pricing Table
- Lists each printer model with Mono and Colour pricing per device
- Columns vary by Billing Model (e.g., Base + Click shows base and click rates separately)
- **HP Click Cost**: HP's price charged to the Partner
- **Click Price** (Customer price): modifiable by partner — any change **triggers an exception** (see [[11_Exceptions]])
- The End Customer Price shown in the Proposal Document is the Click Price

### Hardware and Accessories Pricing Table
- Appears dynamically based on devices in the proposed fleet
- A3 devices → **Preferred Premier Hardware Distributor** pricing (set at partner setup)
- A4 devices → **Core Distributor(s)** pricing:
  - Single Core Distributor selected → that distributor's pricing
  - Multiple Core Distributors selected → country default pricing
- Click "+" next to a SKU to expand and show accessory pricing

**Pricing fields:**

| Field | Description |
|-------|-------------|
| Target Unit Device IBP | Price partner wants HP to consider; defaults to Unit Device IBP; modifying triggers exception |
| Unit Device IBP | HP's expected partner buy price through distribution |
| Total Net IBP | (Qty × IBP) + Accessories Sub Total |
| Target Acc IBP | Partner's target accessory price; defaults to Unit Acc IBP |

### Software Pricing Table
See [[09_Software_Management]] for software pricing calculation detail.

### Distributor Selection
- **A3 Premier Distributor**: set at partner setup time; visible by default when A3 devices are in the quote
- **A4 Core Distributor(s)**: partner chooses which core distributor(s) to buy from when A4 devices are selected
- Selecting a Core Hardware Distributor triggers Core Special Price OPGs via Eclipse (see [[12_Quote_OPG_Deals]])

## Related Features
- [[08_Proposed_Fleet]] — device list drives pricing tables
- [[09_Software_Management]] — software pricing table
- [[11_Exceptions]] — modifying Click Price or Target Unit IBP triggers exceptions
- [[12_Quote_OPG_Deals]] — distributor selection and approved exceptions drive OPG generation
- [[13_Documents_and_Win]] — Generate Document button activates once pricing is saved

## Integration Points
| System             | Direction | What flows                                              |
| ------------------ | --------- | ------------------------------------------------------- |
| PriceHub           | ↔ MPC     | OPG creation for hardware/supplies distributor ordering |
| Master Data / DART | → MPC     | IBP pricing, distributor pricing                        |
| Eclipse            | ← MPC     | OPG deal generation (via approved exception)            |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->


## Tags
#systems