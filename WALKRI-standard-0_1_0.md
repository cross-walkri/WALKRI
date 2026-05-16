---
title: WALKRI - Working Architecture for Legible, Knowledge-Ready Intake
version: 0.1.0
date: 2026-05-15
license: CC0
status: Working draft. Initial specification. Companion standard to CROSS v0.2.4.
companion_standard: CROSS (github.com/cross-walkri/CROSS)
brand: CROSS+WALKRI
related_documents:
  - WALKRI-interface-specification-0_1_0.md
  - WALKRI-CROSS-boundary-0_1_0.md
companion_documents:
  - WALKRI-guidance-0_1_0.md
  - WALKRI-templates-0_1_0.md
  - WALKRI-rubric-0_1_0.md
  - WALKRI-worked-examples-0_1_0.md
---

# WALKRI - Working Architecture for Legible, Knowledge-Ready Intake

Version 0.1.0 | 2026-05-15 | CC0

---

## Part I: Purpose and Scope

WALKRI (Working Architecture for Legible, Knowledge-Ready Intake) is a standard for epistemic quality at the point of data capture. It specifies how fields and criteria used to collect structured information must be defined, so that the resulting data is valid, consistent, provenance-aware, and reusable by both humans and automated systems.

### The Problem

Funders, organizations, and programs regularly publish intake fields without operationally defining them. A dropdown labeled "Contributions" offers single-select options with no definitions. A gate criterion labeled "Qualifies as DPG" appears without specifying which of the nine Digital Public Goods Standard indicators apply, which evidence satisfies each, what threshold constitutes passage, or whether registry membership is accepted as a proxy for current indicator qualification. Each gap produces a different failure: one reviewer checks the registry; another assesses indicators directly; a third accepts a self-assessment; none of them is wrong, given what the criterion actually says. These are not edge cases; they are the default condition of most structured data collection in the grant, program, and research evaluation space.

The consequences are predictable. Applicants interpret underspecified fields differently from one another and from reviewer expectations. Reviewers apply inconsistent interpretations across a cohort, producing non-reproducible outcomes. Downstream analysts inherit a dataset whose nominal consistency conceals definitional variance; analysis built on that data is suspect at the foundation, not because the analysis is wrong, but because the instrument was never precise enough to support it.

The same precision obligation that CROSS (Common Reporting Outcome Standards Schema) imposes on applicant indicators has not been applied to the fields and criteria funders use to collect data. WALKRI closes that gap. It operates at the instrumentation and collection layer: the point where a question is encoded as a field before any applicant ever sees it.

### What WALKRI Does

WALKRI specifies: what information a field definition must contain before it is considered complete; what process must be followed to produce a conformant field; what quality standards the field must meet; and what provenance information must travel with the data once collected.

WALKRI is not a form builder. It does not render forms, generate user interfaces, or integrate with any specific form platform's API. Form tools (Fillout, Jotform, Typeform, KoBoToolbox, REDCap, and others) are interchangeable rendering layers. WALKRI sits above them as a quality gate, operating on JSON Schema as its native format, which underlies all major form tools. A field that meets WALKRI's specification requirements can be rendered by any conformant tool; the quality of the resulting data is independent of which tool is used.

WALKRI is portable. It functions as a companion to any obligation standard that specifies what data must be collected, or it can be used independently by any organization that wants to improve its own data collection practices without reference to an external obligation framework.

### The CROSS+WALKRI Relationship

CROSS specifies what must be collected: the indicators, evidence requirements, and gate criteria that programs and applicants must satisfy. WALKRI specifies how those fields must be defined so that what gets collected matches what was required. CROSS tells a program that applicants must demonstrate open licensing; WALKRI tells the program how to define the open licensing field precisely enough that all applicants interpret it consistently, all reviewers assess it by the same standard, and the resulting data can be trusted by downstream analysis. Together they are branded CROSS+WALKRI. The two standards are designed to be used together, but each is independently operable.

---

## Part II: The Three Interfaces

WALKRI has three relationships, each requiring a defined connection.

### 2.1 Obligation Standards

WALKRI connects to whatever framework specifies what must be collected. CROSS is the primary example; the connection is generic, so WALKRI works with any obligation standard.

An obligation standard specifies what must be collected: the indicators, criteria, and evidence requirements that constitute a complete response. WALKRI specifies how those fields must be defined so that the collection produces the data required by the obligation standard.

