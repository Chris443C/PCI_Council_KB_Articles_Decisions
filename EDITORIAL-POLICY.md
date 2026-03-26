# Editorial Policy — Patronusec Internal KB

**Owner:** Head of QA
**Version:** 1.0
**Effective date:** [To be completed at HoQA sign-off]
**Review due:** Annually, or upon material change to the firm's QA processes

This policy governs the creation, review, approval, maintenance, and retirement of articles in the Patronusec Internal Knowledge Base. All QSAs must read and follow this policy.

---

## 1. Purpose

This KB exists to:

1. Capture agreed firm positions on interpreting PCI DSS, P2PE, PIN, 3DS, and SSF requirements
2. Provide consistent, approved ROC and SAQ wording templates for QSAs to use in assessments
3. Create a traceable, auditable record of how interpretive decisions were made and by whom

An article that is in `status: agreed` represents the **current firm position** and should be followed by all QSAs when delivering assessments. Deviating from an agreed position requires documented justification in the assessment record.

---

## 2. Article Types

There are two primary article types:

### 2.1 Interpretation Article

An agreed firm position on how to interpret a specific requirement or set of requirements.

- Contains a full STAR narrative (Situation, Task, Action, Result)
- Represents a **decision**, not a recommendation
- May be challenged by a QSA, but deviation requires written justification
- Becomes part of the firm's QA evidence base

### 2.2 Wording-Guidance Article

Agreed template text for use in ROC sections, SAQ responses, or assessment narratives.

- Contains the agreed wording template in a clearly demarcated block
- Always paired with a companion interpretation article (cross-referenced via `related_requirements`)
- QSAs may adapt the wording for entity-specific context but must not change its substance

### 2.3 Process Note

Internal QA process guidance that is not tied to a specific requirement.
Examples: "How we document compensating controls in a ROC", "How we handle scope disputes during pre-assessment scoping".

---

## 3. Roles and Responsibilities

| Role | Responsibility |
|------|---------------|
| **Any QSA** | May submit a draft article or raise an agenda item for the monthly meeting |
| **Meeting Chair** | Facilitates the monthly meeting and records the agreed position |
| **Head of QA** | Default approver for all articles; may delegate to programme leads |
| **Programme Lead** (if delegated) | May approve articles for their designated programme only |
| **SharePoint Owner** | Publishes approved articles to the internal SharePoint site |

**Named approvers as of [effective date]:**

| Programme | Approver |
|-----------|----------|
| DSS | [Name] |
| P2PE | [Name] |
| PIN | [Name] |
| 3DS | [Name] |
| SSF | [Name] |

*Update this table whenever delegated approvers change. Head of QA retains override authority at all times.*

---

## 4. Submission Process

### Step 1 — Raise an agenda item

Any QSA may raise an item for discussion at the monthly meeting by:
- Submitting a brief written description of the challenge to the meeting chair **at least 5 working days before the meeting**
- Including: the requirement reference, the specific ambiguity or challenge, and the proposed position (if any)

Items raised with less than 5 days' notice may be deferred to the following month.

### Step 2 — Monthly meeting discussion

The meeting chair facilitates discussion. The meeting must reach one of the following outcomes for each item:

| Outcome | Action |
|---------|--------|
| **Agreed position** | Proceed to article creation |
| **Deferred** | Item carried forward to next meeting with additional research assigned |
| **Referred to PCI SSC** | QSA to submit a formal FAQ request; article creation deferred until response received |
| **No consensus** | Majority position recorded; dissenting view noted in the article |

### Step 3 — Article creation

The QSA who raised the item (or a nominated delegate) creates the article:

1. Copy the appropriate template from `_templates/`
2. Complete **all required `(R)` fields** in the frontmatter
3. Write the STAR narrative (interpretation articles) or wording template (wording-guidance articles)
4. Set `status: draft`
5. Open a pull request (PR) against the `main` branch with a title matching the article ID and title
6. Request review from the named approver in the PR

### Step 4 — Review and approval

