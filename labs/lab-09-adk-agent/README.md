# Lab 9: Build a Tool-Using Agent (Authorization Limits)

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 110 min  ·  **Autograding:** unit tests on your agent module

## Objective
Build a small Python agent (Google ADK or a plain function-calling loop against
Ollama) whose tools are **allowlisted**. A dangerous tool must be **absent** from
the allowlist, and the agent must **refuse** any tool not on the list.

**Why it matters:** agents act. Confining them to least-privilege tools is the
core control that keeps an autonomous system safe (CO5).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO5 - Activities a security specialist performs | Enforce least-privilege tool authorization on an agent |
| CO6 - Security+ readiness | Domain 4.0 Security Operations (automation with guardrails) |

**Security+ SY0-701 domain:** 4.0 Security Operations (automation, orchestration, least privilege).

## Prerequisites
- Python 3. Optional: Ollama for a live model loop.

## Contract (the grader depends on this)
Create `agent.py` at the repo root exposing:
- `ALLOWED_TOOLS` - a list/set/dict of allowed tool names (non-empty).
- `run_tool(name, **kwargs)` - executes a tool **only if** `name` is in `ALLOWED_TOOLS`; otherwise it **refuses** (raise `PermissionError`/`ValueError`, or return a value containing "refus"/"not allowed").
- No dangerous tool (`shell`, `exec`, `eval`, `system`, `delete_file`, `rm`, `subprocess`, `write_file`) may appear in `ALLOWED_TOOLS`.

## Tasks
1. Define at least two **safe** tools (e.g., `get_time`, `calculator`) with keyword-arg signatures.
2. Populate `ALLOWED_TOOLS` with only safe tools; **remove** the dangerous `shell` tool from the starter.
3. Enforce the allowlist inside `run_tool` (default-deny).
4. (Optional) Wire a function-calling loop to Ollama.
5. Keep `tests/test_agent.py` passing (`python3 -m unittest`); it uses a **mocked deterministic LLM**, so no Ollama is needed.

## Deliverables
- `agent.py` implementing the contract.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh` (and `--syscheck` first).

## Grading (behavior tested by executing your agent against a mocked deterministic LLM)
| Criterion | Points |
|-----------|-------:|
| `agent.py` present | 12 |
| `ALLOWED_TOOLS` defined & non-empty | 18 |
| No dangerous tool in allowlist | 25 |
| Mock LLM's non-allowlisted request refused | 25 |
| Benign mock LLM tool sequence executes | 20 |
| **Total** | **100** |

*The allowlist/refusal/benign criteria are in a dependency group with `agent_exists`: if `agent.py`
is missing or fails to import, they report "blocked by agent_exists" so you see the root cause.*
