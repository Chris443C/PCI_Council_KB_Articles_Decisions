# KB Article Schema

This file defines the canonical frontmatter schema for all articles in this repository.
Every article **must** pass validation against this schema before its `status` can be set to `agreed`.

Fields marked **(R)** are required. Fields marked **(O)** are optional but strongly recommended.
Validation is enforced by the frontmatter linter (Phase 2). Until then, reviewers must check manually.

---

## Frontmatter Reference

```yaml
# ── Core Identity ──────────────────────────────────────────────────────────────

id: "DSS-6.4.3-001"
# (R) Unique article identifier. Format: {PROGRAMME}-{REQUIREMENT}-{SEQUENCE}
# PROGRAMME: DSS | P2PE | PIN | 3DS | SSF
# REQUIREMENT: dot-notation, e.g. 6.4.3 or 3.1 or A3.2.1
# SEQUENCE: zero-padded 3-digit integer, assigned in creation order per requirement
# Example: DSS-6.4.3-001, P2PE-3.1-002, PIN-10-001

title: "Inline scripts and CSP requirement under 6.4.3 for hosted payment pages"
# (R) Full descriptive title. Must be specific enough to distinguish from related articles.
# Bad: "CSP question"  Good: "Inline scripts and CSP requirement under 6.4.3 for hosted payment pages"

slug: "dss-6.4.3-inline-scripts-csp"
# (R) URL-safe identifier. Lowercase, hyphens only, no dots.
# Must be unique across the entire repository.

# ── Classification ─────────────────────────────────────────────────────────────

programme: "DSS"
# (R) Assessment programme this article belongs to.
# Allowed values: DSS | P2PE | PIN | 3DS | SSF

standard_version: "4.0.1"
# (R) The version of the standard this article applies to.
# Examples: "4.0.1" (PCI DSS), "3.1" (P2PE), "3.1" (PIN), "2.3.1" (3DS), "1.2" (SSF)
# IMPORTANT: An article is only valid for the version stated here.
# When a new standard version is published, all articles must be reviewed.

requirement: "6.4.3"
# (R) Primary requirement reference in dot-notation.
# For top-level requirements: "6", "8", "12"
# For sub-requirements: "6.4.3", "8.3.6"
# For test procedures: "6.4.3.a" (use sub_requirement for this level of specificity)

sub_requirement: ""
# (O) Specific test procedure, e.g. "6.4.3.a" — use when the article addresses a
# specific test procedure rather than the requirement as a whole.

related_requirements: ["6.4.2", "6.5.1"]
# (O) Other requirement references that interact with this one.
# Cross-programme references are allowed, e.g. "P2PE-3.1" to reference a P2PE requirement.
# Keep this list to genuinely relevant cross-references — not exhaustive.

article_type: "interpretation"
# (R) The type of article.
# Allowed values:
#   interpretation   — An agreed firm position on how to interpret a requirement.
#                      The primary article type. Contains a full STAR narrative.
#   wording-guidance — Agreed template text for ROC/SAQ responses or assessment narratives.
#                      Always paired with a companion interpretation article.
#                      Contains a wording_template block instead of a full STAR narrative.
#   process-note     — Internal QA process guidance not tied to a specific requirement.
#                      E.g. "how we handle compensating controls in a ROC".

# ── Lifecycle ──────────────────────────────────────────────────────────────────

status: "agreed"
# (R) Current lifecycle status of the article.
# Allowed values:
#   draft         — Not yet reviewed. Do not rely on draft articles in assessments.
#   under-review  — Flagged for review (e.g. new standard version published).
#                   Treat as draft until returned to agreed.
#   agreed        — Reviewed and approved. Safe to rely on in active assessments.
#   superseded    — Replaced by a newer article. Remains visible for audit purposes.
#                   superseded_by must be populated when this status is set.
#   retired       — No longer applicable (e.g. requirement removed from standard).
#                   Remains visible for historical audit. superseded_by is blank.
# IMPORTANT: Only the named approver may change status to "agreed".

created_date: "2026-02-12"
# (R) ISO 8601 date the article was first created (YYYY-MM-DD).

agreed_date: "2026-02-12"
# (O) ISO 8601 date the article was formally agreed at a meeting.
# Must be populated before status can be set to "agreed".

meeting_id: "2026-02-12-monthly"
# (R) Identifier of the meeting where the article was agreed.
# Format: YYYY-MM-DD-{type}, e.g. "2026-02-12-monthly", "2026-03-05-ad-hoc"
# This is the primary traceability link for QA audit purposes.

review_due: "2027-02-12"
# (R) ISO 8601 date by which the article must next be reviewed.
# Default: 12 months from agreed_date.
# Must be overridden to 30 days from today whenever a new version of the
# relevant standard is published.

superseded_by: ""
# (O) ID of the article that replaces this one. Populate when setting status to "superseded".
# Example: "DSS-8.3.6-002"

supersedes: ""
# (O) ID of the article this one replaces. Populate on the new article when it supersedes an older one.
# Example: "DSS-8.3.6-001"

# ── Attribution ────────────────────────────────────────────────────────────────

proposed_by: "J. Smith"
# (R) Full name (or initials) of the QSA who raised the item at the meeting.

approved_by: "Head of QA"
# (R) Full name or role of the person who approved the article.
# Default approver: Head of QA.
# Delegated approvers per programme may be agreed by the Head of QA.

second_reviewer: ""
# (O) Second named reviewer, used for contentious interpretations or those
# likely to be challenged during a QA review.

source_references:
  - "PCI SSC FAQ #1234 (2025-09)"
  - "PCI DSS v4.0.1 ROC Template v1.1"
# (O) List of normative sources consulted when agreeing this position.
# Include: PCI SSC FAQs (with number and date), information supplements,
# ROC template version, and any other authoritative references.
# Do NOT cite the standard text itself as a source — cite FAQs and supplements.

# ── Scope Applicability ────────────────────────────────────────────────────────

applies_to: ["ROC", "SAQ A", "SAQ A-EP", "SAQ D"]
# (O) Which assessment types this article applies to.
# Allowed values: ROC | SAQ A | SAQ A-EP | SAQ B | SAQ B-IP | SAQ C | SAQ C-VT |
#                 SAQ D | SAQ D-SP | SAQ P2PE | AOC | all
# Omit this field to mean "all assessment types".

applies_to_regions: ["global"]
# (O) Restrict applicability to specific regions or jurisdictions.
# Use "global" unless the interpretation is region-specific (e.g. a UK card scheme rule).
# Examples: ["global"], ["UK", "EU"], ["US"]

applies_to_merchant_levels: ["all"]
# (O) Restrict applicability to specific merchant/service provider levels.
# Examples: ["all"], ["L1", "L2"], ["L3", "L4"]

# ── Search and Discovery ───────────────────────────────────────────────────────

tags: ["javascript", "CSP", "inline-scripts", "e-commerce", "payment-page"]
# (O) Free-text keywords for search. Use lowercase, no spaces (use hyphens).
# Always include the requirement number as a tag (e.g. "6.4.3").
# Do NOT use tags as a substitute for controlled fields — programme and requirement
# are the primary search dimensions.

summary: "One-sentence plain-English summary for search result previews."
# (R) A single sentence (max 200 characters) describing the article's conclusion.
# This is the text shown in search results and index pages. Write it to be
# understandable by a QSA reading it out of context.

# ── Legal and Compliance ───────────────────────────────────────────────────────

disclaimer_accepted: true
# (R) Must be true before status can be set to "agreed".
# By setting this to true, the author confirms:
# - The article represents an internal Patronusec position, not an official PCI SSC position.
# - A disclaimer block is included in the article body.
# - The article does not reproduce PCI SSC copyright material verbatim beyond
#   what is necessary for reference purposes.

contains_standard_excerpts: false
# (R) Set to true if the article contains direct quotations from a PCI SSC
# published standard or programme document.
# When true, the article requires an additional IP review by the Head of QA
# before it can be published to SharePoint.
# When in doubt, paraphrase and cite the section number rather than quoting.
```

