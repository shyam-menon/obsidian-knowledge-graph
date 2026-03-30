---
tags: [mpc, mpc/fleet]
---

# 08 — Proposed Fleet

The Proposed Fleet is the **core of the proposal** — it defines all devices that will be under contract, their locations, and the SLAs that apply to each location. Pricing is calculated based on what is in the Proposed Fleet.

## Key Behaviours

### Adding Devices

| Method | Notes |
|--------|-------|
| **Manual** | Add Device Manually button; HP models only; one model at a time with qty |
| **Excel import** | Download template; mandatory fields: Make, Model, Qty, New HW (Yes/No), Local Device, Monthly Mono/Colour usage, Location Name, Post Code, City |
| **HP Product Configurator** | Configurator link per device via the "Managed By Configurator" tab |

### Device Attributes (Manual Add)
- **Device condition**: New Hardware or Installed Base — affects pricing fields and exception triggers
- **Target Partner Price**: only available for New Hardware; defaults to Indicative Buy Price (IBP); modifying it triggers an exception
- **HP Installation of Hardware**: if checked, HP is responsible for installation and costs are added to the quote
- **Local device**: network-connected (No) vs USB-connected (Yes)
- **Monthly Mono/Colour Page Volume**: if changed to > 150% of HP default, a warning is shown and HP Account Manager approval is required

### EOSL (End of Service Life) Handling
Devices flagged EOSL have an end-of-service date within the contract term. Three options:
1. Remove the device from the proposed fleet
2. Submit an exception to support the device for the full term (see [[11_Exceptions]])
3. Shorten the contract term (minimum 12 months) so it fits within the EOSL date

### Fleet Views
| Tab | Shows |
|-----|-------|
| Managed By Model | New HW flag, Supported / Unsupported / EOSL status |
| Managed By Location | Devices grouped per location |
| Managed By Configurator | Links to HP Configurator per device |

### Locations and SLA
- Locations must have devices assigned before they appear in the Fleet Locations Summary
- Address Line 1 and 2: **40 character maximum** (country-dependent)
- SLA is assigned **per location** — click current SLA option to see alternatives and update
- Locations entered here also appear under Customer Locations in Customer Details

## Related Features
- [[07_Current_Fleet]] — source of devices moved into Proposed Fleet
- [[10_Pricing]] — device list drives the MPS Pricing Table and hardware/accessories tables
- [[11_Exceptions]] — unsupported devices, New HW discounts, and EOSL trigger exceptions
- [[09_Software_Management]] — software solutions sit alongside the fleet at proposal level

## Integration Points
| System | Direction | What flows |
|--------|-----------|------------|
| HP Product Configurator | ↔ MPC | Device configuration for A3/A4 SKUs |
| Master Data / DART | → MPC | Supported device list, EOSL dates, IBP pricing |

## Requirements
<!-- Obsidian backlinks will auto-populate here -->
