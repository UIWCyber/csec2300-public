# Lab 3: CI / DevSecOps Pipeline

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 100 min  ·  **Autograding:** workflow-file + secret-removal checks

## Objective
Build a GitHub Actions pipeline that runs a **linter**, a **secret scan**
(gitleaks-style), and a **dependency audit** - then fix a *seeded leaked secret*
already committed in `starter/app/config.py` and update `.gitignore`.

**Why it matters:** shifting security left into CI catches vulnerabilities and
leaked secrets before they ship (CO2).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO2 - Mitigation & deterrent techniques for attacks/vulnerabilities | Automated SAST/secret/dependency gates in CI |
| CO6 - Security+ readiness | Domain 2.0 (Threats/Vulnerabilities/Mitigations), 4.0 (Security Operations) |

**Security+ SY0-701 domain:** 2.0 Threats, Vulnerabilities & Mitigations; 4.0 Security Operations (automation, CI).

## Prerequisites
- Lab 2 complete. Basic YAML.

## Tasks
1. Create `.github/workflows/ci.yml` (a **new** workflow, separate from the autograder).
2. Add a job/step that runs a **linter** (e.g., `ruff`, `flake8`, `hadolint`, or `eslint`).
3. Add a step that runs a **secret scanner** (e.g., `gitleaks`).
4. Add a step that runs a **dependency audit** (e.g., `pip-audit`, `safety`, or `npm audit`).
5. **Remove the seeded secret** from `starter/app/config.py` (read it from an environment variable instead) and delete any committed `.env`.
6. Update `.gitignore` to exclude `.env`.
7. Write a `SECURITY.md` documenting that the leaked key was **rotated/revoked** (the lesson: rotate the secret; do not try to scrub history).

## Deliverables
- `.github/workflows/ci.yml` with the three security stages.
- `starter/app/config.py` with the hardcoded key removed; no `.env` in the tree.
- `.gitignore` excluding `.env`.
- `SECURITY.md` documenting secret rotation.

## Running this lab on Windows

Every command below is written for a Mac or Linux shell. On Windows 11, open
PowerShell from the Start menu, change into your lab folder, and use the right column.
Both columns run the same code and produce the same score.

| Mac, Linux or Git Bash | Windows PowerShell |
| --- | --- |
| `bash autograde/run.sh --syscheck` | `powershell -ExecutionPolicy Bypass -File autograde\run.ps1 --syscheck` |
| `bash autograde/run.sh` | `powershell -ExecutionPolicy Bypass -File autograde\run.ps1` |

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
| `ci.yml` workflow present | 12 |
| Linter step present | 13 |
| Secret-scan step present (gitleaks) | 18 |
| Dependency-audit step present | 12 |
| Seeded secret removed from repo (HEAD) | 20 |
| `.gitignore` excludes `.env` | 10 |
| `SECURITY.md` documents rotation | 15 |
| **Total** | **100** |
