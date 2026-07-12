# Lab 0: Environment & Identity Setup

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 90 min  ·  **Autograding:** GitHub Actions + local `autograde/run.sh`

## Objective
Stand up the toolchain and professional identity you will use all semester: a
configured `git`, an SSH key registered with GitHub, a working GitHub account,
and a Docker + GPU smoke test. You will capture proof in a `setup-report.md`
and a captured command-output file.

**Why it matters:** every later lab is delivered as a private GitHub repository and
graded by automation. A security professional (CO5) works from a trusted,
identifiable, reproducible workstation - this lab builds yours.

## Course-Outcome Mapping
| Outcome | Evidence in this lab |
|---------|----------------------|
| CO5 - Activities a security specialist performs | Configure identity, keys, and container/GPU tooling |
| CO6 - Security+ SY0-701 readiness | Practices in Domain 4.0 (Security Operations): secure configuration, identity |

**Security+ SY0-701 domain:** 4.0 Security Operations (secure baseline, identity & access).

## Prerequisites
- A computer with `git`, `ssh`, and Docker installed (lab GPU machines qualify).
- A GitHub account (create one at https://github.com/join if needed - do this yourself; the grader never asks for a password).

## Tasks
1. **Identity** - set `git config --global user.name` and `user.email`, then record them in `setup-report.md`.
2. **SSH key** - generate an ed25519 key (`ssh-keygen -t ed25519`), add the public key to GitHub, and paste your public key fingerprint into the report.
3. **GitHub account** - record your GitHub username and profile URL.
4. **Docker smoke test** - run `docker --version` and `docker run --rm hello-world`; capture output.
5. **GPU smoke test** - run `nvidia-smi` (lab machines) or `system_profiler SPDisplaysDataType` / `sysctl -n machdep.cpu.brand_string` (Mac); capture output.
6. **Capture** - save the combined command output to `env-check.txt` and summarize in `setup-report.md` under the required headings.

## Deliverables
- `setup-report.md` with headings: **Identity**, **SSH**, **GitHub**, **Docker**, **GPU** (all filled, no placeholders).
- `env-check.txt` - captured output of the smoke-test commands.

## Submission
Commit both files and push to your assignment repository. The Actions workflow
runs `autograde/run.sh` automatically; you can also run it locally:
```
bash autograde/run.sh
```

## Grading
| Criterion | Points |
|-----------|-------:|
| `setup-report.md` present | 5 |
| Git identity (name + email) recorded | 10 |
| SSH key / fingerprint present | 10 |
| GitHub username / profile recorded | 10 |
| `env-check.txt` capture present | 10 |
| Docker smoke output present | 10 |
| GPU / CPU smoke output present | 10 |
| Required report sections present | 15 |
| No leftover placeholders | 10 |
| Report meets minimum length (150 words) | 10 |
| **Total** | **100** |
