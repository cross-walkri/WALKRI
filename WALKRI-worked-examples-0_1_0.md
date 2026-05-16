---
title: WALKRI Worked Examples
version: 0.1.0
date: 2026-05-15
license: CC0
status: Working draft. Companion to WALKRI-standard-0_1_0.md.
source: Octant Epoch 12 grant evaluation cycle, 2026.
---

# WALKRI Worked Examples

Version 0.1.0 | 2026-05-15 | CC0

---

## Introduction

These examples demonstrate what WALKRI failures look like in practice and what conformant specifications would have looked like in their place. They are drawn from the Octant Epoch 12 grant evaluation cycle. Octant is a web3 public goods funding program; in Epoch 12, 29 grant applications were evaluated using a form built in Fillout. Several fields in that form produced inconsistent applicant responses that complicated evaluation because those fields lacked precise operational definitions, compliance thresholds, or evidence forms. The cases documented here are real specification failures from that cycle, reconstructed in WALKRI's five-element format to show what the fields should have contained before any application was accepted.

Each example follows the same structure: the field as published, a description of what happened in evaluation, and a WALKRI-conformant specification showing all five elements. The final example is a positive case, showing a field that would pass WALKRI audit without modification. The last two sections draw quantitative observations from the Epoch 12 experience and close with a summary for practitioners who run grant evaluations.

The before/after blocks use structured comparison formatting throughout. Prose sections use prose. The goal is not to criticize the Octant team's execution; the goal is to make the failure modes concrete enough that they are recognizable and fixable in future cycles.

---

## Example 1: The DPG Eligibility Field

### The field as published

```
Label:              "Building on Ethereum or qualifying as DPG per DPGAlliance"
Response form:      Not specified (applicants answered in free text)
Evidence form:      Not specified
Compliance threshold: Not specified
```

### What happened

Evaluators could not consistently assess DPG eligibility because the field did not specify which of the nine DPG Standard indicators applied, what evidence form satisfied each, or whether all nine or a subset were required. Registry membership was used as a proxy for the nine-indicator assessment, which is incorrect: registry membership confirms past assessment, not current qualification. Projects that had been assessed for the registry years earlier were treated as currently qualifying even where the project had changed substantially since assessment. Evaluations across 29 applications produced inconsistent DPG determinations because each evaluator applied a personal interpretation of what "qualifying as DPG" meant.

### WALKRI-conformant specification

**Criterion intent:** Whether the project satisfies the Digital Public Goods Standard as an alternative to the Ethereum pathway, assessed against the nine DPG Standard indicators, for purposes of determining pathway eligibility at time of application.

**Operational definition:**
- Inclusion: a project qualifies if it satisfies the required DPG Standard indicators as specified in the compliance threshold below.
- Exclusion: registry membership alone does not qualify a project; the current state of the project must satisfy the indicators at the time of evaluation.
- Unit of analysis: the applying project, not the organization.
- Edge case: a project in the DPG registry that has changed substantially since registry assessment is evaluated against current indicators, not registry status. Substantial change is defined as a change in license, a change in core functionality, or a change in technical dependencies that affects platform independence.

**Response form:** Multi-select. Applicants select the pathway that applies: Ethereum mainnet, Ethereum Layer 2, or DPG Standard. Multi-select because some projects may qualify under both pathways.

**Response form justification:** The original single free-text framing required applicants to argue for whichever pathway they believed applied, without a structured mechanism to indicate that both pathways applied. Projects that qualified on both grounds were recorded inconsistently, producing artificial distinctions in pathway distribution across the cohort. A multi-select resolves this and produces a cleaner dataset for cross-project analysis.

**Evidence form:** For the DPG pathway, a completed DPG self-assessment form or a link to the project's evidence for each required indicator. Evidence must be accessible from public sources without authentication.

