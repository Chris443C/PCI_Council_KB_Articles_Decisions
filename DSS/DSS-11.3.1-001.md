---
id: "DSS-11.3.1-001"
title: "Wording guidance: internal vulnerability scanning using cloud-native continuous scanning tools (Azure Defender, AWS Inspector, GCP, OCI, and equivalents)"
slug: "dss-11.3.1-cloud-native-continuous-scanning-wording"
programme: "DSS"
standard_version: "4.0.1"
requirement: "11.3.1"
sub_requirement: ""
related_requirements: ["11.3.1.1", "11.3.1.2", "11.3.1.3", "6.3.1", "12.3.1"]
article_type: "wording-guidance"
status: "agreed"
created_date: "2026-03-12"
agreed_date: "2026-03-12"
meeting_id: "2026-03-12-monthly"
review_due: "2027-03-12"
superseded_by: ""
supersedes: ""
proposed_by: "C. Ince"
approved_by: "Head of QA"
second_reviewer: ""
source_references:
  - "PCI DSS v4.0.1 Requirements 11.3.1, 11.3.1.1, 11.3.1.2, 11.3.1.3 — Guidance column"
  - "PCI DSS v4.0.1 ROC Template v1.1 — Section 5.3 Quarterly Internal Scan Results"
  - "Microsoft Defender for Cloud documentation — continuous assessment feature"
  - "AWS Amazon Inspector documentation — continuous scanning mode"
  - "PCI DSS v4.0.1 Requirement 6.3.1 — Vulnerability risk ranking"
  - "PCI DSS v4.0.1 Requirement 12.3.1 — Targeted risk analysis"
applies_to: ["ROC"]
applies_to_regions: ["global"]
applies_to_merchant_levels: ["all"]
tags: ["vulnerability-scanning", "11.3.1", "cloud-native", "continuous-scanning", "azure-defender", "aws-inspector", "gcp", "oci", "containers", "ci-cd"]
summary: "Approved ROC wording for Requirements 11.3.1–11.3.1.3 and Section 5.3 where entities use cloud-native continuous vulnerability scanning in place of traditional periodic scan reports."
disclaimer_accepted: true
contains_standard_excerpts: false
---

# DSS-11.3.1-001 — Wording guidance: internal vulnerability scanning using cloud-native continuous scanning tools

> **Disclaimer:** This article represents the agreed internal interpretation of Patronusec
> assessors as of the agreed date above. It does not constitute an official PCI SSC
> position. QSAs should exercise professional judgement and consult the PCI SSC directly
> for formal clarification where required.

> **Standard version:** Applicable to PCI DSS v4.0.1 only.
> Review required before applying to any future standard version.

> **Wording guidance:** The template text below is approved for internal use in Patronusec
> assessments only. It must not be shared with entities, clients, or third parties without
> the written approval of the Head of QA.

---

## Background

Requirements 11.3.1 through 11.3.1.3 require entities to perform internal vulnerability scanning across in-scope components, with high-risk and critical vulnerabilities remediated and validated. The traditional expectation is a periodic (at least quarterly) scan producing a report that clearly identifies all assets scanned, scan dates, and vulnerability findings.

Increasingly, entities hosted in cloud environments are using the cloud provider's native security tooling for continuous or near-real-time vulnerability scanning rather than running traditional scan tools on a schedule. These tools — including Microsoft Defender for Cloud (Azure), Amazon Inspector (AWS), GCP Artifact Analysis, OCI Vulnerability Scanning Service, Alibaba Security Center, and Tencent Vulnerability Scan Service — operate differently from traditional scanners:

- They are typically **always on** across the environment rather than scheduled
- They generate **alerts** when vulnerabilities are identified, not periodic reports
- Once a vulnerability is remediated, it **disappears from the active finding list** — there is no historical report in the traditional sense
- Evidence of scanning is demonstrated through dashboards, time-stamped exports, and alert/remediation logs rather than a point-in-time scan report

This creates a recurring challenge for QSAs: the entity demonstrably has better vulnerability coverage than the quarterly minimum, but the evidence format does not match what QSAs have historically expected. The agreed wording below addresses how to capture this correctly in a ROC.

**Covered tools in this article:**
- Azure: Microsoft Defender for Cloud
- AWS: Amazon Inspector
- GCP: Artifact Analysis / Artifact Registry vulnerability scanning
- OCI: OCI Vulnerability Scanning Service and OCI Registry image scanning
- Alibaba: Security Center
- Tencent: Vulnerability Scan Service / Container image security scanning
- Any equivalent cloud-native continuous scanning tool with comparable capabilities

**Pre-conditions before using this wording:**
The QSA must verify the following before applying any variant below:
1. The tool is enabled across all in-scope components — not selectively enabled on some systems only
2. Time-stamped evidence is available demonstrating continuous activity throughout the assessment period (dashboards, exported finding histories, or audit logs showing scan activity)
3. High-risk and critical vulnerabilities were remediated and follow-up validation is evidenced in the tool's remediation tracking
4. The entity's vulnerability risk-ranking methodology (Req 6.3.1) is documented and applied to classify findings from this tool
5. The scanning is performed by, or the results are reviewed by, personnel with appropriate qualifications and organisational independence