The field specification requirements, data quality standards, and external standard reference protocol in this standard originated in CROSS Parts IV, V, and VIII and have been moved here. CROSS v0.3.0 will reference WALKRI for those requirements rather than specifying them directly. Until v0.3.0 is published, the exact boundary is documented in WALKRI-CROSS-boundary-0_1_0.md. A conformant obligation standard provides: a named set of collection requirements; a version identifier that can serve as a reference anchor; and, optionally, a designated mapping to WALKRI's five criterion specification elements.

An obligation standard that formally references WALKRI must specify, for each of its collection requirements, which WALKRI criterion specification elements it enforces and at what threshold. CROSS does this in its Gate Criterion Specification (Part IV). Other obligation standards may structure this mapping differently; WALKRI accepts any mapping that is explicit, versioned, and auditable.

Organizations using WALKRI without any obligation standard use Part III of this document directly as their specification authority.

### 2.2 Form Rendering Tools

WALKRI works with form tools through JSON Schema, the format that underlies Fillout, Jotform, Typeform, REDCap, and others. WALKRI does not integrate with any specific tool's API; it operates on the shared format underneath them.

A WALKRI-conformant field specification can be expressed as a JSON Schema object, reviewed by the WALKRI Audit Tool, and then passed to any form platform for rendering without loss of specification integrity.

Two secondary compatible formats are recognized: REDCap data dictionaries and XLSForm. Both formats are widely used in research and humanitarian data collection contexts where JSON Schema tooling may not be available. WALKRI-compliant fields expressed in these formats must preserve all five criterion specification elements in structured metadata fields; the detailed mapping specifications for these formats are provided in WALKRI-interface-specification-0_1_0.md.

WALKRI's quality guarantees are enforced at the specification stage, before any form is published.

### 2.3 Data Consumers

Data collected through WALKRI-conformant fields produces output aligned with Croissant (ML-ready dataset metadata), FAIR principles, and W3C PROV (provenance tracking). This makes the data directly usable by analysts and AI pipelines without cleanup.

WALKRI's enrichment layer produces output aligned with three external standards:

**Croissant** (ML-ready dataset metadata): A WALKRI-enriched dataset includes field-level metadata sufficient for automated ingestion by machine learning pipelines, including option definitions, evidence form specifications, and version anchors for any referenced external standards.

**FAIR principles** (Findable, Accessible, Interoperable, Reusable): WALKRI-enriched output carries the provenance fields and schema version information required for FAIR compliance. The interoperability requirement is met by JSON Schema as the native format; the reusability requirement is met by the operational definitions that travel with each field.

**W3C PROV** (provenance data model): WALKRI's provenance fields map to the W3C PROV data model's core entities (Entity, Activity, Agent) so that the collection history of any data element can be expressed in a standard provenance graph. The detailed alignment specifications for all three targets are in WALKRI-interface-specification-0_1_0.md.

---

## Part III: Field Specification Requirements

A WALKRI-conformant field must satisfy five criterion specification requirements. These requirements apply to funders specifying gate criteria, to researchers designing survey fields, to organizations building intake forms, and to any other entity using WALKRI to govern data collection. A field that does not satisfy all five requirements is not WALKRI-conformant, regardless of how it is labeled or where it appears in a form.

The five requirements are: criterion intent, operational definition, response form, evidence form, and compliance threshold.

### 3.1 Criterion Intent

**What it requires:** A written statement of what the field measures, distinct from its label. The criterion intent answers: what does a true response to this field tell us about the applicant or subject?

**Why it is required:** A label is a name. An intent is a measurement claim. The label "Community Engagement" can mean the number of community members reached, the depth of co-design processes, the geographic distribution of engagement, or the frequency of contact. Each is a different measurement instrument. Without a written criterion intent, the field designer cannot assess whether the response form is capable of capturing what they intended, and reviewers cannot assess responses against a consistent standard.

**Failure mode when absent:** Different reviewers interpret the same label differently. Applicants optimize for the interpretation they believe their reviewer holds, producing responses that are locally rational and globally inconsistent. Downstream analysis treats the field as if it measured a single thing when it measured several different things across the cohort.

### 3.2 Operational Definition

**What it requires:** A complete definition of each option or response category in the field, with qualifying examples and non-qualifying examples for each. For binary fields: what conditions produce a "yes" and what conditions produce a "no," with at least one edge case determination. For numeric fields: the unit of measurement, the counting rule, and the boundary conditions. For text fields: the scope of acceptable response content and the minimum content that constitutes a complete response.

**Why it is required:** An option without a definition delegates interpretation to applicants. Two applicants with identical circumstances will select different options if their interpretation of the option labels diverges. The resulting data is not comparable; it reflects applicant interpretation variance rather than actual differences in the applicant population.

