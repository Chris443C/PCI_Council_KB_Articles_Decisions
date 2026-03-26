# Patronusec Council Meeting — Agenda Item Submission

> Reformatted from original submission document `Section4-P2PE-PROVS.docx`.
> Original submitted informally; this record captures it in the standard format for the agenda.

---

## Submission Details

| Field | Value |
|-------|-------|
| **Submitted by** | [Name — to confirm from original email chain] |
| **Date submitted** | [To confirm] |
| **Target meeting** | 2026-03-12 Monthly |
| **Assessment programme** | P2PE |
| **Requirement(s)** | KMS/EMS/DMS P-ROV Report Template — Section 4; Requirement 1-4, Requirement 6-4 |
| **Item type** | Interpretation question |
| **Priority** | Normal |

---

## 1. Background

During P2PE assessments using the PCI P2PE KMS, EMS, DMS P-ROV report template, Section 4 (Findings and Observations) includes the instruction:

> "Every requirement denoted as 'N/A' in the reporting section below must be documented in this table and vice versa."

In practice, P-ROV reports frequently contain requirements where the overall (parent) requirement is marked as In Place, but one or more sub-requirements are marked as Not Applicable. This creates ambiguity: does the Section 4 instruction apply only to the N/A marking on the overall requirement, or also to individual sub-requirements marked N/A?

This question has come up on multiple P2PE assessments. Without an agreed firm position, different assessors are populating Section 4 differently, creating inconsistency across our P-ROV deliverables.

---

## 2. The Specific Question or Challenge

1. Does the Section 4 N/A table instruction apply only to overall (parent) requirements marked N/A, or also to individual sub-requirements marked N/A?

2. Where a sub-requirement contains mixed findings — part In Place and part Not Applicable (e.g. Requirement 6-4.b) — how should this be handled in Section 4?

**Concrete examples raised:**

**Example A — Requirement 1-4:**
- 1-4 (overall): In Place
- 1-4.a: In Place
- 1-4.b: Not Applicable (organisation uses a PCI PTS-approved device rather than a FIPS-approved HSM)
- Should 1-4.b be listed in Section 4 despite the parent being In Place?

**Example B — Requirement 6-4.b:**
- 6-4.b contains one element that is In Place and one that is Not Applicable
- Should this appear in Section 4? If so, as a full N/A entry or a partial entry?

---

## 3. Proposed Position

**Proposed by submitter:**

The instruction applies to **any** requirement or sub-requirement marked N/A — not only to top-level requirements.

Therefore:
- If a sub-requirement is marked N/A, it must be listed in Section 4, even if the parent requirement is In Place.
- For mixed sub-requirements (part In Place, part N/A), the N/A portion must be explicitly addressed in Section 4 with a description of which specific clause is N/A and why.

**Example A conclusion:** Requirement 1-4.b must appear in Section 4 because it is marked N/A, regardless of the parent being In Place.

**Example B conclusion:** Requirement 6-4.b should appear in Section 4 with a specific description of which part is N/A, e.g.: "Requirement 6-4.b (partial): [specific clause] is Not Applicable because [reason]."

**Sources consulted:** PCI P2PE KMS/EMS/DMS P-ROV Report Template Section 4 instruction text.

---

## 4. Impact if Not Resolved

Assessors are currently inconsistent in populating Section 4. Some include sub-requirement N/A entries; some do not. This creates reviewable inconsistency across P-ROV deliverables and could attract a finding during a PCI SSC quality review.

No immediate deadline, but there are active P2PE assessments where this question is live.

---

## 5. Desired Output

- [x] An agreed interpretation — a firm Patronusec position on how to read the Section 4 instruction
- [x] A process note — internal guidance on how to handle mixed N/A sub-requirements

---

## 6. Supporting Materials

- `Section4-P2PE-PROVS.docx` — original submission with annotated examples and Requirement 1-4 / 6-4 diagrams
