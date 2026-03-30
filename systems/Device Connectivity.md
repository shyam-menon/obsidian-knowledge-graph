Title: Device Connectivity — IoT Pipeline for Print Fleet Data Collection

Idea: The device connectivity layer is composed of four components that work in sequence: FM Audit Server collects raw data from networked printers on-site, Stratus provisions devices into the IoT mesh and maintains a Device Shadow (virtual representation for remote management even when offline), JAM handles device registration, credential management, and remote diagnostics, and SDS provides cloud-based monitoring with ML-driven predictive analytics. Together they form the pipeline from physical device to cloud telemetry.

Why it matters: Without a reliable device connectivity layer, all telemetry-driven features — auto-replenishment, usage billing, remote diagnostics — cannot function. Each component in the stack has a single responsibility (collect, provision, manage, analyse), and failure at any layer degrades the entire pipeline. The Device Shadow pattern is particularly valuable: it decouples remote management commands from the device needing to be online at that moment.

Connections:

- [[UsageService]] — Telemetry collected by FM Audit and JAM flows into Usage Service for processing
- [[Fleet Operations]] — FleetOps uses JAM and SDS for remote device operations and diagnostics
- [[MPC]] — MPC triggers device registration and de-registration in JAM during onboarding
- [[Paladin]] — Device services use Paladin for authentication

## Tags
#systems