**Failure mode when absent:** Nominal consistency (all applicants chose from the same options) conceals actual definitional variance. Analysis of the resulting data produces conclusions that are artifacts of the interpretation distribution, not of the underlying population.

For text fields and qualitative narrative responses, the operational definition specifies the scope and minimum content requirements rather than exhaustive option definitions. The additional design challenges posed by inherently qualitative fields are addressed in Appendix A.

### 3.3 Response Form

**What it requires:** The response type for the field (single-select, multi-select, binary, numeric, text, URL, or composite), with a written justification for why that response type is appropriate for the criterion intent. The justification must address whether the response type is capable of capturing the variance in the underlying construct that the criterion intent requires.

**Why it is required:** Response type is not a formatting decision; it is a measurement decision. A single-select response form assumes the construct is categorical with mutually exclusive categories. A numeric response form assumes the construct is quantifiable on a common scale. Using the wrong response form for a construct produces systematic measurement error that cannot be corrected in analysis.

**Failure mode when absent:** Fields are designed for administrative convenience rather than measurement accuracy. The resulting data has bounded variance by construction, masking real differences in the population.

### 3.4 Evidence Form

**What it requires:** A specification of the artifact that satisfies the criterion. For document-based evidence: the document type, the required content, and whether a link or upload is required. For quantitative evidence: the data source, the collection methodology at a level of detail sufficient for independent replication, and the time period the evidence must cover. For external verification evidence: the verifying party, the scope of what they verified, and what form their verification must take.

**Why it is required:** A criterion without an evidence form is an assertion without a verification path. Reviewers cannot assess evidence they cannot locate, and applicants cannot produce evidence they have not been told to collect. The evidence form closes the loop between the measurement claim in the criterion intent and the data that supports it.

**Failure mode when absent:** Applicants submit diverse artifact types in response to the same criterion, some of which satisfy the measurement intent and some of which do not. Reviewers make implicit artifact quality judgments that are inconsistent across the cohort. The resulting data cannot be audited because there is no specification against which to audit it.

### 3.5 Compliance Threshold

**What it requires:** For any field or criterion that references an external standard, the referencing party must specify: which components of the external standard apply to this criterion; what evidence satisfies each component; and what the minimum threshold for passage is (e.g., all nine indicators must be met, or at least six of nine indicators must be met with the remaining three requiring documented mitigation plans).

**Why it is required:** External standards are rarely binary. The Digital Public Goods Standard has nine indicators, each with multiple sub-requirements. A criterion that says "Qualifies as DPG" without a compliance threshold delegates interpretation to reviewers: one reviewer may require all nine indicators; another may require six; a third may accept a DPG nomination as sufficient evidence regardless of indicator status. The compliance threshold eliminates this variance by specifying what passage means before any application is reviewed.

**Failure mode when absent:** Reviewer-level interpretation variance becomes the de facto standard. Outcomes are determined partly by which reviewer a given application receives. The data cannot support cross-cohort comparison because the threshold was not held constant.

**Worked illustration (DPG Standard):** A program requiring Digital Public Good status as a gate criterion must specify a compliance threshold that enumerates all nine indicators of the DPG Standard (relevance to a Sustainable Development Goal; use of approved open licenses; clear ownership; platform independence; documentation; non-extraction of data; adherence to privacy and applicable laws; adherence to standards and best practices; and responsible data use policies), states which evidence satisfies each indicator (e.g., "Indicator 2 requires a clearly stated SPDX license identifier in the project repository"), and names the minimum threshold for passage (e.g., "All nine indicators must be satisfied; indicators 1, 2, and 3 are non-waivable"). The compliance threshold must also address the registry question explicitly: the Digital Public Goods Alliance maintains a registry of projects that have previously been assessed against the standard. Registry membership is a record of past assessment, not a guarantee of current qualification. A project in the registry may have changed substantially since assessment; a project not in the registry may currently satisfy all nine indicators. The compliance threshold must state whether registry membership is accepted as sufficient evidence of current qualification, or whether independent indicator assessment is required regardless of registry status. Leaving this unstated produces the most common DPG evaluation failure: reviewers who check the registry as a proxy for indicator assessment, applying a standard the funder did not actually specify. A reference that says "the project must meet the DPG Standard" without this compliance threshold is not a criterion specification; it is a label.

---

## Part IV: The Three-Stage Process

WALKRI specifies a three-stage process for producing WALKRI-conformant fields. The stages may be traversed by a funder designing new fields, an auditor reviewing existing fields, or an AI assistant guiding either. All three stages are required for WALKRI certification. A form produced by skipping Stage 1 or Stage 3 may appear complete but fails the conditions that make the field work in practice.

### 4.1 Stage 1: Ideation

