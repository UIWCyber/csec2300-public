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

## Submission
Push to your repository. Run locally with `bash autograde/run.sh`.
Run `bash autograde/run.sh --syscheck` first to confirm your environment.

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
