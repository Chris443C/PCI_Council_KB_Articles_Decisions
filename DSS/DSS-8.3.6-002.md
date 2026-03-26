---
id: "DSS-8.3.6-002"
title: "Wording guidance: ROC response for legacy system password length with documented compensating measures"
slug: "dss-8.3.6-legacy-system-roc-wording"
programme: "DSS"
standard_version: "4.0.1"
requirement: "8.3.6"
sub_requirement: ""
related_requirements: ["8.3.6"]
article_type: "wording-guidance"
status: "agreed"
created_date: "2026-02-12"
agreed_date: "2026-02-12"
meeting_id: "2026-02-12-monthly"
review_due: "2027-02-12"
superseded_by: ""
supersedes: ""
proposed_by: "C. Ince"
approved_by: "Head of QA"
second_reviewer: ""
source_references:
  - "PCI DSS v4.0.1 ROC Template v1.1 — Section 8"
  - "PCI SSC FAQ #1455 (2023-11)"
applies_to: ["ROC"]
applies_to_regions: ["global"]
applies_to_merchant_levels: ["all"]
tags: ["password", "legacy", "8.3.6", "roc-wording", "compensating-measures"]
summary: "Approved ROC wording for Requirement 8.3.6 where a legacy system cannot support 12-character or complex passwords but compensating measures are in place."
disclaimer_accepted: true
contains_standard_excerpts: false
---

# DSS-8.3.6-002 — Wording guidance: ROC response for legacy system password length with documented compensating measures

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

## Agreed Wording

> **Context:** ROC Requirement 8.3.6, Testing Procedures narrative section (the "Assessor's Findings" or equivalent free-text narrative in the ROC template). Used where one or more in-scope systems cannot technically support a 12-character minimum password or complexity requirements, and the compensating measures documented in DSS-8.3.6-001 are in place.

---

> **Agreed text:**
>
> [System name / system type, e.g. "The [VENDOR] [MODEL] EPOS terminals located in [LOCATION]"] cannot technically support a minimum password length of 12 characters or character complexity requirements due to a vendor-imposed firmware limitation. This limitation was confirmed via [vendor documentation reference, e.g. "vendor advisory VA-2024-083 dated [date]"]. No vendor update path to address this limitation is currently available.
>
> In accordance with Requirement 8.3.6, the 8-character minimum is applied as the applicable technical fallback for the length element.
>
> To address the associated risk arising from the absence of complexity support, the entity has implemented the following compensating measures:
>
> - **Account lockout:** Accounts are locked after [N, must be ≤10] failed authentication attempts. This was verified via [evidence reference, e.g. "system configuration screenshot SC-8.3.6-01"].
> - **Authentication monitoring:** Failed authentication attempts on these systems are captured in [log source] and are subject to daily review / automated alerting in accordance with Requirement 10.2.1.2. Verified via [evidence reference].
> - **Network restriction:** These systems are isolated to a dedicated management VLAN ([VLAN ID/name]) with no direct internet path. Access is restricted to [authorised management hosts/IP ranges]. Verified via [firewall rule evidence reference / network diagram reference].
>
> The assessor has reviewed the above compensating measures and determined that, in combination, they achieve the intent of Requirement 8.3.6 by materially reducing the risk associated with the reduced password strength. This determination is consistent with the firm's agreed internal position (ref: DSS-8.3.6-001).
>
> Requirement 8.3.6 is assessed as **In Place** for these systems, with the above compensating measures noted.

---

> **Notes on use:**
> - This wording may only be used where ALL THREE compensating measures (lockout, monitoring, network restriction) are verified and evidenced. See DSS-8.3.6-001 for the full assessment position.
> - The wording is for the ROC narrative section. The ROC tracker status should be "In Place" — the compensating measures are documented in the narrative, not via Appendix B, unless one of the three controls is absent.
> - Fields in [square brackets] must be completed with entity-specific values before use. Do not leave placeholder text in a final ROC.
> - If the entity also has a formal Appendix B compensating control for this requirement (e.g. because one of the three controls is absent), use the Appendix B template wording instead and reference the CC number in the narrative.
> - Do not use this wording for privileged accounts or service accounts — those must meet the full requirement.

---

## Background

**Companion article:** [DSS-8.3.6-001](DSS-8.3.6-001.md) — Minimum password length: 8-character fallback for legacy systems and the requirement for additional compensating measures

The companion interpretation article (DSS-8.3.6-001) contains the full analysis of when the 8-character fallback applies and what compensating measures are required. The wording above was agreed at the same meeting and represents the approved narrative for capturing this finding in a ROC.

---

## What Not to Write

| Avoid | Reason |
|-------|--------|
| "The system does not meet Requirement 8.3.6 but a compensating control is in place." | This implies Appendix B was invoked. Only use this phrasing if Appendix B was formally completed. |
| "The entity is exempt from 8.3.6 for legacy systems." | There is no exemption — the 8-character fallback is an accommodation, not an exemption. |
| "Passwords are managed in accordance with policy." | Too vague — does not demonstrate assessment of the specific technical limitation. |
| Omitting the three compensating measures from the narrative. | The narrative must stand alone as evidence. A reviewer reading the ROC must be able to understand why "In Place" was marked without referring to other documents. |

---

## See Also

- [DSS-8.3.6-001](DSS-8.3.6-001.md) — Interpretation: legacy system password length and compensating measures threshold