**What the stage produces:** An ideation record: a structured document that names each information need the form is intended to satisfy, the decision that each piece of information will inform, and the failure mode if that information is missing or imprecise. The ideation record is not published to applicants; it governs the field design process in Stage 2.

**Who performs it:** The question-holder: the funder, program, organization, or researcher who will use the collected data to make decisions.

**How it connects to Stage 2:** Each information need in the ideation record becomes the input for one field specification in Stage 2. The criterion intent for each Stage 2 field is derived directly from the ideation record's description of what the information need actually is. If a Stage 2 field cannot be traced to an ideation record entry, that field lacks a documented rationale and cannot be certified.

**Failure mode when skipped:** Fields created without an ideation record tend to be labels rather than instruments. The creator encodes what they assumed the question was rather than what they actually needed to know. When the data fails to support the decision it was collected for, there is no ideation record to diagnose where the design broke down.

### 4.2 Stage 2: Specification

**What the stage produces:** A WALKRI field specification: a structured document for each field containing all five criterion specification requirements from Part III. The field specification is the artifact that form tools render and that the WALKRI Audit Tool assesses.

**Who performs it:** The question-holder, working from the ideation record, or a field specification practitioner working from a brief provided by the question-holder. The WALKRI Ideation Tool and the WALKRI Audit Tool (described in Part IX) support this stage.

**How it connects to Stage 3:** The operational definition and examples in the Stage 2 specification are the source material for Stage 3 applicant guidance. Stage 3 does not add new definitional content; it translates the Stage 2 specification into applicant-facing language. If the Stage 2 specification is incomplete, the Stage 3 guidance will be incomplete.

**The pre-publishing quality gate:** Before any field is shown to applicants, it must pass an AI-assisted review that assesses the field specification against Parts III through VII of this standard. The review flags any of the five criterion specification requirements that are absent or insufficient. Flags are either resolved (the specification is revised to address the flag) or overridden. An override requires a documented justification explaining why the flag does not apply to this field's context. Overrides are recorded in the conformance record produced at certification; they are not failures, but they are disclosed. A field with unresolved and undocumented flags is not eligible for certification.

**Failure mode when skipped:** Fields are built directly from the ideation record without passing through formal specification. The intent is embedded in the question-holder's head rather than in a document. Reviewer inconsistency emerges because there is no specification to adjudicate disputes. Downstream data consumers inherit a dataset with no machine-readable field definitions.

### 4.3 Stage 3: Applicant Guidance

**What the stage produces:** Applicant-facing documentation accompanying each field. This documentation explains: what the field is asking; what a complete response looks like (with at least one positive example); what common incomplete or incorrect responses look like (with at least one negative example); and why the field exists (briefly, as context, not as justification).

**Who performs it:** The question-holder or a communications practitioner working from the Stage 2 field specification. The WALKRI Guidance companion document (WALKRI-guidance-0_1_0.md) provides templates and worked examples.

**How it connects to Stage 2:** Stage 3 documentation is derived from Stage 2's operational definition and examples. No new definitional content is introduced in Stage 3. The translation from specification language (designed for precision) to applicant language (designed for comprehension) is the core work of this stage.

**Failure mode when skipped:** Even a precisely specified field produces inconsistent responses if applicants cannot interpret it correctly. The failure mode is structurally identical to the failure mode of an underspecified field: interpretation variance in the applicant population produces nominally consistent data with hidden definitional variance.

---

## Part V: Data Quality Standards

Five data quality standards apply to all fields across all obligation modes. These standards were moved from CROSS Part VIII and are reproduced here as WALKRI's independent quality framework. They apply whether or not CROSS is the governing obligation standard.

For each standard, the assessment question is what an auditor asks when evaluating a field. The failure mode describes what happens to the data when the standard is not met. The connecting note identifies which criterion specification requirement from Part III the standard most directly enforces.

### 5.1 Validity

**Assessment question:** Does the measurement instrument have a documented logical chain from the evidence specified in the evidence form to the result claimed in the criterion intent?

**Failure mode:** The field measures a proxy for the intended construct rather than the construct itself, but the proxy relationship is undocumented. Analysis treats the measurement as a direct observation of the construct and reaches conclusions that are valid for the proxy but not for the construct. The error is invisible because there is no criterion intent statement against which to test the logical chain.

**Application across field types:** For quantitative indicators, validity requires that the construction methodology produces a number that logically represents the criterion intent's measurement claim. For binary completion criteria, validity requires that the evidence form specifies an artifact whose presence or absence logically indicates the criterion. For qualitative narrative fields, validity requires that the scope defined in the operational definition logically captures the dimension the criterion intent claims to measure.

