# Lab 4: Docker Hardening

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 90 min  ·  **Autograding:** Dockerfile parse (+ optional build/inspect)

## Objective
Take the deliberately sloppy `Dockerfile` in this repo (runs as **root**, uses
`:latest`, bakes **secrets** into `ENV`, huge base image, no health check) and
harden it: non-root `USER`, a **pinned slim** base, no secrets, and a
`HEALTHCHECK`.

**Why it matters:** container images are production attack surface. Least
privilege and reproducible, minimal images reduce blast radius (CO1, CO2).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO1 - Basic concepts of information systems security | Least privilege, minimal trusted base |
| CO2 - Mitigation & deterrent techniques | Drop root, pin versions, remove embedded secrets |
| CO6 - Security+ readiness | Domain 3.0 Security Architecture (secure baselines, containers) |

**Security+ SY0-701 domain:** 3.0 Security Architecture (secure baselines, virtualization/containers).

## Prerequisites
- Docker installed (optional for full grade; the grader still parses the Dockerfile without Docker).

## Tasks
1. Pin the base image to a specific **slim** tag or digest (no `:latest`).
2. Create and switch to a **non-root** user with a `USER` directive.
3. Remove all secrets from `ENV`/`ARG`; read them at runtime instead.
4. Add a `HEALTHCHECK` instruction.
5. Prefer `COPY` over `ADD`; do not run privileged installs you do not need.
6. (Optional, if Docker present) Build and confirm the container runs as a non-root UID.

## Deliverables
- A hardened `Dockerfile` at the repo root.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh`.
Run `bash autograde/run.sh --syscheck` first to confirm the Docker daemon is reachable.

## Grading
| Criterion | Points |
|-----------|-------:|
| `Dockerfile` present | 10 |
| Base image pinned (not `:latest`) | 15 |
| Minimal/slim base (slim/alpine/distroless) | 10 |
| Non-root `USER` directive | 15 |
| No secrets in `ENV`/`ARG` | 15 |
| `HEALTHCHECK` present | 15 |
| Image builds from your Dockerfile (Tier C) | 10 |
| Container runs as non-root (Tier C) | 5 |
| App still serves `/health` (Tier C) | 5 |
| **Total** | **100** |

*The three Tier C criteria build and run your image; they are skipped (0 pts, clearly marked
"skipped (environment unavailable)") when the Docker daemon is unreachable, and graded fully on the
lab GPU machines. `runs-as-non-root` and `serves /health` are in a dependency group with the image
build: if the build fails they report "blocked by image_builds" so you see the single root cause.*