---

## Wording-Guidance Articles: Additional Fields

Articles with `article_type: wording-guidance` must also include one or more named **wording variant blocks** after the frontmatter.

### Why multiple variants?

A single requirement may need different approved wordings depending on the technology in use (e.g. on-premises vs. cloud-native), the SAQ type, or the level of detail required. Each variant is named and self-contained so a QSA can quickly identify which one applies.

### Variant block format

Each variant is a separate level-3 heading (`### Variant: {Name}`) containing:

```markdown
### Variant: {Name}
<!-- e.g. "Generic", "Shorter", "Cloud-native / continuous scanning", "Container / CI-CD" -->

> **Context:** [One sentence: where in the ROC/SAQ this wording is used, and when this variant applies.]

> **Agreed text:**
>
> [The agreed template wording, formatted exactly as it should appear in the ROC/SAQ.
>  Use % Placeholder_Name % for entity-specific values — see Placeholder Convention below.]

> **Notes on use:**
> - [Condition 1 on when this variant applies]
> - [List of placeholders that must be replaced before use]
```

### ROC table cell wording

Where a requirement has a corresponding ROC table (e.g. Section 5.3 Quarterly Scan Results), include a separate variant block for each column that requires agreed wording:

```markdown
### Variant: ROC Table — {Table Name} — {Column Name}

> **Context:** [Which ROC table and column this applies to.]

> **Agreed text:**
>
> [The agreed cell wording, including any date range patterns.]
```

