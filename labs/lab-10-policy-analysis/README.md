# Lab 10: Privacy & Compliance Policy Analysis

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 100 min  ·  **Autograding:** section/word-count/table checks

## Objective
Analyze the privacy and compliance posture of the class AI stack (local LLM +
WebUI + agent) against **GDPR** and **FERPA**. You produce a structured
`analysis.md` with required sections and a completed data-inventory table.

**Why it matters:** identifying and analyzing privacy and policy issues is a core
professional duty (CO4).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO4 - Privacy and policy issues | Analyze the stack against GDPR/FERPA, build a data inventory |
| CO6 - Security+ readiness | Domain 5.0 Governance, Risk & Compliance |

**Security+ SY0-701 domain:** 5.0 Security Program Management & Oversight (privacy, compliance).

## Prerequisites
- Labs 7-9 (you are analyzing that stack).

## Tasks
1. Copy `starter/analysis-template.md` to `analysis.md`.
2. Complete every required section: **Data Inventory**, **GDPR Analysis**, **FERPA Analysis**, **Risks**, **Recommendations**.
3. Fill the **data-inventory table** with at least **4 rows**, columns: Component, Data Category, Storage Location, Lawful Basis (all filled).
4. Cite at least **two specific regulation articles/sections** (e.g., "GDPR Article 6", "Article 30", "34 CFR § 99").
5. Provide at least **3 risk-and-mitigation pairs**.
6. Write substantive analysis (>= 600 words total). Remove all placeholders.

## Deliverables
- `analysis.md` with all sections, a completed inventory table, citations, risk/mitigation pairs, and no placeholders.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh` (and `--syscheck` first).

## Grading (100% machine-checked; no manual grading)
| Criterion | Points |
|-----------|-------:|
| `analysis.md` present | 8 |
| Section: Data Inventory | 6 |
| Section: GDPR Analysis | 6 |
| Section: FERPA Analysis | 6 |
| Section: Risks | 6 |
| Section: Recommendations | 6 |
| Data-inventory table complete (>= 4 rows, 4 columns filled) | 18 |
| >= 2 specific regulation article/section citations | 14 |
| >= 3 risk-and-mitigation pairs | 14 |
| Minimum length (>= 600 words) | 8 |
| No placeholders remaining | 8 |
| **Total** | **100** |
