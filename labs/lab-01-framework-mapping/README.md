# Lab 1: Framework Mapping (NIST CSF & CIS Controls)

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 75 min  ·  **Autograding:** Structured-answer grader (`answers.yaml`)

## Objective
Read a realistic breach scenario and map its events to the five **NIST CSF 2.0**
functions (Identify, Protect, Detect, Respond, Recover) and to specific **CIS
Critical Security Controls v8**. You produce a machine-checkable `answers.yaml`.

**Why it matters:** frameworks are the shared language of security governance
(CO1). Analysts translate messy incidents into framework language every day.

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO1 - Basic concepts of information systems security | Classify events by CSF function and CIS control |
| CO6 - Security+ readiness | Domain 5.0 (Governance, Risk & Compliance): frameworks |

**Security+ SY0-701 domain:** 5.0 Security Program Management & Oversight (frameworks, GRC); 1.0 General Security Concepts.

## Per-student scenario
You are assigned scenario **A** or **B** based on your repository (anti-copy: a
classmate on the other variant has different correct answers). First run:
```
bash starter/which-scenario.sh
```
Then read `starter/scenario-A.md` **or** `starter/scenario-B.md` accordingly.

## Prerequisites
- Run `starter/which-scenario.sh` and read your assigned scenario file.
- Skim the NIST CSF 2.0 functions and the CIS Controls v8 list (links in HINTS).

## Tasks
1. Determine your variant and read the matching scenario file.
2. For each numbered event, choose the **primary CSF function**.
3. For each control question, name the **CIS Control number** that best applies.
4. Answer the impact question (CIA triad).
5. Fill all fields in `answers.yaml` (copy the template from `starter/answers-template.yaml`).

## Deliverables
- `answers.yaml` at the repo root with every field filled.

## Submission
Push to your repository; the workflow runs `autograde/run.sh`. Run locally with `bash autograde/run.sh`.
Run `bash autograde/run.sh --syscheck` first to confirm your environment.

## Grading
| Criterion | Points |
|-----------|-------:|
| `answers.yaml` present & parseable | 10 |
| CSF: detection event -> Detect | 10 |
| CSF: containment event -> Respond | 10 |
| CSF: preventive control -> Protect | 10 |
| CSF: restore-from-backup -> Recover | 10 |
| CSF: asset inventory -> Identify | 10 |
| CIS: primary (access control) number | 10 |
| CIS: secondary number (variant-dependent) | 10 |
| CIS: recovery (backups) number | 10 |
| CIA: primary impact (variant-dependent) | 10 |
| **Total** | **100** |