**Connection to Part III:** Validity most directly enforces the criterion intent requirement (3.1), because a validity failure is a failure to connect the evidence form to the criterion intent through a logical chain.

### 5.2 Integrity

**Assessment question:** Is evidence collection separated from the actor who benefits from a favorable outcome?

**Failure mode:** Self-reported evidence with no third-party verification produces data whose accuracy is systematically biased toward favorable outcomes. The bias is not necessarily dishonest; actors rationally interpret ambiguous situations in ways that favor their position. Without separation between the evidence collector and the beneficiary, the data reflects this rational bias and cannot be used to compare actors on a common scale.

**Application across field types:** For quantitative indicators, integrity requires an independent data source or a verification pathway that separates the reporting actor from the data. For binary completion criteria, integrity requires that the specified artifact can be verified by a reviewer without relying on the applicant's characterization of it. For qualitative narrative fields, integrity is structurally harder to enforce; the standard applies as a design aspiration and a disclosure requirement (the reviewer must know that the field relies on self-report).

**Connection to Part III:** Integrity most directly enforces the evidence form requirement (3.4), because the evidence form is where the source and verification pathway of the evidence are specified.

### 5.3 Precision

**Assessment question:** Is the measurement instrument capable of detecting differences at the magnitude relevant to the decisions the data will inform?

**Failure mode:** A single-select field with three options (low, medium, high) cannot detect the difference between a program that reached 10 people and a program that reached 100 people if both fall into the "low" bucket. If the decision requires distinguishing between these programs, the instrument is too coarse to support it. The failure produces a dataset that appears complete but is informationally insufficient for its stated purpose.

**Application across field types:** For quantitative indicators, precision requires that the unit and counting rule are fine-grained enough to detect the relevant differences. For binary completion criteria, precision is binary by construction; the precision question is whether the binary distinction is the right one or whether the decision requires a more granular assessment. For qualitative narrative fields, precision requires that the scope defined in the operational definition is narrow enough to produce responses that are meaningfully comparable.

**Connection to Part III:** Precision most directly enforces the response form requirement (3.3), because the response form determines the resolution of the measurement instrument.

### 5.4 Reliability

**Assessment question:** Is the methodology for collecting and interpreting this field consistent across reporting periods and across reviewers within a single reporting period?

**Failure mode:** A field whose interpretation changes across reporting periods produces data that cannot be compared over time. A field whose interpretation varies across reviewers within a reporting period produces data that reflects reviewer assignment rather than applicant characteristics. Both failures produce longitudinal or cross-sectional analysis whose conclusions cannot be attributed to changes in the underlying population.

**Application across field types:** For quantitative indicators, reliability requires that the construction methodology is documented in enough detail that it can be applied consistently across periods without re-interpretation. For binary completion criteria, reliability requires that the evidence form specifies a verifiable artifact rather than a judgment call. For qualitative narrative fields, reliability requires a scoring rubric or codebook that reviewers apply consistently; a field without a rubric is inherently unreliable.

**Connection to Part III:** Reliability most directly enforces the operational definition requirement (3.2), because consistency of interpretation across periods and reviewers depends on the definition being precise enough to constrain interpretation.

### 5.5 Timeliness

**Assessment question:** Is the evidence specified in the evidence form current to the decision cycle for which the data is being collected?

**Failure mode:** Evidence that is technically present but outdated misleads decisions that depend on the current state of the applicant. A three-year-old impact assessment submitted as evidence of current reach produces a favorable data point for a decision that should have been made on current information. The decision is made on stale data and the failure is invisible because the evidence form did not specify a recency requirement.

**Application across field types:** For quantitative indicators, timeliness requires that the evidence form specifies the time period the data must cover relative to the submission date. For binary completion criteria, timeliness requires that the artifact attesting to completion is recent enough to be probative. For qualitative narrative fields, timeliness requires that the scope in the operational definition specifies whether responses must reflect current practice or may reflect historical practice.

**Connection to Part III:** Timeliness most directly enforces the evidence form requirement (3.4), because the evidence form is where recency requirements and time-period specifications must appear.

---

## Part VI: External Standard Reference Protocol

Any field or criterion that references an external standard must follow the External Standard Reference Protocol. A reference to an external standard without this protocol is not a criterion specification; it is a delegation of interpretation to whoever reviews the field. The resulting data is unauditable and inconsistent.

### 6.1 Required Reference Elements

A conformant external standard reference must include four elements:

**URL:** The canonical URL of the external standard being referenced. The URL must resolve to the standard document itself, not to a landing page or organizational homepage.

