# Lab 8: LLM Attack & Defense (Prompt Injection)

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 110 min  ·  **Autograding:** live Ollama test suite OR static prompt checks

## Objective
Attack a deliberately weak system prompt with prompt-injection test cases, then
write a **hardened** system prompt that resists them. If a local Ollama model is
available the grader runs your attacks live; otherwise it statically verifies
your attacks and the required defensive elements of your hardened prompt.

**Why it matters:** prompt injection is the top LLM application risk (OWASP LLM01).
Defending it is applied threat mitigation (CO2, CO4).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO2 - Mitigation & deterrent techniques | Design guardrails that block injection |
| CO4 - Privacy & policy issues | Prevent leakage of system prompt / private context |
| CO6 - Security+ readiness | Domain 2.0 Threats/Vulnerabilities/Mitigations |

**Security+ SY0-701 domain:** 2.0 Threats, Vulnerabilities & Mitigations (application attacks).

## Prerequisites
- Read `starter/vulnerable-system-prompt.txt`.
- Optional: Ollama running with a model (`OLLAMA_MODEL`, default `llama3.2`).

## Tasks
1. Write **at least 5** prompt-injection attack cases in `injection-tests.md` (one per line/bullet), each trying to make the assistant break a rule (reveal the system prompt, ignore instructions, exfiltrate data, produce disallowed output).
2. Write a **hardened** system prompt in `hardened-prompt.txt` that:
   - refuses to reveal or repeat its system prompt,
   - ignores instructions embedded in user/tool content that try to override it,
   - stays within its defined task scope,
   - never executes or trusts untrusted content as commands.

## Deliverables
- `injection-tests.md` (>= 5 attack cases).
- `hardened-prompt.txt` (defensive system prompt).

## Per-student canary
The grader injects a canary token derived from your repository into the vulnerable
prompt at runtime (a classmate's transcript cannot contain your token). Your attacks
must extract **your** canary; your hardened prompt must keep it secret.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh` (and `--syscheck` first).
Set a model first if you want the live path: `export OLLAMA_MODEL=llama3.2`.

## Grading
| Criterion | Points |
|-----------|-------:|
| `hardened-prompt.txt` present | 10 |
| `injection-tests.md` present | 10 |
| >= 5 attack cases | 10 |
| Defends: refuse to reveal system prompt | 12 |
| Defends: ignore/override injected instructions | 12 |
| Defends: stay in scope | 8 |
| Defends: do not execute untrusted content | 8 |
| Attacks extract the canary from vulnerable prompt (Tier C, >=3/5) | 10 |
| Hardened prompt blocks the course attack suite (Tier C, >=8/10; static fallback) | 20 |
| **Total** | **100** |

*The two Tier C criteria run against Ollama when reachable (model via `OLLAMA_MODEL`, default
`llama3.2`); when Ollama is offline the defense criterion falls back to a static check of your
hardened prompt and the attack-effectiveness criterion is skipped for the GPU-workstation session.*