The named approver reviews the article against the following checklist:

- [ ] All `(R)` frontmatter fields are present and accurate
- [ ] `meeting_id` matches the meeting where the position was agreed
- [ ] STAR narrative accurately reflects the agreed position (not the proposer's preferred position)
- [ ] No standard text is reproduced verbatim without IP review (if `contains_standard_excerpts: true`, full HoQA review required)
- [ ] Disclaimer block is present in the article body
- [ ] `review_due` date is set to 12 months from `agreed_date`
- [ ] Cross-references to related articles are accurate
- [ ] If this supersedes an existing article, `supersedes` and `superseded_by` are populated on both articles

On approval, the reviewer:
1. Sets `status: agreed` and `approved_by: [their name]`
2. Approves and merges the PR
3. Notifies the SharePoint Owner to publish

---

## 5. Review and Expiry

### 5.1 Standard Review Cycle

All `agreed` articles must be reviewed **within 12 months** of their `agreed_date`. The `review_due` field tracks this.

On the first working day of each month, the Head of QA (or SharePoint Owner) should check the KB index for articles where `review_due` is within 30 days and assign them for review.

### 5.2 Triggered Reviews

The following events trigger an immediate review of affected articles, regardless of `review_due`:

| Trigger | Action |
|---------|--------|
| New version of a standard published | Set all articles for that `programme` and `standard_version` to `status: under-review` within 5 working days |
| PCI SSC FAQ published that contradicts an agreed position | Set affected article(s) to `status: under-review` immediately |
| QSA challenge upheld after review | Review article; update or supersede as appropriate |
| Firm QA finding relating to an assessment covered by an article | Review article for accuracy |

### 5.3 Under-Review Status

An article in `status: under-review` should be treated as `draft` by QSAs — it must not be relied upon in active assessments until returned to `agreed`. A banner is displayed on the SharePoint page indicating this status.

---

## 6. Supersession

When a position changes, the old article is **never deleted**. It must remain visible for historical audit purposes.

**Supersession process:**

1. Create a new article (with a new ID, e.g. `DSS-8.3.6-003`)
2. In the new article, populate `supersedes: DSS-8.3.6-002`
3. In the old article, populate `superseded_by: DSS-8.3.6-003` and change `status: superseded`
4. The old article should include a visible banner at the top:
   > ⚠️ **This article has been superseded.** See [DSS-8.3.6-003] for the current agreed position.

The superseded article must remain accessible via its original URL/ID indefinitely.

---

## 7. Disclaimer Requirements

Every article in `status: agreed` **must** include the following disclaimer block immediately below the article title:

```
> **Disclaimer:** This article represents the agreed internal interpretation of Patronusec
> assessors as of the agreed date above. It does not constitute an official PCI SSC
> position. QSAs should exercise professional judgement and consult the PCI SSC directly
> for formal clarification where required.

> **Standard version:** Applicable to [programme] v[standard_version] only.
> Review required before applying to any future standard version.
```

For wording-guidance articles, add:

```
> **Wording guidance:** The template text below is approved for internal use in Patronusec
> assessments only. It must not be shared with entities, clients, or third parties without
> the written approval of the Head of QA.
```

---

## 8. Intellectual Property

8.1 Do not reproduce PCI SSC standard text verbatim. Reference requirements by section number and paraphrase.

8.2 If a verbatim quote is essential for clarity, it must be brief (one or two sentences maximum), clearly attributed, and the article must be flagged with `contains_standard_excerpts: true`. This triggers an additional IP review by the Head of QA.

8.3 Programme materials for PIN and P2PE carry additional distribution restrictions. Assessors working on these programmes must confirm with the Head of QA before including any content derived from restricted materials.

8.4 This KB is internal only. No article may be shared with clients, entities, or third parties without explicit written approval from the Head of QA.

---

## 9. Change Log

| Version | Date | Author | Change |
|---------|------|--------|--------|
| 1.0 | [TBC] | Head of QA | Initial version |