**Version anchor:** A date-stamped access record, a version number, or a content hash sufficient to identify the exact version of the external standard that was consulted. External standards evolve; a reference without a version anchor cannot be audited because the auditor cannot determine which version of the standard was in effect when the field was designed. For standards that use dated versions (e.g., "DPG Standard v1.1.9, accessed 2025-11-01"), the access date is the version anchor. For standards that use semantic versioning, the version number is the anchor. For standards without formal versioning, a content hash (SHA-256) of the document as accessed is the anchor.

**Scope:** A statement of what part of the external standard applies to this criterion. Many external standards are multi-part documents; the scope statement identifies which indicators, sections, or requirements are germane.

**Compliance threshold:** The enumeration of which components of the external standard must be satisfied for passage, what evidence satisfies each component, and the minimum threshold for passage. The compliance threshold is the mechanism that prevents reviewer-level interpretation variance from determining outcomes.

### 6.2 The Compliance Threshold Requirement

The compliance threshold is the most frequently omitted element of the external standard reference protocol, and its absence is the most consequential failure. When a threshold is absent, reviewers must construct their own interpretation of what "compliant with the referenced standard" means. Different reviewers construct different interpretations. The data reflects reviewer assignment rather than applicant compliance with the standard.

A compliance threshold is not a summary of the referenced standard. It is a specification of how the referenced standard applies to this specific criterion in this specific context. The threshold must be explicit enough that a reviewer who had never seen the external standard before could apply it consistently with a reviewer who had studied it in depth.

### 6.3 Worked Illustration: The DPG Standard

The Digital Public Goods Standard (DPGS) is a nine-indicator standard used by the Digital Public Goods Alliance to assess whether a digital solution qualifies as a digital public good. It is the most common external standard referenced in open-source software and technology grant programs.

A program that uses DPG qualification as a gate criterion must produce a compliance threshold that:

1. Names all nine indicators: (1) relevance to a Sustainable Development Goal, (2) use of an approved open license, (3) clear ownership, (4) platform independence, (5) documentation, (6) non-extraction of data, (7) adherence to privacy and applicable laws, (8) adherence to standards and best practices, and (9) responsible data use policies.

2. States what evidence satisfies each indicator. For example: Indicator 2 requires a clearly stated SPDX license identifier in the project repository's root-level LICENSE file or README; a reference to a license in prose text without an SPDX identifier does not satisfy this indicator.

3. States the minimum threshold for passage. For example: All nine indicators must be satisfied for gate passage. Indicators 1, 2, and 3 are non-waivable. For indicators 4 through 9, an applicant who cannot satisfy an indicator may submit a documented mitigation plan; a maximum of two indicators may be satisfied via mitigation plan.

A reference that says "the project must meet the DPG Standard" without these elements is not a compliance threshold. It is a label.

**The registry distinction.** The Digital Public Goods Alliance registry records past assessments. Registry membership confirms that a project was assessed at some prior point and met the standard at that time. It does not confirm current qualification: the project may have changed, its dependencies may have changed, or the standard itself may have been updated. A compliance threshold that accepts registry membership as evidence of current qualification must state this explicitly and accept the limitation that comes with it. A compliance threshold that requires current indicator assessment must specify which indicators apply and what evidence satisfies each, regardless of whether the project is registered. Leaving the registry question unstated is the most frequently observed DPG compliance threshold failure.

---

## Part VII: Provenance and Schema Requirements

WALKRI-conformant data collection produces two categories of obligations: provenance fields that must accompany the data, and schema requirements that govern how field definitions change over time.

### 7.1 Provenance Fields

Every WALKRI-enriched dataset must include the following provenance fields at the dataset level and, where technically feasible, at the field level:

**Field creator identity:** An organizational identifier or practitioner identifier for the entity that designed the field specification. This field enables downstream consumers to contact the specifying entity for definitional clarification and supports accountability for data quality decisions.

**Specification timestamps:** ISO 8601 timestamps for when the field specification was created and last modified. These timestamps are distinct from the timestamps on the collected data; they record the history of the instrument, not the history of responses to it.

**WALKRI version:** The version of this standard that governs the field specification. Version differences in the standard may affect the interpretation of conformance; downstream consumers need this information to assess whether a field specification meets the version of the standard they are using.

**Form tool identifier:** The class of form tool used to render the field (e.g., "KoBoToolbox," "REDCap," "Fillout"), not the specific instance or deployment. This supports reproducibility assessment: a downstream consumer can determine whether the rendering tool class imposes any known constraints on response capture.

**Field specification version:** The version of the field specification itself, distinct from the WALKRI version. Field specifications evolve independently of the standard; the field specification version tracks changes to the definition of a specific field.

