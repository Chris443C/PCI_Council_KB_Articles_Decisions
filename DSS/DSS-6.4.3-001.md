---
id: "DSS-6.4.3-001"
title: "Content Security Policy (CSP) requirement under 6.4.3: applicability where inline scripts are present on a hosted payment page"
slug: "dss-6.4.3-csp-inline-scripts-hosted-payment-page"
programme: "DSS"
standard_version: "4.0.1"
requirement: "6.4.3"
sub_requirement: ""
related_requirements: ["6.4.2", "6.5.1", "11.6.1"]
article_type: "interpretation"
status: "agreed"
created_date: "2026-03-12"
agreed_date: "2026-03-12"
meeting_id: "2026-03-12-monthly"
review_due: "2027-03-12"
superseded_by: ""
supersedes: ""
proposed_by: "S. Ahmed"
approved_by: "Head of QA"
second_reviewer: "C. Ince"
source_references:
  - "PCI DSS v4.0.1 Requirement 6.4.3 — Guidance column"
  - "PCI DSS v4.0.1 Requirement 6.4.3.a / 6.4.3.b / 6.4.3.c test procedures"
  - "PCI SSC Information Supplement: Skimming Prevention — Best Practices for Merchants (2020)"
  - "PCI SSC FAQ #1501 — CSP and script integrity for payment pages (2024-02)"
  - "W3C Content Security Policy Level 3 specification"
applies_to: ["ROC", "SAQ A-EP", "SAQ D"]
applies_to_regions: ["global"]
applies_to_merchant_levels: ["L1", "L2", "L3", "L4"]
tags: ["CSP", "content-security-policy", "inline-scripts", "javascript", "payment-page", "e-commerce", "6.4.3", "script-integrity", "skimming"]
summary: "Inline scripts on a payment page do not prevent CSP compliance under 6.4.3, but each inline script must be individually justified, authorised, and integrity-verified; 'unsafe-inline' in the CSP is not acceptable."
disclaimer_accepted: true
contains_standard_excerpts: false
---

# DSS-6.4.3-001 — Content Security Policy (CSP) requirement under 6.4.3: applicability where inline scripts are present on a hosted payment page

> **Disclaimer:** This article represents the agreed internal interpretation of Patronusec
> assessors as of the agreed date above. It does not constitute an official PCI SSC
> position. QSAs should exercise professional judgement and consult the PCI SSC directly
> for formal clarification where required.

> **Standard version:** Applicable to PCI DSS v4.0.1 only.
> Review required before applying to any future standard version.

---

## Situation

Requirement 6.4.3 requires that all scripts loaded and executed in a consumer's browser for payment pages originating from the entity's environment must be managed as follows:

- A method is in place to confirm each script is authorised
- A method is in place to assure the integrity of each script
- An inventory of all scripts is maintained with written business justification

The requirement applies to all payment pages that are served from the entity's own environment. It does not apply to pages fully hosted by a third party (e.g. a P2PE validated solution or a fully-redirected payment page where the entity serves no page content).

During assessments of merchants with hosted payment pages, QSAs encountered a recurring challenge: many legitimate payment pages include inline JavaScript, typically for:

- Tracking/analytics (e.g. Google Tag Manager initialisation)
- UX enhancements (e.g. real-time card number formatting)
- Payment form event handling (e.g. preventing form submission before validation)
- Third-party payment widget integration code

The challenge arose because a strict Content Security Policy (CSP) — the most common technical mechanism for satisfying 6.4.3 — cannot hash or nonce inline scripts that are dynamically generated or change between deployments. QSAs were receiving conflicting interpretations about whether the presence of inline scripts on a payment page meant:

(a) The entity could not satisfy 6.4.3 at all until inline scripts were removed, or
(b) Inline scripts are permissible if individually controlled, documented, and integrity-verified, or
(c) The entity could use `'unsafe-inline'` in their CSP as an interim measure

---

## Task

Agree a firm position on the following:

1. Can an entity satisfy Requirement 6.4.3 if their hosted payment page contains inline JavaScript?
2. If yes, what controls must be in place for each inline script?
3. Is the use of `'unsafe-inline'` in a CSP an acceptable method of satisfying 6.4.3?
4. What does "integrity verification" mean for an inline script that cannot be covered by a `<script src>` SRI hash?
5. What must the QSA assess and document?

---

## Action

The team reviewed the requirement text and guidance column for 6.4.3, PCI SSC FAQ #1501, and the W3C CSP Level 3 specification.

**On inline scripts and CSP compliance:**

The requirement does not mandate the use of a CSP header as the mechanism — it mandates the controls (authorisation, integrity, inventory). A CSP is the most practical implementation for external scripts, but for inline scripts, the controls must be achieved by other means.

The team agreed the following:

