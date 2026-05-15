---
title: WALKRI-CROSS Boundary Specification
version: 0.1.0
date: 2026-05-15
license: CC0
status: Working draft. Governs the relationship between WALKRI v0.1.0 and CROSS v0.2.4, and specifies the changes required for CROSS v0.3.0.
---

# WALKRI-CROSS Boundary Specification

Version 0.1.0 | 2026-05-15 | CC0

---

## Part 1: The Dividing Principle

CROSS owns the obligation architecture: it specifies what must be demonstrated, by whom, at which gate, and in which obligation mode. WALKRI owns the specification quality layer: it specifies how the fields and criteria collecting that demonstration must be defined so that the resulting data is valid, consistent, and auditable. The division is clean. A CROSS gate says "provide an operational definition." WALKRI says what an operational definition must contain. CROSS says "reference an external standard." WALKRI says what a conformant external standard reference must include. CROSS says "the indicator must meet the data quality standards." WALKRI names those standards, defines their assessment questions, and states their failure modes. One standard sets the obligation architecture; the other sets the quality floor for how that architecture is implemented at the field level.

The portability consequence runs in both directions. WALKRI works without CROSS because the specification quality layer does not depend on any particular obligation architecture: any program that collects structured data and cares about whether its fields are precisely defined can adopt WALKRI independently. CROSS works without WALKRI in the sense that it can be adopted by programs not yet implementing WALKRI; but CROSS-conformant programs are expected to achieve WALKRI Standard certification for their fields as the ecosystem matures. The two standards are designed to be used together and are jointly branded CROSS+WALKRI when both are in force.

---

## Part 2: Section-by-Section Mapping

The table below maps every current CROSS v0.2.4 Part and subsection to one of four statuses.

**Status definitions:**

- **STAYS IN CROSS:** Content remains in CROSS; no change required for v0.3.0.
- **MOVES TO WALKRI:** Content is now owned by WALKRI; CROSS v0.3.0 references WALKRI for this requirement rather than reproducing it.
- **STAYS IN CROSS, REFERENCES WALKRI:** CROSS retains the obligation; WALKRI provides the specification quality layer that governs how the obligation is met.
- **SPLIT:** The obligation (what must be demonstrated) stays in CROSS; the specification quality requirements (how fields and criteria must be defined to meet that obligation) move to WALKRI.

