# Patronusec Council Meeting — Agenda Item Submission

> Reformatted from original submission document `section6.2-sampling.docx`.
> Original submitted informally; this record captures it in the standard format for the agenda.

---

## Submission Details

| Field | Value |
|-------|-------|
| **Submitted by** | [Name — to confirm from original email chain] |
| **Date submitted** | [To confirm] |
| **Target meeting** | 2026-03-12 Monthly |
| **Assessment programme** | DSS |
| **Requirement(s)** | ROC Template Section 6.2 — Sampling of System Components |
| **Item type** | Wording guidance request |
| **Priority** | Normal |

---

## 1. Background

The standard ROC sampling narrative in Section 6.2 currently reads:

> "Sampling of System Components — The assessor selected the number of samples as an accurate reflection of the various configurations of components i.e. all load balancers have the same configuration, therefore the assessor selected only a single component as a sample as it reflects the same configuration on the other components. Components with unique software and/or configurations were included in the sample sets."

This wording includes a specific example (load balancers) which, while illustrative, causes recurring problems in practice:

1. The load balancer example does not apply to many environments and attracts reviewer comments when used in contexts where load balancers are irrelevant
2. The phrase "i.e." (meaning "that is") makes the example feel like a definition rather than an illustration
3. The wording is less reusable across different assessment environments than it could be

The issue has been observed repeatedly across different assessors' ROC deliverables.

---

## 2. The Specific Question or Challenge

1. Should the current Section 6.2 sampling narrative be revised to remove the load balancer example and replace it with more neutral, environment-agnostic language?
2. If so, what is the agreed replacement wording?

---

## 3. Proposed Position

Remove the specific load balancer example and replace with wording based on common characteristics (make, model, function, configuration) that applies across any environment type.

**Proposed replacement wording (from original submission):**

> "Sampling of system components was determined by the assessor to accurately reflect the range of in-scope devices and component types present in the environment. Sample selection was based on common characteristics such as make, model, function, and configuration. Where multiple components shared the same relevant characteristics, a representative sample was selected. Components with unique software, function, or configuration were included separately within the sample sets."

**Sources consulted:** Current ROC template Section 6.2 text; practical assessment experience.

---

## 4. Impact if Not Resolved

QSAs continue using the existing wording with the load balancer example, which attracts unnecessary reviewer comments and requires manual editing on each assessment. Low-risk but creates avoidable friction and inconsistency.

No immediate deadline.

---

## 5. Desired Output

- [x] Agreed ROC/SAQ wording — a replacement template for Section 6.2 sampling narrative

---

## 6. Supporting Materials

- `section6.2-sampling.docx` — original submission with current and proposed wording
