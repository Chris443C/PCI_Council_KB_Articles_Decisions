---
id: "DSS-ROC-S6.2-001"
title: "Wording guidance: ROC Section 6.2 sampling of system components narrative"
slug: "dss-roc-s6.2-sampling-narrative"
programme: "DSS"
standard_version: "4.0.1"
requirement: "ROC-S6.2"
sub_requirement: ""
related_requirements: []
article_type: "wording-guidance"
status: "draft"
created_date: "2026-03-12"
agreed_date: ""
meeting_id: ""
review_due: ""
superseded_by: ""
supersedes: ""
proposed_by: "[To confirm from original submission]"
approved_by: ""
second_reviewer: ""
source_references:
  - "PCI DSS v4.0.1 ROC Template v1.1 — Section 6.2 Sampling of System Components"
applies_to: ["ROC"]
applies_to_regions: ["global"]
applies_to_merchant_levels: ["all"]
tags: ["sampling", "roc-wording", "section-6.2", "system-components", "methodology"]
summary: "Replacement wording for ROC Section 6.2 that removes the load balancer example and uses environment-agnostic language based on make, model, function, and configuration groupings."
disclaimer_accepted: false
contains_standard_excerpts: false
---

# DSS-ROC-S6.2-001 — Wording guidance: ROC Section 6.2 sampling of system components narrative

> **⚠️ DRAFT — Not yet agreed.** This article has not been reviewed at a Patronusec Council
> meeting. Do not rely on it in active assessments until status is set to `agreed`.

> **Disclaimer:** This article represents the agreed internal interpretation of Patronusec
> assessors as of the agreed date above. It does not constitute an official PCI SSC
> position. QSAs should exercise professional judgement and consult the PCI SSC directly
> for formal clarification where required.

> **Standard version:** Applicable to PCI DSS v4.0.1 ROC Template v1.1 only.
> Review required if a revised ROC template is published.

> **Wording guidance:** The template text below is approved for internal use in Patronusec
> assessments only. It must not be shared with entities, clients, or third parties without
> the written approval of the Head of QA.

---

## Background

The ROC Template Section 6.2 provides a standard narrative for describing the assessor's sampling approach. The current template wording uses a specific load balancer example as an illustration of homogeneous component grouping.

In practice, this example causes recurring issues:

- In environments without load balancers (or where load balancers are out of scope), the example is irrelevant and attracts reviewer comments
- The phrase "i.e." makes the example read as a definition rather than an illustration, making it harder to adapt to different environments
- Assessors frequently edit the wording per-engagement to remove the example, but do so inconsistently

The proposed replacement retains the intent of the original — explaining that components with common characteristics were grouped, with a representative sample taken, and unique components included separately — but removes the technology-specific example in favour of neutral, environment-agnostic language based on make, model, function, and configuration.

---

## Agreed Wording

### Variant: Standard (replaces current Section 6.2 template wording)

> **Context:** ROC Section 6.2 "Sampling of System Components" — the assessor's narrative describing how samples were selected. This variant replaces the current template wording in all new ROC deliverables once agreed.

> **Agreed text:**
>
> Sampling of system components was determined by the assessor to accurately reflect the range of in-scope devices and component types present in the environment. Sample selection was based on common characteristics such as make, model, function, and configuration. Where multiple components shared the same relevant characteristics, a representative sample was selected. Components with unique software, function, or configuration were included separately within the sample sets.

> **Notes on use:**
> - This wording is intentionally generic and applies to any environment type. Do not re-add technology-specific examples unless the assessment involves a genuinely unusual configuration that requires explanation.
> - No placeholders — this wording is used as-is. The entity-specific detail (which components, how many, what characteristics) belongs in the body of the assessment, not in this introductory narrative.
> - If the sampling approach deviates from standard practice (e.g. a particularly large or complex environment requiring a more detailed justification), extend this wording with an additional sentence rather than replacing it.

---

### Variant: Extended (for complex or large environments)

> **Context:** Use in addition to the Standard variant where the environment is large or complex enough that a brief additional justification of the sampling approach is warranted — e.g. multi-site, mixed cloud/on-premises, or highly heterogeneous component sets.

> **Agreed text:**
>
> Sampling of system components was determined by the assessor to accurately reflect the range of in-scope devices and component types present in the environment. Sample selection was based on common characteristics such as make, model, function, and configuration. Where multiple components shared the same relevant characteristics, a representative sample was selected. Components with unique software, function, or configuration were included separately within the sample sets.
>
> Given the scale and complexity of the in-scope environment, the assessor applied additional consideration to ensure sample coverage across [key dimensions, e.g. "geographically distributed sites / mixed on-premises and cloud-hosted components / multiple operating system types"]. The resulting sample set is considered by the assessor to provide sufficient breadth and depth to support accurate findings across the assessed environment.

> **Notes on use:**
> - Use only where the additional justification genuinely adds context. Do not use this variant as a default — the Standard variant is sufficient for the majority of assessments.
> - Replace `[key dimensions]` with the specific characteristics of the environment being described.

---

## Current Wording (for reference)

The wording this article replaces, currently in the ROC Template v1.1 Section 6.2:

> "Sampling of System Components — The assessor selected the number of samples as an accurate reflection of the various configurations of components i.e. all load balancers have the same configuration, therefore the assessor selected only a single component as a sample as it reflects the same configuration on the other components. Components with unique software and/or configurations were included in the sample sets."

**Why this is being replaced:**
- The load balancer example is technology-specific and irrelevant in many environments
- The "i.e." construction makes the example read as a rule rather than an illustration
- In practice, assessors edit it per-engagement inconsistently, creating variation across deliverables

---

## What Not to Write

| Avoid | Reason |
|-------|--------|
| "All [specific technology] components have the same configuration, therefore only one was sampled." | Technology-specific examples invite reviewer questions about whether the configuration claim was verified. The agreed wording avoids this by referring to grouping criteria rather than specific outcomes. |
| "A risk-based approach was used to select samples." | Vague and does not describe the actual selection methodology. The agreed wording is specific about the grouping criteria. |
| Leaving the current template wording unchanged with the load balancer example. | Once this article is agreed, use the Standard variant above instead. |

---

## See Also

- *No directly related KB articles — sampling methodology applies across all requirements*

---

> **Action required before publishing:** Set `agreed_date`, `meeting_id`, `review_due`, `approved_by`, `disclaimer_accepted: true`, and change `status` from `draft` to `agreed` once council review is complete.