| Part / Subsection | Status | Notes |
|---|---|---|
| Part I: Independence and Suite References | STAYS IN CROSS | Pure CROSS obligation architecture; no specification quality content |
| Part II: Independent Obligation Dimensions (all dimensions except IP) | STAYS IN CROSS | Triggering logic and tier structure are obligation architecture |
| Part II: IP Ownership Declaration field quality | STAYS IN CROSS, REFERENCES WALKRI | The obligation to submit an IP ownership declaration stays in CROSS; field quality of that declaration is governed by WALKRI |
| Part III: Obligation Modes | STAYS IN CROSS | Mode declaration logic and diagnostic rules are pure obligation architecture |
| Part IV: Four gate types | STAYS IN CROSS | Gate existence, activation logic, and mode-specific entry requirements |
| Part IV: Pre-Award Indicator Confirmation | STAYS IN CROSS | Gate lifecycle management; the confirmation window and silence-as-confirmation rule are process obligations |
| Part IV: Evidence scope (four levels) | STAYS IN CROSS | What evidence is required at each scope level |
| Part IV: Outcome Verification with Counterfactual Reference | STAYS IN CROSS | The four required contract elements at counterfactual reference level are evidence obligations |
| Part IV: Evidence strength (four levels) | STAYS IN CROSS | How evidence is verified; the verification mechanism taxonomy |
| Part IV: Infrastructure declaration | STAYS IN CROSS | Funder-side process obligation; published before the round opens |
| Part IV: Proportionality | STAYS IN CROSS | Scaling logic calibrated by the Coordination Scaling Standard |
| Part IV: Cost-effectiveness for continuation | STAYS IN CROSS | Continuation criterion; obligation architecture |
| Part IV: External Standard References | MOVES TO WALKRI | URL, version anchor, scope, and compliance threshold protocol now in WALKRI Part VI; CROSS v0.3.0 references WALKRI for these requirements |
| Part IV: Gate Criterion Specification | MOVES TO WALKRI | The bidirectional precision principle and five criterion specification requirements (criterion intent, operational definition, response form, evidence form, compliance threshold) now in WALKRI Part III; CROSS v0.3.0 references WALKRI |
| Part V: Indicator Specification - field list (what fields are required) | STAYS IN CROSS | The obligation to provide each named field stays in CROSS |
| Part V: Indicator Specification - operational definition content requirements | MOVES TO WALKRI | Inclusion criteria, exclusion criteria, unit of analysis, and edge case determination now in WALKRI Part III, Criterion 2; CROSS v0.3.0 says "provide an operational definition meeting WALKRI requirements" |
| Part V: Indicator Specification - construction methodology quality | MOVES TO WALKRI | The quality standard for construction and aggregation methodology now in WALKRI; CROSS v0.3.0 says "provide a construction methodology meeting WALKRI requirements" |
| Part V: Indicator Specification - data source quality | MOVES TO WALKRI | Independence and corroboration requirements now governed by WALKRI Integrity standard (Part V of WALKRI) |
| Part V: Measurement form and evidence classification (three-axis) | STAYS IN CROSS, REFERENCES WALKRI | CROSS retains the three-axis classification (source type, measurement form, aggregation type); WALKRI's evidence form requirement (Part III, Criterion 4) governs how each axis is specified |
| Part V: On-chain execution and verification instruments | STAYS IN CROSS, REFERENCES WALKRI | The obligation to specify invariant, verification method, verification artifact, and failure surface stays in CROSS; evidence form specification quality is governed by WALKRI |
| Part V: Sustainability and transition plan | STAYS IN CROSS | Obligation architecture; funder-activated optional field |
| Part VI: Concurrent Funding Disclosure | STAYS IN CROSS | Pure obligation; no specification quality content |
| Part VI-A: Scope Attribution and Outcome Credit | STAYS IN CROSS | Pure obligation; additionality declaration and outcome credit attribution are obligation requirements |
| Part VII: Conflict of Interest Framework | STAYS IN CROSS | Pure obligation architecture; tier structure, web3-specific categories, and process requirements |
| Part VIII: Data Quality Standards | MOVES TO WALKRI | Validity, Integrity, Precision, Reliability, and Timeliness now in WALKRI Part V; CROSS v0.3.0 references WALKRI for assessment questions and failure mode definitions |
| Part IX: Grant Configurator | STAYS IN CROSS, REFERENCES WALKRI | CROSS retains the Grant Configurator as the funder onboarding instrument; CROSS v0.3.0 says "the Grant Configurator must achieve WALKRI Standard certification for all published fields" |
| Part IX: Field clarity gate paragraph | MOVES TO WALKRI | The mechanism for flagging underspecified fields before a round opens is now described in WALKRI Part IV (the three-stage process and pre-publishing quality gate); CROSS references it |
| Part IX: Grantee Dashboard | STAYS IN CROSS | Implementation architecture |
| Part IX: Reviewers Dashboard | STAYS IN CROSS | Implementation architecture |
| Part IX: CROSS skill | STAYS IN CROSS | Implementation architecture |
| Part IX: Runbooks | STAYS IN CROSS | Implementation architecture |
| Part X: Companion Documents | STAYS IN CROSS | CROSS companion documents |
| Part XI: Funder Obligations and Redress | STAYS IN CROSS | Pure obligation architecture; internal clarification, structured appeals, independent redress |

---

## Part 3: How CROSS v0.3.0 References WALKRI

