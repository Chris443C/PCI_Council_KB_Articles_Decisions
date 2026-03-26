# Patronusec Council — KB Articles & Decisions

Internal knowledge base for Patronusec's monthly council meetings. Captures agreed interpretations, standard ROC/SAQ wording, and governance records for PCI DSS, P2PE, PIN, 3DS, and SSF assessments.

---

## What this is

Each month, Patronusec QSAs bring interpretation challenges and wording questions to a council meeting. Agreed positions are recorded here as versioned, governed articles — providing a traceable, searchable reference for active assessments.

**Two article types:**

| Type | Purpose |
|------|---------|
| `interpretation` | Firm agreed position on how to interpret a requirement. Uses STAR narrative (Situation / Task / Action / Result). |
| `wording-guidance` | Approved template text for ROC or SAQ responses, with named variants and `% Placeholder %` tokens for entity-specific values. |

---

## Repository layout

```
/DSS/                          PCI DSS articles
/P2PE/                         P2PE articles
/PIN/                          PIN articles
/3DS/                          3DS articles
/SSF/                          SSF articles
/_governance/                  Meeting agenda items, minutes, escalation records
/_templates/                   Blank templates for new articles and meeting records
SCHEMA.md                      Canonical frontmatter schema and validation rules
EDITORIAL-POLICY.md            Submission, approval, review cycle, and IP rules
```

---

## Article status

| Status | Meaning |
|--------|---------|
| `draft` | Not yet reviewed — do not rely on in assessments |
| `under-review` | Flagged for re-review (e.g. new standard version published) |
| `agreed` | Reviewed and approved — safe to use in active assessments |
| `superseded` | Replaced by a newer article — visible for audit purposes only |
| `retired` | Requirement removed from standard — historical reference only |

Only the Head of QA (or a named delegate) may set `status: agreed`.

---

## Articles

### PCI DSS

| ID | Title | Status |
|----|-------|--------|
| [DSS-8.3.6-001](DSS/DSS-8.3.6-001.md) | Password length: legacy system 8-char fallback and compensating measures | `agreed` |
| [DSS-8.3.6-002](DSS/DSS-8.3.6-002.md) | Wording guidance: ROC narrative for legacy system password length | `agreed` |
| [DSS-6.4.3-001](DSS/DSS-6.4.3-001.md) | Inline scripts and CSP requirement under 6.4.3 for hosted payment pages | `agreed` |
| [DSS-11.3.1-001](DSS/DSS-11.3.1-001.md) | Wording guidance: internal vulnerability scanning across cloud platforms | `agreed` |
| [DSS-ROC-S6.2-001](DSS/DSS-ROC-S6.2-001.md) | Wording guidance: ROC Section 6.2 sampling narrative | `draft` |

### P2PE

| ID | Title | Status |
|----|-------|--------|
| [P2PE-1-4-001](P2PE/P2PE-1-4-001.md) | Section 4 N/A table: applicability to sub-requirements in the P-ROV report | `draft` |

---

## Creating a new article

1. Copy the appropriate template from `/_templates/`
2. Assign the next ID from the sequence register in `SCHEMA.md` and update the register
3. Fill in all `(R)` required frontmatter fields — leave `agreed_date`, `meeting_id`, `approved_by` blank until the council meeting
4. Set `status: draft`
5. Submit for the next monthly meeting using the agenda item template

See [EDITORIAL-POLICY.md](EDITORIAL-POLICY.md) for the full submission and approval process.

---

## After a council meeting

Once an article is agreed:

1. Set `agreed_date`, `meeting_id`, `review_due` (default: 12 months from today)
2. Set `approved_by` to the approver's name
3. Set `disclaimer_accepted: true`
4. Change `status` from `draft` to `agreed`
5. Commit with the meeting ID in the commit message

---

## Governance

- **Submission:** Any QSA may submit a draft (5-day lead time before the meeting)
- **Approval:** Head of QA, or a named delegate per programme
- **Review cycle:** 12 months from `agreed_date`, or immediately on a new standard version
- **Supersession:** Old articles are never deleted — they remain visible with a superseded banner
- **IP:** Articles must not reproduce PCI SSC text verbatim. All articles carry an internal disclaimer.

Full policy: [EDITORIAL-POLICY.md](EDITORIAL-POLICY.md) · Schema reference: [SCHEMA.md](SCHEMA.md)

---

> **Internal use only.** Articles represent agreed Patronusec positions, not official PCI SSC positions. Do not share with clients or third parties without written approval from the Head of QA.
