# WALKRI: Working Architecture for Legible, Knowledge-Ready Intake

Version 0.1.4 | 2026-05-18 | CC0

Every intake form has questions. No standard has ever required those questions to function as measurement instruments before anyone answers them. WALKRI is the first.

![GIGO pipeline: obligation never specified and questions not designed to measure enter a funnel, producing data that cannot be compared, aggregated, or trusted. No existing tool touches the source.](assets/gigo-pipeline.png)

A field that does not specify what it measures is a label. Labels produce responses. They do not produce data. The difference matters at every layer: a reviewer cannot assess what was not defined, an analyst cannot aggregate what was not measured consistently, and an institutional funder cannot verify what was never specified. WALKRI addresses this at the source, before any applicant sees the form.

WALKRI is a companion standard to CROSS (Common Reporting Outcome Standards Schema). Together they are published as CROSS+WALKRI. CROSS specifies the obligation architecture of a grants round: what grantees must demonstrate at each payment gate. WALKRI specifies the quality of the fields through which that demonstration is collected. CROSS without WALKRI produces a well-structured obligation with a poorly specified measurement surface. WALKRI without CROSS produces high-quality fields with no accountability architecture behind them. The two are designed to be used together.

WALKRI is also portable: it works with any obligation standard, not only CROSS.

---

## What WALKRI specifies

Five requirements apply to every intake field before any applicant sees it.

A field must specify what it measures, not just what it asks. A field must define the unit of measurement or the categories of valid response. A field must state the population or scope to which responses apply. A field must identify the data source or evidence type required to answer it. A field must declare how its responses will be used in evaluation.

A field that satisfies all five is a measurement instrument. A field that fails any one is a label. The distinction is structural, not a matter of degree. Labels produce data that cannot be compared, aggregated, or trusted downstream.

WALKRI also specifies five gate declaration instruments: the Obligation Mode Declaration, the Evidence Standard Declaration, the Comparison Frame Declaration, the Attribution Claim Declaration, and the Sufficiency Assessment Declaration. These instruments apply at the program level, before individual fields are designed, and establish the accountability context that field design must satisfy.

---

## Where WALKRI sits in the stack

![CROSS+WALKRI stack: any form builder or grants platform below, CROSS+WALKRI in the middle providing obligation architecture and field quality, Web3 and institutional standards above. One conformant round, both directions, no extra work.](assets/stack-diagram.png)

WALKRI operates on JSON Schema, which underlies every major form builder. Fillout, Typeform, KoBoToolbox, REDCap, and any comparable tool already output JSON Schema. A WALKRI-conformant field specification produced in any of those tools is equally conformant as one produced in a dedicated audit instrument. Programs do not change their stack. They specify their fields correctly before publishing the form.

Above the field level, a CROSS+WALKRI-conformant round produces data that is structurally comparable across programs and auditable after the fact, not because every program uses the same indicators or the same vocabulary, but because every program has declared its obligation architecture and designed its fields to specification. That position in the stack is why compatibility is the primary benefit: it does not require replacing what already exists below, and it makes everything built above it interoperable with everything else.

Both CROSS and WALKRI are published CC0. No licensing, no arrangements, no asks.

---

## Who this is built for

![Cascade pyramid: Grantees and Reviewers at the base, Operators and Platform Providers, Analysts and Institutional Funders, Strategic Planners at the apex. Smaller decisions at the base; billions at stake at the top. Strategic level value requires ecosystem-wide adoption to materialise.](assets/for-all-pyramid.png)

WALKRI serves all six layers of the grants ecosystem without modification: grantees, reviewers, program operators, platform providers, analysts, and institutional funders. The field quality that WALKRI requires at the intake layer compounds upward: an analyst consuming data from ten WALKRI-conformant programs gets structured, comparable, trustworthy data automatically. An institutional co-funder gets compliance output as a byproduct of the round being run correctly. Strategic planners deciding how to allocate at scale eventually get something real to work with instead of GIGO.

---

## Documents

- `WALKRI-standard-0_1_4.md` - Main specification
- `WALKRI-interface-specification-0_1_0.md` - Three-interface specification (upward, lateral, downstream)
- `WALKRI-CROSS-boundary-0_1_0.md` - Formal boundary between WALKRI and CROSS
- `WALKRI-guidance-0_1_2.md` - Practitioner guidance including gate declaration instrument guidance
- `WALKRI-templates-0_1_2.md` - Field specification templates, worksheets, and gate declaration forms
- `WALKRI-rubric-0_1_2.md` - Audit and certification rubric with gate declaration assessment
- `WALKRI-worked-examples-0_1_2.md` - Worked examples from Epoch 12 and comparable programs