---

## Placeholder Convention

Use `% Placeholder_Name %` (percent signs, space, Title_Case_With_Underscores, space, percent sign) to mark entity-specific values that must be substituted before the wording is used in a ROC or SAQ.

**Rules:**
- Placeholders must use Title_Case_With_Underscores — e.g. `% Internal_Vulnerability_Scanning_Tool %`, `% Entity_Name %`
- Every placeholder used in a wording block must be listed in the "Notes on use" section of that variant
- Do not use angle brackets `<like this>` or square brackets `[like this]` — those are reserved for editorial comments in templates
- Before a ROC is finalised, all `%` placeholders must be replaced with entity-specific values. A completed ROC must contain no `%` characters from this convention.

**Common standard placeholders:**

| Placeholder | Description |
|-------------|-------------|
| `% Internal_Vulnerability_Scanning_Tool %` | Name of the tool used for internal vuln scanning (e.g. "Microsoft Defender for Cloud") |
| `% External_Vulnerability_Scanning_Tool %` | Name of the ASV or external scan tool |
| `% Penetration_Testing_Entity %` | Name of the organisation that performed the pen test |
| `% Entity_Name %` | The assessed entity's trading name |
| `% Assessment_Period_Start %` | Start date of the assessment period (e.g. "01 January 2025") |
| `% Assessment_Period_End %` | End date of the assessment period |
| `% Policy_Name %` | Name of the entity's relevant policy document |

---

## Validation Rules

The following rules will be enforced by the frontmatter linter (Phase 2).
Until then, reviewers must check these manually before approving.

| Rule | Condition |
|------|-----------|
| R1 | All `(R)` fields must be present and non-empty |
| R2 | `programme` must be one of: `DSS`, `P2PE`, `PIN`, `3DS`, `SSF` |
| R3 | `article_type` must be one of: `interpretation`, `wording-guidance`, `process-note` |
| R4 | `status` must be one of: `draft`, `under-review`, `agreed`, `superseded`, `retired` |
| R5 | `created_date`, `agreed_date`, `review_due` must be valid ISO 8601 dates |
| R6 | `id` must match format `{PROGRAMME}-{REQUIREMENT}-{NNN}` |
| R7 | `slug` must be lowercase, hyphens only, unique across repo |
| R8 | `disclaimer_accepted` must be `true` before `status: agreed` is set |
| R9 | `superseded_by` must be populated when `status: superseded` |
| R10 | `meeting_id` must be populated when `status: agreed` |
| R11 | `summary` must be 200 characters or fewer |
| R12 | `review_due` must be a date in the future when `status: agreed` is set |

---

## Article ID Sequence Register

Maintain this table to avoid ID collisions. Update it whenever a new article is created.

| Programme | Requirement | Last Used ID | Next ID |
|-----------|-------------|--------------|---------|
| DSS | 6.4.3 | DSS-6.4.3-001 | DSS-6.4.3-002 |
| DSS | 8.3.6 | DSS-8.3.6-002 | DSS-8.3.6-003 |
| DSS | 11.3.1 | DSS-11.3.1-001 | DSS-11.3.1-002 |
| DSS | ROC-S6.2 | DSS-ROC-S6.2-001 | DSS-ROC-S6.2-002 |
| P2PE | 1-4 | P2PE-1-4-001 | P2PE-1-4-002 |

**Note on non-requirement IDs:** Some articles relate to ROC template sections rather than specific DSS requirements (e.g. `DSS-ROC-S6.2`). Use the format `{PROGRAMME}-ROC-{SECTION}-{NNN}` for these. P2PE requirements use hyphen-notation (e.g. `1-4`) rather than dot-notation — this is intentional and matches the P2PE standard's own numbering.

*Update this table as part of the article creation process.*
