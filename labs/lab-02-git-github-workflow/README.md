# Lab 2: Git & GitHub Workflow

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 90 min  ·  **Autograding:** git-history inspection

## Objective
Practice the professional git workflow: feature branches, a merge, tags,
signed (or signed-off) commits, and secrets hygiene via `.gitignore`. The grader
inspects your `git log`.

**Why it matters:** version control is where security work is reviewed and
audited (CO3). Clean history and no leaked secrets are baseline hygiene.

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO3 - Access control, identity, cryptography for securing/managing | Signed commits (identity/crypto), branch protection discipline |
| CO6 - Security+ readiness | Domain 4.0 (Security Operations), 3.0 (change/config management) |

**Security+ SY0-701 domain:** 4.0 Security Operations; 3.0 Security Architecture (change management).

## Practice first
Warm up on these before doing the graded tasks:
- https://learngitbranching.js.org/
- https://gitmastery.me/

## Prerequisites
- Lab 0 complete (git identity + SSH key).

## Tasks
1. Make at least **8 commits** spread over **at least 2 different clock hours** (work incrementally, not one bulk dump).
2. Create a `feature/<name>` branch, commit on it, and **merge** it back into `main`.
3. Create an annotated **tag** (e.g., `v1.0`).
4. Keep a **consistent author identity** across your commits.
5. Add a `.gitignore` that excludes secrets (`*.env`, `*.pem`, `*.key`, `secrets/`).
6. Ensure **no secrets** are committed (no private keys or `API_KEY=` literals in the tree).

> The grader performs light history forensics. A single bulk commit is not blocked but is
> flagged for review; genuine incremental work over time passes cleanly.

## Deliverables
- A git repository (the assignment repository itself) whose history satisfies the checks.
- `.gitignore` with secret patterns.

## Submission
Push all branches and tags: `git push --all && git push --tags`.
Run `bash autograde/run.sh --syscheck` first to confirm git identity is set.

## Grading
| Criterion | Points |
|-----------|-------:|
| Directory is a git repository | 10 |
| At least 8 commits | 12 |
| Commits span >= 2 distinct hours | 8 |
| Consistent commit author | 8 |
| Feature branch exists | 12 |
| A merge commit exists | 12 |
| At least one tag | 8 |
| `.gitignore` excludes secret patterns | 15 |
| No secrets committed to the tree | 15 |
| **Total** | **100** |
