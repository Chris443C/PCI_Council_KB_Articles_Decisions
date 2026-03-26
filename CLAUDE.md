# Project CLAUDE.md

Read and follow in this order:
1. `.claude/global.md`
2. this `CLAUDE.md`
3. `.claude/commands/*` when invoked

This file contains project-specific rules, repository context, local conventions, and any intentional overrides to the managed global Claude rules.

Do not duplicate generic coding, safety, workflow, or standards already defined in `.claude/global.md` unless this project intentionally overrides them.

---

## 1. Project Context

- **Project name:** PCI Council KB Articles & Decisions
- **Purpose:** Internal knowledge base for Patronusec monthly meetings covering PCI DSS, P2PE, PIN, 3DS, and SSF interpretation decisions. Captures agreed wording for QSA responses, ROC template guidance, and requirement-level decisions. Intended for publication to a SharePoint site.
- **Primary format:** Markdown (`.md`) articles and structured content
- **Target output:** SharePoint-compatible pages, indexed and searchable by assessment programme and requirement number
- **Assessment programmes covered:** PCI DSS, P2PE, PIN, 3DS, SSF
- **Key stakeholders:** QSAs at Patronusec
- **Architecture summary:** Content-only repository — no application code. Articles follow a STAR format (Situation, Task, Action, Result). May include tooling/scripts to generate or publish SharePoint content.

---

## 2. Repository-Specific Conventions

- **Article format:** Each KB article uses STAR structure — Situation, Task, Action, Result
- **Naming:** Article files should be named descriptively, e.g. `DSS-6.4.3-inline-scripts-compensating-control.md`
- **Tagging:** Each article should include frontmatter with:
  - `programme:` (e.g. DSS, P2PE, PIN, 3DS, SSF)
  - `requirement:` (e.g. 6.4.3)
  - `date:` (ISO format, e.g. 2026-03-25)
  - `status:` (draft / agreed / superseded)
- **Folder structure:** Organise by assessment programme (e.g. `/DSS/`, `/P2PE/`, `/PIN/`, `/3DS/`, `/SSF/`)
- **No speculative content:** Only document outcomes that have been agreed in a Patronusec internal meeting

---

## 3. Validation Overrides

This repository is content-only — there is no build pipeline. The managed `.NET` build/test/format steps do not apply here.

- Required validation: Review article markdown renders correctly and frontmatter is valid
- Required check before publishing: Confirm `status: agreed` and requirement reference is accurate
- No automated tests apply

---

## 4. Security and Compliance Rules

- Do not include client-specific data, entity names, or live assessment findings in KB articles
- Articles are internal guidance — do not assume they represent PCI SSC official positions unless explicitly attributed
- Do not reproduce copyrighted PCI SSC text verbatim beyond what fair use and internal reference permits
- Treat agreed wording as internally privileged; do not commit anything marked as commercially sensitive

---

## 5. Local Overrides to Global Rules

- **Override:** `.NET` coding standards (Sections 5.x of global.md) do not apply — this is a content repository
  - **Rationale:** No application code exists here
  - **Scope:** Entire repository unless tooling/scripts are added in future

---

## 6. Project Commands

```yaml
language: "Markdown / Content"
restore_command: "N/A"
build_command: "N/A"
test_command: "N/A"
format_check_command: "N/A"
notes: "Content-only repo. Validate markdown rendering and frontmatter accuracy manually."
```
