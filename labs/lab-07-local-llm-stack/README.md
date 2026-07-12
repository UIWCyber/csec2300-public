# Lab 7: Local LLM Stack (Ollama + Open WebUI)

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 100 min  ·  **Autograding:** compose validation (+ optional health check)

## Objective
Write a `docker-compose.yml` that deploys **Ollama** + **Open WebUI** on a
**private network**, with **pinned images** and **resource limits**, and a named
volume for model data.

**Why it matters:** running models locally keeps data on-premises - a privacy
and data-governance control (CO4). Pinning and limits are supply-chain and
availability hygiene.

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO4 - Privacy and policy issues | Keep inference and data local; document the boundary |
| CO6 - Security+ readiness | Domain 3.0/4.0 (architecture, secure deployment) |

**Security+ SY0-701 domain:** 3.0 Security Architecture; 4.0 Security Operations.

## Prerequisites
- Docker + docker compose (optional for full grade; compose is parsed without Docker).

## Tasks
1. Define an `ollama` service with a **pinned** image and a **named volume** for `/root/.ollama`.
2. Define an `open-webui` service with a **pinned** image, publishing only the WebUI port to the host.
3. Put both on a **user-defined private network**; **do not publish Ollama's 11434 to the host** (WebUI reaches it over the private network).
4. Add **resource limits** (`mem_limit` or `deploy.resources.limits`) to each service.
5. (Tier C, if Docker present) `docker compose up -d`; the grader confirms WebUI responds on the host while a host probe of `11434` fails (isolation).

## Deliverables
- `docker-compose.yml` at the repo root satisfying the checks.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh` (and `--syscheck` first).

## Grading
| Criterion | Points |
|-----------|-------:|
| `docker-compose.yml` present & parseable | 10 |
| `ollama` service defined | 10 |
| `open-webui` service defined | 10 |
| Images pinned (no `:latest`) | 15 |
| Private user-defined network | 12 |
| Resource limits on services | 12 |
| Named volume for model data | 8 |
| Ollama 11434 not published to host (static) | 8 |
| Isolation probe: WebUI up, host 11434 unreachable (Tier C) | 15 |
| **Total** | **100** |

*The isolation probe is skipped ("skipped (environment unavailable)") unless the stack is running; it is
graded on the GPU workstations. Isolation is probed from outside the network, not read from the YAML.*
