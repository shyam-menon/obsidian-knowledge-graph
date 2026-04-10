
---

## 1. What is SRS vs STS (at HP)?

### ✅ **SRS – Security Architecture Review Services**

**What it is**

- A **design‑time review** of your application or product architecture
- Evaluates **how security is built into the solution**, not whether it’s exploitable yet

**Focus areas**

- High‑level and detailed architecture
- Trust boundaries, data flows, identities
- AuthN/AuthZ model, secrets handling, encryption
- Cloud configuration posture
- Third‑party dependencies
- AI/ML, data, and privacy controls (if applicable)

**Key characteristics**

- Happens **early (“shift‑left”)**
- Uses architecture diagrams + questionnaires
- Produces **security requirements & design gaps**
- May explicitly state **whether STS is required**

**From HP Cybersecurity material**

> _“Security Architecture Review Services (SRS): security review of your application or product architecture to identify security weaknesses and vulnerabilities in the architecture/design.”_ [[1_SRS STS..._Finalized | PowerPoint]](https://hp.sharepoint.com/teams/HPICSPS/_layouts/15/Doc.aspx?sourcedoc=%7B1180BD43-CE1B-490C-83FE-FD37E289D0E5%7D&file=1_SRS%20STS%20Bootcamp%20CW_032624_v3.2.2_Finalized.pptx&action=edit&mobileredirect=true&DefaultItemOpen=1)

---

### ✅ **STS – Security Testing Services**

**What it is**

- **Hands‑on testing** of a running application
- Validates whether real vulnerabilities can be **exploited**

**Focus areas**

- Dynamic testing, manual testing
- Pen‑testing techniques
- API testing
- External attack surface validation
- Automated & manual vulnerability discovery

**Key characteristics**

- Requires a **deployed/testable environment**
- Typically **pre‑production**
- Produces **findings with severity ratings**
- Often mandatory for **internet‑facing solutions**

**From HP Cybersecurity material**

> _“Security Testing Services (STS): security testing of the application or product using automated and manual methods to identify potential security vulnerabilities that may be exploited by an attacker.”_ [[1_SRS STS..._Finalized | PowerPoint]](https://hp.sharepoint.com/teams/HPICSPS/_layouts/15/Doc.aspx?sourcedoc=%7B1180BD43-CE1B-490C-83FE-FD37E289D0E5%7D&file=1_SRS%20STS%20Bootcamp%20CW_032624_v3.2.2_Finalized.pptx&action=edit&mobileredirect=true&DefaultItemOpen=1)

---

## 2. Core Differences — Side‑by‑Side

|Dimension|**SRS**|**STS**|
|---|---|---|
|Primary intent|Design risk identification|Exploit & vulnerability discovery|
|When|Early (design / major change)|Late (test / pre‑prod)|
|Input|Architecture diagrams, flows|Running application|
|Output|Security requirements, gaps|Vulnerability findings|
|Mandatory|**Yes – for all HP solutions**|Conditional|
|Environment needed|❌ No|✅ Yes|
|“Shift Left”|✅ Strong|❌ No|

---

## 3. How is it Determined: SRS or STS?

### ✅ Rule #1 (Hard rule at HP)

> **Every solution requires SRS.**  
> There is **no scenario** where SRS is skipped.

This is explicitly stated and reinforced across Cyber Tech Talks, Bootcamp decks, and internal Teams guidance. [[🗣️ Introd...n be confu | Viva Engage]](https://engage.cloud.microsoft/main/threads/eyJfdHlwZSI6IlRocmVhZCIsImlkIjoiMzc5MzE2Nzk4NDQyNzAwOCJ9)

---

### ✅ Rule #2: When does STS become mandatory?

STS is **conditionally required**, typically when **any of the following apply**:

#### 1. External / Internet‑Facing Exposure

- Public APIs
- SaaS portals
- Partner or customer‑accessible endpoints
- Public cloud exposure

> _“Security testing (STS) is required prior to releasing a new application or product that has an external (i.e., internet) facing component.”_ [[Cyclops Scrum | Teams]](https://teams.microsoft.com/l/message/19:meeting_NTk0NWZmYTYtZDQ0ZS00OThhLTlmMjgtMWY5Y2JlOWMyYjQ2@thread.v2/1727325159419?context=%7B%22contextType%22:%22chat%22%7D)

---

#### 2. Major Change to an Existing Externally Facing System

Examples:

- Auth model change
- API surface change
- Cloud migration (on‑prem → cloud)
- Identity / access changes (e.g., Paladin onboarding)
- New integrations or data paths

---

#### 3. Explicit Outcome of SRS

Very important:

- **SRS output may explicitly state: “STS required”**
- This is common for:
    - High‑risk architectures
    - AI/ML platforms
    - Data‑heavy or regulated systems

> _“SRS requests can be done in parallel with STS requests … Report will indicate, if STS is required.”_ [[1_SRS STS..._Finalized | PowerPoint]](https://hp.sharepoint.com/teams/HPICSPS/_layouts/15/Doc.aspx?sourcedoc=%7B6CB48CFD-D630-4B30-AE5C-9B1A98863BF9%7D&file=1_SRS%20STS%20Bootcamp_030624_v3.1_Finalized.pptx&action=edit&mobileredirect=true&DefaultItemOpen=1)

---

#### 4. Selected Internal Systems (Exception Case)

Even for internal tools:

- Cyber may **select certain internal apps** for STS if:
    - High privilege
    - Sensitive data
    - Horizontal impact risk

[[Cyclops Scrum | Teams]](https://teams.microsoft.com/l/message/19:meeting_NTk0NWZmYTYtZDQ0ZS00OThhLTlmMjgtMWY5Y2JlOWMyYjQ2@thread.v2/1727325159419?context=%7B%22contextType%22:%22chat%22%7D)

---

## 4. Practical Decision Flow (Use This)

Is this a new solution or major change?

        |

        └── Yes → SRS (mandatory)

                    |

                    ├─ External or public exposure?

                    |      └── Yes → STS required

                    |

                    ├─ SRS flags high risk?

                    |      └── Yes → STS required

                    |

                    └─ Internal only + low risk?

                           └── Usually SRS only

``

---

## 5. Common HP Scenarios (Mapped)

### ✅ Internal HP Tool (No internet exposure)

- ✅ SRS: **Required**
- ✅ STS: **Usually not**, unless Cyber flags it

### ✅ Partner / Customer‑facing SaaS (e.g., MPC, X360)

- ✅ SRS: **Required**
- ✅ STS: **Required**

### ✅ API platform / AI service

- ✅ SRS: **Required**
- ✅ STS: **Almost always required**
    - Especially with data movement, model inference, or credentials

### ✅ Dev / Non‑Prod Deployment

- ❌ SRS/STS not strictly blocking
- ✅ **Both mandatory before PROD**

[[Cyclops Scrum | Teams]](https://teams.microsoft.com/l/message/19:meeting_NTk0NWZmYTYtZDQ0ZS00OThhLTlmMjgtMWY5Y2JlOWMyYjQ2@thread.v2/1727325159419?context=%7B%22contextType%22:%22chat%22%7D)

---

## 6. Who Makes the Final Call?

**Primary determination path**

1. You submit **SRS**
2. Security Architect reviews and:
    - Clears with SRS only **OR**
    - Flags **STS as mandatory**

**You don’t self‑decide STS** — the **SRS outcome and cyber policy** do.

---

## 7. Short Answer (If You Need to Explain to Stakeholders)

> **SRS reviews the design and architecture; STS tests the real system for exploitable vulnerabilities.  
> All solutions require SRS. STS is required when the system is external, high‑risk, or when SRS mandates it.**

---

Up: [[Security & auth]]

## Tags
#security