---

## Agreed Wording — Requirement 11.3.1

### Variant: Generic (full)

> **Context:** ROC Requirement 11.3.1 free-text narrative / Assessor's Findings section. Use this variant for the primary description of the scanning approach. Use the Shorter variant where the requirement is clearly and simply met and no special circumstances apply.

> **Agreed text:**
>
> The entity uses % Internal_Vulnerability_Scanning_Tool % to perform internal vulnerability scanning across in-scope CDE and connected system components. Vulnerability assessments are performed on a continuous basis, with time-stamped scan outputs, dashboards, and/or exported reports retained to demonstrate that scanning occurred more frequently than once every three months during the assessment period.
>
> High-risk and critical vulnerabilities, as defined in the entity's vulnerability risk-ranking methodology under Requirement 6.3.1, are tracked through remediation and validated through follow-up scans or updated scan results. The scan tool is maintained with current vulnerability intelligence, and scanning activities are performed by qualified personnel with appropriate organisational independence.

> **Notes on use:**
> - Use only where the tool is enabled continuously across all in-scope systems. Do not use for hybrid environments where some systems are scanned by a traditional tool — describe each scanning approach separately.
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name, e.g. "Microsoft Defender for Cloud", "Amazon Inspector", "GCP Artifact Analysis"

---

### Variant: Shorter

> **Context:** ROC Requirement 11.3.1 narrative where the scanning approach is straightforward and fully evidenced. Suitable where the tool is clearly continuous, coverage is complete, and there are no unusual circumstances.

> **Agreed text:**
>
> The entity's internal vulnerability scanning process is performed using % Internal_Vulnerability_Scanning_Tool %. Evidence reviewed demonstrated continuous vulnerability assessment throughout the assessment period, exceeding the minimum requirement for scanning at least once every three months. High-risk and critical vulnerabilities were remediated and verified through subsequent scan results.

> **Notes on use:**
> - Use only where all pre-conditions are fully met and no caveats apply. If any pre-condition is uncertain, use the Generic (full) variant with additional explanatory text.
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

## Agreed Wording — Requirement 11.3.1.1

### Variant: Generic (full)

> **Context:** ROC Requirement 11.3.1.1 free-text narrative. This sub-requirement covers how non-critical/non-high-risk vulnerabilities are managed — i.e. those not requiring immediate remediation under the entity's risk ranking.

> **Agreed text:**
>
> For vulnerabilities identified through % Internal_Vulnerability_Scanning_Tool % that are not ranked as high-risk or critical under the entity's Requirement 6.3.1 risk-ranking methodology, remediation timeframes are managed in accordance with the entity's targeted risk analysis performed under Requirement 12.3.1. The entity's vulnerability management process includes rescans or follow-up validation, as needed, to confirm such vulnerabilities have been addressed in line with risk-based remediation timelines.

> **Notes on use:**
> - The entity must have a documented targeted risk analysis (Req 12.3.1) that defines remediation timeframes for lower-ranked vulnerabilities. Verify this document exists before using this wording.
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

### Variant: Shorter

> **Context:** Shorter version for 11.3.1.1 where the targeted risk analysis is straightforward and clearly documented.

> **Agreed text:**
>
> Lower-ranked vulnerabilities identified by % Internal_Vulnerability_Scanning_Tool % are addressed according to the entity's targeted risk analysis and are re-evaluated through rescans or follow-up validation as needed.

> **Notes on use:**
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

## Agreed Wording — Requirement 11.3.1.2

### Variant: Generic (full)

> **Context:** ROC Requirement 11.3.1.2 free-text narrative. This sub-requirement covers authenticated scanning — scanning that uses credentials to assess vulnerabilities that are only visible to authenticated users of the system.

> **Agreed text:**
>
> The entity uses % Internal_Vulnerability_Scanning_Tool % to perform authenticated internal vulnerability scanning for in-scope systems that accept credentials for scanning. Systems that do not support authenticated scanning are documented. Where authenticated scanning is used, sufficient privileges are provided to enable thorough assessment of vulnerabilities local to the target system. Where applicable, accounts used for authenticated scanning that permit interactive login are managed in accordance with Requirement 8.2.2.

> **Notes on use:**
> - Verify that the tool is configured to use credentials for systems that support authenticated scanning. Check the tool's scan configuration or policy settings.
> - Verify that any scanning accounts permitting interactive login are managed per Req 8.2.2 (shared/generic accounts). These are common in legacy environments.
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

### Variant: Cloud / container-friendly

> **Context:** Use where the environment includes containerised workloads or cloud-managed services where traditional authenticated scanning is not applicable or is replaced by the cloud provider's native assessment method.