Inline scripts are not prohibited by 6.4.3. The requirement is technology-neutral — it requires the *controls*, not a specific technical mechanism. An entity may have inline scripts on a payment page provided each inline script is:

1. **Inventoried** — included in the script inventory with a unique identifier (e.g. function name, file reference, or hash)
2. **Authorised** — has a documented business justification signed off by a responsible person (e.g. the e-commerce owner or CISO)
3. **Integrity-verified** — the entity has a method to detect unauthorised changes. The team identified three acceptable methods for inline scripts:
   - **CSP nonce:** A cryptographically random nonce is generated server-side per response and included both in the CSP header (`script-src 'nonce-{value}'`) and as an attribute on each inline `<script>` tag. This is the preferred method as it provides strong per-request integrity.
   - **CSP hash:** The SHA-256 (or SHA-384/SHA-512) hash of the inline script content is included in the CSP header (`script-src 'sha256-{hash}'`). This works for static inline scripts that do not change between deployments. The hash must be recalculated and the CSP header updated whenever the script changes.
   - **Change detection monitoring (Req 11.6.1 alignment):** Where CSP nonces or hashes are not technically feasible, the entity must demonstrate real-time monitoring of the payment page HTML/JS (as required by 11.6.1) that would detect any unauthorised modification of inline scripts. This is the weakest of the three options and requires assessor judgement on whether the monitoring is genuinely real-time and comprehensive.

**On `'unsafe-inline'`:**

The team agreed that the use of `'unsafe-inline'` in a CSP `script-src` directive does **not** satisfy Requirement 6.4.3. `'unsafe-inline'` disables the integrity-enforcement function of the CSP for all inline scripts. An entity using `'unsafe-inline'` has no mechanism to prevent a maliciously injected inline script from executing — which is precisely the attack vector 6.4.3 is designed to prevent. This applies regardless of other controls.

Assessors must not mark 6.4.3 as "In Place" for entities whose CSP includes `'unsafe-inline'` without a formal Appendix B compensating control addressing the absence of inline script integrity controls.

**On the use of Google Tag Manager (GTM) and similar tag containers:**

GTM and similar containers are frequently used on payment pages. The team agreed the following sub-position:

- The GTM container script itself (`gtm.js`) is a third-party external script and must be inventoried, authorised, and integrity-controlled like any other external script (SRI hash or equivalent).
- Scripts injected by GTM into the page (tags) are a separate concern. The entity must demonstrate that the GTM container is locked (publication requires approval), that the approved tag list is documented, and that no GTM tag can inject scripts not in the inventory. If these controls are in place, GTM-managed tags may be treated as controlled inline scripts for the purposes of 6.4.3.
- GTM preview mode must be disabled on production payment pages.

---

## Result

**Agreed position:**

Inline scripts are not prohibited by Requirement 6.4.3. An entity with inline JavaScript on a hosted payment page may satisfy 6.4.3 provided each inline script is inventoried with a documented business justification, and one of the three integrity verification methods is implemented: CSP nonce (preferred), CSP hash, or real-time change detection under Req 11.6.1 (weakest — requires strong assessor justification).

The use of `'unsafe-inline'` in a CSP `script-src` directive does not satisfy Requirement 6.4.3 under any circumstances. An entity relying on `'unsafe-inline'` is not in compliance with 6.4.3 and requires either remediation or a formal Appendix B compensating control.

**Conditions:**

- This position applies to payment pages hosted on entity infrastructure (including entity-controlled cloud environments). It does not apply to fully third-party-hosted redirect/iframe payment pages.
- The CSP nonce method requires server-side nonce generation per response. Client-side or static nonces do not satisfy the integrity requirement.
- The GTM sub-position applies only where the GTM container is locked and governed. An unlocked container with open publishing access does not satisfy the inventory/authorisation controls.

**Assessment impact:**

For each in-scope payment page, the QSA must:

1. Obtain the complete script inventory and verify it includes all inline scripts (not just external scripts)
2. Verify each inline script has a documented business justification
3. Verify the integrity method in use: review the CSP header for nonces or hashes; confirm nonces are server-generated and per-request; confirm hashes match the current script content
4. If `'unsafe-inline'` is present in `script-src`: mark 6.4.3 as "Not In Place" or raise a finding; do not mark as In Place without Appendix B
5. If GTM is in use: verify the container is locked, review the approved tag list, and confirm no un-inventoried scripts are injected
6. Document all of the above in the ROC with evidence references to the CSP header capture, script inventory, and business justification records

---

## See Also

- [DSS-6.4.2-001](DSS-6.4.2-001.md) *(not yet created)* — Scope of 6.4.2/6.4.3 — which pages constitute "payment pages" requiring controls
- [DSS-11.6.1-001](DSS-11.6.1-001.md) *(not yet created)* — Real-time change detection under 11.6.1 and its relationship to 6.4.3 integrity controls