**Compliance threshold** (DPG Standard, https://digitalpublicgoods.net/standard/, accessed 2026-05-15):

Required indicators (all four must pass):
- Indicator 1, SDG relevance: named SDG with explanation of relevance.
- Indicator 2, open license: LICENSE file URL in a public repository with an OSI-approved license identifier for software, or a Creative Commons license for content; SPDX identifier required.
- Indicator 4, platform independence: list of dependencies with confirmation that none are mandatory proprietary platforms.
- Indicator 5, documentation: public documentation URL accessible without authentication.

Advisory indicators (3, 6, 7, 8, 9): reviewers note presence or absence but advisory indicators do not determine passage.

Minimum threshold: all four required indicators must pass. Failure on any required indicator is a gate fail on the DPG pathway.

### WALKRI audit result

| Element | Original field | WALKRI-conformant specification |
|---|---|---|
| Criterion intent | Absent | Pass |
| Operational definition | Absent | Pass |
| Response form | Not specified | Pass |
| Evidence form | Absent | Pass |
| Compliance threshold | Absent | Pass |

**Original field:** Not certifiable. Five unresolved flags.
**Conformant specification:** Certified at Standard level.

---

## Example 2: The "Contributions" Single-Select Field

### The field as published

```
Label:              "Contributions"
Response form:      Single-select dropdown
Options:            Code | Community | Research | Governance | Other
Option definitions: Not specified
Evidence form:      Not specified
```

### What happened

Projects whose work spanned multiple contribution types were forced to select one. A project that maintained production infrastructure while running educational workshops selected either "Code" or "Community" and lost the other dimension in the dataset. The problem compounded at the analysis layer: projects with primarily "Community" contributions were evaluated differently from projects with primarily "Code" contributions even where the public goods impact was comparable. The single-select structure introduced a categorical distortion that was invisible in the collected data because the data looked clean. The distortion was only visible when evaluators tried to compare projects across categories and found that the categories did not represent stable natural kinds in the applicant population.

A second failure compounded the first: none of the five options carried a definition. "Community" could mean in-person events, online forum moderation, translation, or governance facilitation. "Governance" could mean voting in a DAO, writing governance proposals, or building tooling for governance processes. Two applicants with substantively similar work selected different options based on how they described themselves, not on any common definition.

### WALKRI-conformant specification

**Criterion intent:** The primary types of contribution the project makes to the ecosystem, for purposes of understanding the project's public goods pathway and enabling cross-project comparison by contribution type.

**Operational definition:**
- Inclusion: any contribution type that the project has demonstrably produced in the prior 12 months with evidence accessible from public sources.
- Exclusion: aspirational contributions not yet produced; contributions produced by other projects that the applying project only coordinates or funds.
- Unit of analysis: the applying project's outputs.
- Edge case: a project that began operations within the prior 12 months is assessed on the period of operation; the 12-month window does not disqualify newer projects.

**Option definitions** (each option is defined; applicants may select all that apply):
- Code: software artifacts released under an open license in a public repository, including applications, libraries, tooling, and protocol implementations.
- Community: documented facilitation, education, or coordination activities with named participants or events, including workshops, curricula, translations, and moderated forums.
- Research: published findings under an open license accessible without authentication, including reports, papers, and documented investigations.
- Infrastructure: operational systems with verifiable uptime records, including nodes, relays, bridges, oracles, and indexers.
- Governance: participation in on-chain or structured off-chain governance with verifiable records, including proposal authorship, protocol design contributions, and governance tooling development.

**Response form:** Multi-select. Applicants may select all contribution types that apply.

**Response form justification:** Most projects contribute across multiple types. A single-select forces artificial categorization that distorts evaluation and reduces data quality for cross-project analysis. The original single-select also had no option definitions, meaning the categorical distortion was compounded by interpretation variance within each category.

**Evidence form:** For each selected contribution type, a URL to a public artifact demonstrating that contribution type within the prior 12 months. A project selecting three contribution types must submit at least one URL per type.

### WALKRI audit result

| Element | Original field | WALKRI-conformant specification |
|---|---|---|
| Criterion intent | Absent | Pass |
| Operational definition | Absent (options undefined) | Pass |
| Response form | Single-select on multi-value construct (design error) | Pass |
| Evidence form | Absent | Pass |
| Compliance threshold | N/A (no external standard) | N/A |

**Original field:** Not certifiable. Four flags, including a response form design error.
**Conformant specification:** Certified at Standard level.

Note on response form design errors: a design error differs from a missing element. A missing element is an absence; a design error is an active structural choice that produces systematic measurement error. The single-select on a multi-value construct is a design error because it cannot be fixed by adding a definition. The response type itself must change.

---

## Example 3: A Well-Specified Field (Positive Case)

This example shows a field that passes WALKRI audit without modification. It is drawn from a hypothetical but realistic version of a "Prior grant funding" field from a rigorous grant program. The purpose is to demonstrate that WALKRI conformance does not require heroic effort when specification discipline is applied from the start.

### The field as specified

**Label:** Prior grant funding received in the past 24 months

**Criterion intent:** The total amount of grant funding received by the applying project from external funders in the 24-month period ending on the application deadline, for purposes of assessing funding concentration and evaluating the marginal impact of the requested grant.

**Operational definition:**
- Inclusion: any grant, award, or non-dilutive funding received by the project or its operating entity from an external funder, including retroactive public goods funding rounds, foundation grants, and program awards.
- Exclusion: investment (equity, token, or convertible note); revenue from products or services; funding received by a parent organization that was not specifically designated for this project; in-kind contributions.
- Unit of measurement: USD equivalent at the time of receipt, using the exchange rate on the date of receipt for non-USD denominations.
- Counting rule: each distinct grant award is counted separately. A multi-tranche grant is counted as one award; the total committed amount is reported, not the amount disbursed to date.
- Boundary condition: funding received on the application deadline date is included; funding received after the deadline is excluded regardless of when it was announced.
- Edge case: if the project is incorporated in multiple legal entities and the grant was received by a sister entity that shares operational infrastructure, include it and note the entity relationship.

**Response form:** Numeric (USD equivalent, integer, no decimals), followed by a multi-field structured input listing each grant by funder name, amount, date, and grant program name.

**Response form justification:** A numeric field captures the aggregate for analysis; the structured list captures the provenance of each component for reviewer verification. A single text field would produce responses in inconsistent formats that are not machine-readable.

**Evidence form:** For each grant listed, a publicly accessible announcement URL or award letter. Self-reported totals without supporting URLs are not accepted. If no public announcement exists, a redacted award letter or a letter of attestation from the funder is acceptable.

**Compliance threshold:** Not applicable. This field does not reference an external standard. The operational definition above is the compliance specification.

**Timeliness note:** Evidence must reflect the 24-month window ending on the application deadline. Evidence from outside this window should not be submitted and will not be considered.

### WALKRI audit result

| Element | Assessment |
|---|---|
| Criterion intent | Pass: measurement claim is clear and distinct from the label |
| Operational definition | Pass: inclusion, exclusion, unit, counting rule, boundary condition, and one edge case all present |
| Response form | Pass: response type is appropriate for the construct; justification addresses why numeric plus structured list is correct |
| Evidence form | Pass: artifact type, required content, and acceptable alternatives are specified; recency requirement is stated |
| Compliance threshold | Pass: no external standard referenced; operational definition is self-sufficient |

**Field certified at Standard level without modification.**

This field took more time to specify than typical form design. That time investment is recovered in evaluation: reviewers applying this field to 29 applications make no discretionary judgments about what counts as prior funding. The operational definition makes those judgments once, in advance, for the entire cohort.

---

## Example 4: The Upstream Value - Before and After Analysis

The cost of underspecified fields is not primarily a data quality cost. It is an evaluator time cost that accrues during review and a reliability cost that accrues when results are contested or when the dataset is reused.

The Epoch 12 evaluation record supports the following observations.

**Eligibility judgment calls:** The DPG eligibility field, as published, required at least one substantive judgment call per application that cited DPG status as a basis for eligibility. Across 29 applications, at least 8 required extended researcher investigation to determine whether the project's claimed DPG status was current and applicable. A WALKRI-conformant DPG field, with its four required indicators and specified evidence form, would have resolved those 8 cases at application time by requiring applicants to submit indicator-level evidence with their application. The evaluator time cost of post-submission investigation is conservatively estimated at 30 to 45 minutes per case, totaling 4 to 6 hours of evaluation time that a conformant field would have eliminated.

**Unverifiable public claims:** Across the 29 applications, at least 12 produced findings of "cannot be confirmed from any public source" on claims that were material to eligibility or impact assessment. A properly specified evidence form requirement, applied at the point of submission, would have surfaced these gaps before any evaluation began. Applicants who cannot satisfy an evidence form requirement at submission time either strengthen their submission or are flagged immediately, rather than passing initial review and requiring intensive investigative work later.

**Contribution type distortion:** The single-select Contributions field produced at least 6 cases where the selected category visibly understated the project's actual contribution profile, based on reviewer notes cross-referenced against the applicant's supporting materials. These 6 cases required qualitative adjustment during evaluation. A multi-select field with defined options would have captured the full profile at the application stage.

**Specification cost vs. evaluation cost:** Specifying the DPG eligibility field and the Contributions field to WALKRI conformance would have required approximately 2 to 4 hours of design time before the round opened. The evaluation time cost attributable to those two underspecified fields alone is estimated at 8 to 12 hours across the full Epoch 12 cohort. The ratio is not favorable to the "we'll figure it out in evaluation" approach. That ratio holds across every round the form is reused in its current state.

These numbers are drawn from the Epoch 12 evaluation record and are reported using "at least" framing where exact counts are uncertain. They are not projections or models; they reflect documented judgment calls and researcher findings from the evaluation cycle.

---

## Closing: The Case Study Summary

Epoch 12 demonstrated a pattern that is common in grant evaluation and predictable in its consequences. A form is built quickly, fields are labeled rather than defined, and eligibility criteria reference external standards without specifying what those standards require in practice. The form looks complete because it has all the right labels. The problems emerge in evaluation, when reviewers discover that the labels do not resolve the questions they need to answer. Evaluators spend time they should not have to spend reconstructing definitions that should have been in the form. Results are harder to defend because the standard was never written down. The dataset is harder to reuse because the fields cannot be trusted to mean the same thing across applications.

WALKRI addresses this at the source: the point where a question becomes a field before any applicant sees it. Applying WALKRI to the two most consequential underspecified fields in Epoch 12 (the DPG eligibility field and the Contributions field) would have taken a few hours before the round opened and would have eliminated an estimated 8 to 12 hours of evaluation judgment work, produced a cleaner and more auditable dataset, and reduced the number of eligibility determinations that depended on individual evaluator interpretation. The investment is in specification. The return is in reliability.