---

## Ecosystem position

Every major form and grants tool was examined before WALKRI was designed. The table below shows where each sits.

| Tool / Standard | Layer | Obligation architecture | Field quality | Web3 output | Institutional output |
|:--|:--|:--|:--|:--|:--|
| **WALKRI** | Specification | n/a (see CROSS) | Five pre-publication field requirements | n/a | USAID data quality criteria |
| **CROSS** | Specification | Three modes, four-gate sequence | n/a (see WALKRI) | DAOIP-5, W3C VCs, OpenGrants | OECD DAC, IRIS+, USAID PIRS |
| [USAID PIRS](https://2017-2020.usaid.gov/sites/default/files/documents/1861/Recommended_PIRS_for_USAID_indicators_0.pdf) | Compliance framework | n/a | Five data quality criteria (retrospective) | n/a | Required indicator documentation |
| [IRIS+](https://iris.thegiin.org/standards/) | Vocabulary | n/a | n/a | n/a | Indicator reference library |
| [Logframe / LFA](https://www.oecd.org/en/topics/sub-issues/development-co-operation-evaluation-and-effectiveness/evaluation-criteria.html) | Methodology | ToC hierarchy only | n/a | n/a | OECD DAC (partial) |
| [KarmaGAP](https://docs.gap.karmahq.xyz/) | Post-funding tracking | n/a | n/a | EAS milestone attestations | n/a |
| [DAOIP-5](https://github.com/metagov/daostar/blob/main/DAOIPs/daoip-5.md) | Interoperability | n/a | n/a | Grants data portability | n/a |
| Form builders (Fillout, Typeform, KoBoToolbox, REDCap) | Collection layer | n/a | n/a | JSON Schema output | n/a |

The pattern: every tool either collects data after fields are defined, tracks outcomes after work is done, provides indicator vocabulary, or handles interoperability. None specify what makes a field a measurement instrument before it is published. WALKRI is the first standard that does.

---

## WALKRI requirements and USAID data quality criteria

USAID requires five data quality criteria to be satisfied for every performance indicator, documented in a Performance Indicator Reference Sheet before data collection begins. WALKRI's five field requirements encode the same underlying principles, applied at the field specification stage rather than assessed retrospectively.

| USAID criterion | What it requires | WALKRI requirement | How WALKRI satisfies it |
|:--|:--|:--|:--|
| Validity | Data measure what they intend to measure | Criterion intent (3.1) + Operational definition (3.2) | Written statement of what the field measures, with qualifying and non-qualifying examples that constrain interpretation |
| Reliability | Consistent results across periods and collectors | Operational definition (3.2) + Compliance threshold (3.5) | Precise definition reduces interpretive variance; calibration record requirement ensures consistent assessment across reviewers |
| Precision | Instrument detects differences of relevant magnitude | Response form (3.3) | Response type must be justified as appropriate for the criterion intent; the choice of response form determines measurement resolution |
| Integrity | Collection is separated from entities benefiting from favorable outcomes | Evidence form (3.4) | Specifies the artifact type and independent access path, structurally separating what counts as evidence from who benefits |
| Timeliness | Data available for management use | Evidence form (3.4) | Must specify recency requirement and time-period specifications for when evidence was collected |

The critical distinction: USAID applies these criteria as a Data Quality Assessment procedure run retrospectively after data is collected. WALKRI applies them at the field specification stage, before any applicant sees the form. A WALKRI-conformant field satisfies the USAID DQA requirements as a structural consequence of having been specified correctly, without a separate assessment.

WALKRI adds three requirements beyond the USAID five: written justification for why the response form is appropriate for the criterion intent, participatory specification documentation where applicable, and compliance threshold specification for fields referencing external standards. These have no USAID equivalent.

The formal compatibility statement is in `statements/USAID-PIRS-CROSS-WALKRI-compatibility-0_1_0.md`.

---

## License

CC0: dedicated to the public domain under Creative Commons Zero v1.0 Universal. See `LICENSE` for the full dedication.

Any grants ecosystem can adopt WALKRI without adopting CROSS, the Coordination Structural Integrity Suite, or any other standard. The five field requirements and gate declaration instruments stand alone.