CROSS v0.3.0 references WALKRI at four locations. The text below specifies what CROSS v0.3.0 will say at each location.

**Reference Point 1: In Part IV, replacing Gate Criterion Specification**

"Gate criteria in a CROSS-conformant round must meet WALKRI criterion specification requirements at Standard certification level or above (WALKRI-standard-0_1_0.md, Part III). A gate criterion that does not pass WALKRI audit before the round opens is a funder-side conformance failure."

**Reference Point 2: In Part IV, replacing External Standard References**

"External standard references in a CROSS-conformant gate must follow the WALKRI External Standard Reference Protocol (WALKRI-standard-0_1_0.md, Part VI), including URL, version anchor, and compliance threshold specification."

**Reference Point 3: In Part V, modifying the operational definition field**

"The operational definition must meet WALKRI requirements for inclusion criteria, exclusion criteria, unit of analysis, and edge case determination (WALKRI-standard-0_1_0.md, Part III, Criterion 2: Operational Definition)."

**Reference Point 4: In Part VIII, replacing Data Quality Standards**

"CROSS-conformant indicators are assessed against the five WALKRI Data Quality Standards: Validity, Integrity, Precision, Reliability, and Timeliness (WALKRI-standard-0_1_0.md, Part V). Reviewers apply WALKRI assessment questions and failure mode definitions during gate assessment."

---

## Part 4: What WALKRI Inherits from CROSS

WALKRI does not reference CROSS. WALKRI is the downstream standard in the dependency direction: CROSS references WALKRI, not the reverse. This is deliberate. WALKRI's specification quality layer must be portable to programs that operate under no external obligation standard at all; if WALKRI referenced CROSS, it would import CROSS's obligation architecture into every WALKRI adoption, including those where CROSS is not in use.

Programs that adopt WALKRI without CROSS inherit nothing from CROSS. They use WALKRI Part III directly as their specification authority, with no gate architecture, obligation mode, or evidence scope requirements implied. The standard governs field quality; it does not impose an obligation architecture.

Programs that adopt both CROSS and WALKRI operate under both standards' requirements simultaneously. CROSS sets the obligation architecture: which gates exist, what must be demonstrated, who must verify it. WALKRI sets the specification quality floor: how the fields and criteria through which those obligations are collected must be defined. The two layers are independent and additive. A CROSS-conformant program that has not achieved WALKRI certification for its fields meets CROSS's obligation architecture requirements but fails WALKRI's specification quality requirements. A WALKRI-certified form used outside any obligation framework meets WALKRI's quality requirements but imposes no obligations on what must be demonstrated by the people filling it in. Both standards are required for a CROSS+WALKRI conformant program.

---

## Part 5: CROSS v0.3.0 Version Note

The changes described in this document require a CROSS v0.3.0 release rather than a patch release. CROSS v0.2.x owned the specification quality layer: Gate Criterion Specification, External Standard Reference Protocol, Indicator Specification operational definition requirements, and Data Quality Standards all lived in CROSS. CROSS v0.3.0 delegates that layer to WALKRI. This is a structural scope change, not a content revision. The substance of each requirement does not change; its governing authority does. Moving a requirement from one standard to another changes where implementers must look for the authoritative definition of that requirement, which is a structural change warranting a minor version bump.

The changelog entry for CROSS v0.3.0 should read: "Extracted Gate Criterion Specification, External Standard Reference Protocol, Indicator Specification quality requirements, and Data Quality Standards to WALKRI v0.1.0. CROSS now references WALKRI for these requirements. No obligation architecture changes."

CROSS v0.2.x implementations remain valid. A program running under CROSS v0.2.4 without WALKRI satisfies CROSS v0.2.4's requirements as published, including the specification quality content that lived in CROSS before this boundary was drawn. Programs upgrading to CROSS v0.3.0 must additionally achieve WALKRI Standard certification for their fields; the substance of what that certification requires is identical to what CROSS v0.2.4 already required, because the requirements moved, not changed.