### 7.2 Schema Requirements

WALKRI imposes three schema requirements on organizations that collect data under WALKRI-conformant fields:

**Consistency across reporting periods:** Field names and their associated definitions must remain consistent across reporting periods unless a versioned change is documented. A field name that appears in two consecutive reporting periods is assumed to refer to the same construct; if the construct has changed, the field must be versioned rather than silently redefined.

**Versioning of changes:** Any change to a field definition produces a new field specification version. The prior definition is retained in the specification record and remains accessible. A downstream consumer aggregating data across reporting periods must be able to access the definition that governed each period's data.

**Comparability documentation:** Changes that affect comparability across reporting periods must be documented with the date of the change, the nature of the change, and its implications for prior data. If an option was added to a single-select field in a new reporting period, the documentation must state what applicants who selected the nearest equivalent option in prior periods were actually reporting, and whether the new option represents a previously unmeasured category or a refinement of an existing one.

### 7.3 Alignment with Output Standards

WALKRI's provenance fields and schema requirements are designed to produce output that meets three external data standards. The alignment is declared here as a design commitment; the detailed mapping specifications appear in WALKRI-interface-specification-0_1_0.md.

Croissant alignment ensures that WALKRI-enriched datasets are machine-readable by ML pipelines without manual metadata reconstruction. FAIR alignment ensures that WALKRI-enriched datasets are findable, accessible, interoperable, and reusable by any downstream consumer. W3C PROV alignment ensures that the provenance history of any data element can be expressed in a standard, tool-independent provenance graph.

---

## Part VIII: WALKRI Certification

### 8.1 What Certification Means

WALKRI certification means that a form or field set has been audited against Parts III, IV, V, VI, and VII of this standard and meets the minimum conformance threshold. Certification is per form version, not per organization. An organization may hold certification for one version of a form while a concurrent version is under audit.

Certification does not mean that the certified form will produce perfect data. It means that the form's fields are specified with sufficient precision that the sources of variance in the collected data are attributable to real differences in the applicant population rather than to definitional ambiguity in the instrument.

### 8.2 Certification Scope

A change to any field definition triggers re-audit for that field. If a form is modified between reporting periods, the modified fields must be re-audited; fields that were not changed retain their prior certification status. The conformance record documents which fields were audited in which audit cycle, so downstream consumers can determine whether the version of the form used in a given reporting period was certified for that period.

### 8.3 The Conformance Record

Certification produces a conformance record: a structured document that is the primary artifact of the certification process. The conformance record contains:

- The audit date (ISO 8601)
- The WALKRI version applied
- The form version audited
- For each field: the field name, the field specification version, and the pass/fail/override status of each of the five criterion specification requirements
- For each override: the text of the flag, the justification for the override, and the name or identifier of the person who authorized it

The conformance record is the artifact that a WALKRI-certified program can produce to demonstrate data quality to downstream data consumers, funders, or research partners. It is the machine-readable proof that the form was designed to a known standard.

### 8.4 Minimum Conformance Threshold

For a field to pass certification, it must satisfy all five criterion specification requirements. A field that satisfies four of five requirements does not pass; it produces a flag that must be resolved or overridden. The minimum conformance threshold for a form is that all fields pass certification, with overrides permitted where documented. A form with unresolved, undocumented flags cannot be certified.

---

## Part IX: Implementation Architecture

WALKRI is implemented through three product-layer tools. These tools are described in implementation documents; this Part names them and states their relationship to the standard.

### 9.1 WALKRI Ideation Tool

The WALKRI Ideation Tool guides question-holders through Stage 1, producing an ideation record. It prompts the question-holder to name each information need, identify the decision it informs, and articulate the failure mode if the information is imprecise or absent. The output is a structured document formatted for direct use as input to the WALKRI Audit Tool in Stage 2.

### 9.2 WALKRI Audit Tool

The WALKRI Audit Tool assesses field specifications against Parts III through VII of this standard. It is the pre-publishing quality gate described in Part IV. The tool accepts a field specification in JSON Schema format (or in the secondary compatible formats specified in Part II) and returns a conformance assessment identifying which of the five criterion specification requirements are satisfied and which produce flags. Flags are annotated with the specific failure mode (drawn from Part III) and a suggested resolution. The tool produces the conformance record described in Part VIII when a full form audit is complete.

### 9.3 WALKRI Enrichment Layer