> **Agreed text:**
>
> The entity uses % Internal_Vulnerability_Scanning_Tool % for authenticated scanning of in-scope systems that accept credentials for scanning. For technologies that do not support authenticated scanning, including applicable containerised components, the entity has documented those systems and relies on the tool's native scanning method appropriate to the technology.

> **Notes on use:**
> - Verify that the documentation of systems not supporting authenticated scanning is current and complete
> - For container images, confirm that the tool scans images in the registry and/or at deployment, not only running containers
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

## Agreed Wording — Requirement 11.3.1.3

### Variant: Generic (full)

> **Context:** ROC Requirement 11.3.1.3 free-text narrative. This sub-requirement requires vulnerability scanning after significant changes to the environment.

> **Agreed text:**
>
> The entity performs internal vulnerability scans using % Internal_Vulnerability_Scanning_Tool % after significant changes to in-scope systems, network segments, container images, deployment patterns, or supporting infrastructure, as applicable. High-risk and critical vulnerabilities identified following significant changes are remediated and follow-up scans are conducted as needed to confirm resolution. These scans are performed by qualified personnel with appropriate organisational independence.

> **Notes on use:**
> - Verify that the entity's change management process includes a trigger to validate vulnerability scan coverage following significant changes. This is frequently a gap — confirm with the change management or DevOps team.
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

### Variant: Container / CI-CD pipeline

> **Context:** Use where the entity deploys containerised workloads via a CI/CD pipeline and vulnerability scanning is integrated into the build/deployment process rather than performed as a separate post-change scan.

> **Agreed text:**
>
> Following significant changes, including changes to base images, application containers, deployment pipelines, platform configuration, or supporting infrastructure, the entity performs internal vulnerability assessment using % Internal_Vulnerability_Scanning_Tool % and reviews resulting findings as part of the change validation process. High-risk and critical vulnerabilities are remediated and re-evaluated prior to or as part of production deployment, as applicable.

> **Notes on use:**
> - Confirm the tool is integrated into the pipeline (not just available as an ad-hoc scan)
> - Confirm there is a gate or review process for critical findings before deployment proceeds
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

## Agreed Wording — ROC Section 5.3 (Quarterly Internal Scan Results)

### Variant: ROC Table — Section 5.3 — Assessor Comments

> **Context:** ROC Section 5.3 "Quarterly Internal Scan Results" — the Assessor Comments column or free-text field that describes the scanning approach for the period. Use this where the entity uses continuous cloud-native scanning and there are no traditional quarterly scan reports.

> **Agreed text:**
>
> The entity uses % Internal_Vulnerability_Scanning_Tool % to perform continuous internal vulnerability assessment. For purposes of this table, each quarterly period is supported by combined dated scan exports, dashboard extracts, or other time-stamped evidence covering the applicable three-month cycle. The assessor reviewed evidence across the last 12 months to verify that scans occurred at a frequency exceeding the minimum quarterly requirement and that identified high-risk and critical vulnerabilities were remediated and validated through subsequent scan results.

> **Notes on use:**
> - **Placeholders:** `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

### Variant: ROC Table — Section 5.3 — "Date of the Scan(s)" column

> **Context:** ROC Section 5.3 "Quarterly Internal Scan Results" — the "Date of the Scan(s)" column for each quarterly row. Use where continuous scanning means there is no single scan date.

> **Agreed text:**
>
> % Quarter_Start_Date % to % Quarter_End_Date %, combined time-stamped outputs from % Internal_Vulnerability_Scanning_Tool %

> **Notes on use:**
> - This replaces a single date with a date range, which is appropriate for continuous scanning tools
> - **Placeholders:**
>   - `% Quarter_Start_Date %` — first day of the quarter, e.g. "01 January 2026"
>   - `% Quarter_End_Date %` — last day of the quarter, e.g. "31 March 2026"
>   - `% Internal_Vulnerability_Scanning_Tool %` — replace with the specific tool name

---

## What Not to Write

| Avoid | Reason |
|-------|--------|
| "Vulnerability scanning is performed continuously using [tool]. No scan report is available." | This accurately describes the situation but marks the requirement as deficient. The agreed wording above reframes the evidence positively while remaining accurate. |
| "The entity is exempt from quarterly scanning because they use continuous scanning." | There is no exemption — the quarterly minimum is met by exceeding it. Do not use the word "exempt". |
| "Scans are performed at least quarterly." | This understates the control where scanning is actually continuous. Use wording that reflects the frequency of the evidence. |
| Leaving the "Date of the Scan(s)" column blank or writing "N/A". | Always complete this column using the date range variant above. A blank cell invites challenge. |

---

## See Also

- [DSS-6.3.1-001](DSS-6.3.1-001.md) *(not yet created)* — Vulnerability risk-ranking methodology requirements and what constitutes a valid risk ranking under Req 6.3.1
- [DSS-11.3.2-001](DSS-11.3.2-001.md) *(not yet created)* — External vulnerability scanning (ASV scans) — separate article
