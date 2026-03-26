---
id: "DSS-8.3.6-001"
title: "Minimum password length: 8-character fallback for legacy systems and the requirement for additional compensating measures"
slug: "dss-8.3.6-legacy-system-password-length"
programme: "DSS"
standard_version: "4.0.1"
requirement: "8.3.6"
sub_requirement: ""
related_requirements: ["8.3.1", "8.2.3", "8.3.9", "12.3.3"]
article_type: "interpretation"
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
  - "PCI DSS v4.0.1 Requirement 8.3.6 — Guidance column"
  - "PCI SSC FAQ #1455 — Password length for legacy systems (2023-11)"
  - "PCI DSS v4.0.1 Appendix B — Compensating Controls"
applies_to: ["ROC", "SAQ B-IP", "SAQ C", "SAQ D"]
applies_to_regions: ["global"]
applies_to_merchant_levels: ["all"]
tags: ["password", "authentication", "legacy", "compensating-control", "8.3.6", "epos", "embedded-system"]
summary: "Where a system cannot support 12-character passwords, the 8-character fallback covers length only; absent complexity support requires documented compensating measures meeting a defined threshold."
disclaimer_accepted: true
contains_standard_excerpts: false
---

# DSS-8.3.6-001 — Minimum password length: 8-character fallback for legacy systems and the requirement for additional compensating measures

> **Disclaimer:** This article represents the agreed internal interpretation of Patronusec
> assessors as of the agreed date above. It does not constitute an official PCI SSC
> position. QSAs should exercise professional judgement and consult the PCI SSC directly
> for formal clarification where required.

> **Standard version:** Applicable to PCI DSS v4.0.1 only.
> Review required before applying to any future standard version.

---

## Situation

Requirement 8.3.6 mandates that, where passwords are used as authentication factors, they must have a minimum length of at least 12 characters — or at least 8 characters if the system does not technically support 12.

During several active assessments, QSAs encountered in-scope systems where the vendor-supplied authentication mechanism had a hard technical limit of 8 characters and no firmware update path was available from the vendor. The systems involved were typically legacy EPOS terminals and embedded industrial control systems that interfaced with the CDE.

The question became more complex when these same systems also lacked support for character complexity requirements — they could not enforce mixed case, numeric, or special characters. The question arose as to whether:

1. The 8-character fallback provision in 8.3.6 was sufficient on its own, or
2. The absence of complexity support created an additional gap requiring a compensating control under Appendix B

---

## Task

Determine the correct assessment position for the following scenario:

1. A system in scope cannot technically support the 12-character minimum — the 8-character fallback provision in 8.3.6 applies.
2. The same system also cannot enforce complexity requirements (mixed case, numeric, special characters).
3. No vendor firmware update path is available.

Specifically, determine:

- Whether the 8-character fallback alone satisfies 8.3.6, or whether the complexity gap requires additional action
- If additional action is required, what constitutes sufficient compensating measures before a formal Appendix B compensating control is needed
- What the QSA must document in the ROC to record this correctly

---

## Action

The team reviewed the requirement text, the guidance column for 8.3.6, and PCI SSC FAQ #1455.

**On the 8-character fallback:**
The fallback is a technical accommodation built into the requirement itself. It is not a compensating control and does not require Appendix B documentation. It applies only to the length element of 8.3.6. An assessor who encounters an 8-character-limited system may note the fallback applies and mark the length sub-element accordingly — no further action is required for length alone.

**On the missing complexity support:**
The guidance column for 8.3.6 states that "additional controls should be in place to manage the associated risk" where the full requirement cannot be met. The team reviewed whether this guidance language triggers a mandatory Appendix B compensating control.

The team's view, informed by FAQ #1455, is that the guidance column does not automatically require Appendix B — but it does require the QSA to document:

1. The technical constraint and its basis (vendor documentation confirming the limitation)
2. What additional controls the entity has in place to offset the increased risk
3. The QSA's professional judgement that the combination of controls achieves the intent of the requirement

**Agreed threshold for "sufficient compensating measures" (without Appendix B):**

The team agreed the following three controls must all be present before a QSA may rely on the guidance column documentation path rather than requiring a formal Appendix B compensating control:

| Control | Rationale |
|---------|-----------|
| Account lockout is enabled (after no more than 10 failed attempts) | Mitigates brute-force risk created by short, simple passwords |
| Failed authentication attempts are monitored and alerted (Req 10.2.1.2 satisfies this) | Provides detective control over attempted exploitation |
| The system's network exposure is restricted — minimum: dedicated management VLAN, no direct internet path | Reduces the attack surface to make exploitation significantly harder |

If **any one** of these three controls is absent, a formal Appendix B compensating control is required.

The team also agreed that QSAs must not mark 8.3.6 as "In Place" in the ROC without the compensating measures documentation being present in the evidence package, regardless of which path is taken.

**On dissenting views:**
No dissenting view was recorded at the meeting.

---

## Result

**Agreed position:** The 8-character fallback in Requirement 8.3.6 covers the length element only. A system that cannot support complexity requirements does not automatically require a formal Appendix B compensating control, but does require explicit documentation of compensating measures in the ROC narrative and evidence package.

**Conditions:**
- This position applies where the technical limitation is confirmed by vendor documentation. A system administrator choosing not to configure complexity requirements does not qualify — the limitation must be a hard technical constraint of the system.
- The three-control threshold (lockout + monitoring + network restriction) must all be met. If any one is absent, Appendix B is required.
- This position does not apply to privileged accounts or service accounts. Those must meet the full requirements of 8.3.1 and 8.3.9 by other means.

**Assessment impact:**
- Obtain vendor documentation confirming the technical limitation (firmware version, vendor advisory, or vendor support statement)
- Verify lockout configuration in system settings
- Verify monitoring coverage via Req 10.2.1.2 evidence (log review or SIEM alerting)
- Verify network segmentation via firewall rules or network architecture review
- Document all three in the ROC narrative with evidence references
- Mark 8.3.6 as "In Place with Compensating Measures Noted" rather than "In Place" in the ROC tracker
- Companion ROC wording is available in DSS-8.3.6-002

---

## See Also

- [DSS-8.3.6-002](DSS-8.3.6-002.md) — Wording guidance: ROC response for legacy system password length with documented compensating measures
- [DSS-8.3.1-001](DSS-8.3.1-001.md) *(not yet created)* — General password policy requirements and scope of application
- [DSS-8.2.3-001](DSS-8.2.3-001.md) *(not yet created)* — Service account and shared credential handling