The WALKRI Enrichment Layer is a post-submission webhook processing system that adds provenance fields to collected data and transforms it into Croissant/FAIR/W3C PROV-aligned output. It operates downstream of the form tool's data collection layer, receiving submitted responses and enriching them with the field-level and dataset-level provenance fields specified in Part VII. The Enrichment Layer does not modify responses; it adds metadata to the dataset. The enriched output is the artifact passed to downstream data consumers, analysts, and AI pipelines.

---

## Part X: Companion Documents

WALKRI v0.1.0 is accompanied by six companion documents.

**WALKRI-guidance-0_1_0.md** provides practitioner guidance for traversing the three-stage process. It contains worked examples of ideation records, field specifications, and applicant guidance documents for common field types.

**WALKRI-templates-0_1_0.md** provides structured templates for each artifact produced by the three-stage process: the ideation record template, the field specification template, and the applicant guidance document template. Templates are provided in JSON Schema format and in a human-readable structured form.

**WALKRI-rubric-0_1_0.md** provides the scoring rubric used by the WALKRI Audit Tool. It operationalizes each of the five criterion specification requirements as an auditable criterion with pass/fail/override conditions. Practitioners and auditors use it to understand how the Audit Tool reaches its assessments and to conduct manual audits where the tool is not available.

**WALKRI-worked-examples-0_1_0.md** provides full worked examples of WALKRI-conformant and non-conformant fields for six common field types: single-select categorical, multi-select, binary (yes/no), numeric with counting rule, URL with evidence specification, and qualitative narrative. Each example includes the non-conformant version, the diagnosis using Part III's failure modes, and the conformant revised version.

**WALKRI-interface-specification-0_1_0.md** provides the detailed technical specifications for the three interfaces described in Part II, including the JSON Schema mapping, the REDCap and XLSForm compatibility mappings, and the detailed alignments with Croissant, FAIR, and W3C PROV.

**WALKRI-CROSS-boundary-0_1_0.md** provides the formal boundary document specifying the division of responsibility between CROSS and WALKRI. It is the reference document for implementers who are deploying both standards and need to know, for any given requirement, whether CROSS or WALKRI is the governing authority.

---

## Appendix A: Open Design Questions (v0.1.0)

The following questions are genuine open design problems as of v0.1.0. They are recorded here because the right answer is not yet settled. The stakes for each question are stated alongside the question.

**Question 1: Tiered minimum conformance threshold.** The current specification requires all five criterion specification elements at Stage 2 certification. A plausible alternative is a tiered minimum: criterion intent and evidence form are required at Stage 1 (ideation audit), and all five elements are required at Stage 2 (publication certification). The rationale for the tier is that Stage 1 is an internal design document and imposing full specification requirements at that stage may slow down ideation in ways that reduce the quality of the ideation record rather than improving it. The risk is that organizations treat Stage 1 certification as sufficient and never complete Stage 2, producing fields that are partially specified and receiving credit for a partial pass. Resolution requires empirical evidence on how organizations actually use the tiered process.

**Question 2: Qualitative and narrative fields.** The five criterion specification requirements were designed primarily for categorical, binary, and quantitative fields. Open-ended narrative fields resist operational definition in the same way: the construct they measure is often inherently multidimensional, and the value of the field is precisely its openness to unanticipated content. Requiring a detailed operational definition for a narrative field may produce a constrained field that defeats the purpose of asking an open question. The design question is whether WALKRI should specify a distinct specification pathway for inherently qualitative fields, or whether the existing requirements should be interpreted more flexibly for these cases. The risk of flexibility is that it becomes a loophole through which underspecified fields are classified as "inherently qualitative" to avoid specification work.

**Question 3: Public vs. private certification registry.** This version of the standard does not specify whether the conformance record produced at certification must be publicly available or may be held privately by the certifying organization. A public registry would allow downstream data consumers to verify certification status independently, which improves the downstream interface described in Part II. It would also create a record of override patterns across the ecosystem, which could improve the standard over time. A private certification model reduces the burden on certifying organizations (who may have proprietary form designs they do not want to publish) and may improve adoption. The question has no dominant answer; it depends on the trust model of the ecosystem in which WALKRI is deployed.

**Question 4: AI-generated field specifications.** The three-stage process described in Part IV is designed for human question-holders assisted by AI tools. A foreseeable use case is AI systems that generate field specifications directly, bypassing Stage 1 (because the AI constructs the ideation record) and Stage 3 (because the AI generates applicant guidance automatically). The design question is whether AI-generated specifications should be treated identically to human-generated specifications for certification purposes, or whether they require a distinct audit pathway that addresses the failure modes specific to AI generation (e.g., specifications that are syntactically complete but semantically misaligned with the question-holder's actual intent). This question will become more pressing as AI-assisted form design becomes the norm rather than the exception.
