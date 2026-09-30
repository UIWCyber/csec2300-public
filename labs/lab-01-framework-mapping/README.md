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

## Running this lab on Windows

Every command below is written for a Mac or Linux shell. On Windows 11, open
PowerShell from the Start menu, change into your lab folder, and use the right column.
Both columns run the same code and produce the same score.

| Mac, Linux or Git Bash | Windows PowerShell |
| --- | --- |
| `bash autograde/run.sh --syscheck` | `powershell -ExecutionPolicy Bypass -File autograde\run.ps1 --syscheck` |
| `bash autograde/run.sh` | `powershell -ExecutionPolicy Bypass -File autograde\run.ps1` |
| `bash starter/which-scenario.sh` | `powershell -ExecutionPolicy Bypass -File starter\which-scenario.ps1` |

The `-ExecutionPolicy Bypass` part is there because Windows blocks scripts by default.
It applies to that one command only and changes nothing on your machine.

## Submission
Push your deliverables to your assignment repository before the deadline. That is the
whole submission: nothing is uploaded to Canvas.

The grader runs on every push. Open your repository and look next to your commit: a yellow
dot means the grader is running, a green check means your score is 100, and a red X means
something is still missing. Click it, then click Details, to see every criterion and the
feedback line saying what the grader looked for. Fix what it names, push again, and repeat.
You may push as many times as you like; the last score before the deadline is your grade.

Grading yourself first is optional and needs Python 3 on your machine: `bash autograde/run.sh`,
or the PowerShell command from the table above.

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
