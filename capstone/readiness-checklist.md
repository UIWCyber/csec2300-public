# Capstone Readiness Checklist

**CSEC 2300 Foundations of Cyber Security** | Instructor: Dr. Gonzalo D Parra

Run this self-audit before presentation day. Score each item GREEN (verified), YELLOW (partial), or RED (missing). Yellows and reds become your final-sprint task list. This checklist mirrors the grading criteria: fix anything that is both a rubric line and currently red before you polish anything else. Final deliverables are due at the posted deadline on Canvas; no late work is accepted.

## Pipeline and Repository

- [ ] **CI is green on HEAD.** The latest commit on your default branch passes every pipeline stage: lint, secret scan, and dependency audit.
  - *How to verify:* open the Actions tab for your latest commit, or run `gh run list --limit 1` and confirm the conclusion is success. The workflow must include a linter (such as ruff or hadolint), a secret scanner (such as gitleaks or trufflehog), and a dependency audit (such as pip-audit or osv-scanner).
- [ ] **No committed secrets.** No private keys, API keys, or tokens anywhere in the tree or history.
  - *How to verify:* run `gitleaks detect --source .` (or your CI secret scanner locally) and confirm zero findings. Secrets belong in files excluded by `.gitignore` or in Docker secrets, never in compose `environment:` blocks.
- [ ] **Repo hygiene is done.** Branch protection on the default branch, signed commits, `gdparra-edu` and `cyberknowledge` added as collaborators, and a README that describes the system.
  - *How to verify:* Settings > Branches shows a protection rule; `git log --show-signature -5` shows verified signatures; Settings > Collaborators lists both accounts.
- [ ] **Contribution spread is real.** Commits come from every team member across the semester, not one author or one weekend.
  - *How to verify:* run `git shortlog -sne` and confirm every member appears with a meaningful count.

## Containers and Network

- [ ] **Dockerfile is hardened.** Non-root `USER`, a `HEALTHCHECK`, and a pinned base image (a version tag or digest, never `:latest`).
  - *How to verify:* run `grep -E '^(USER|HEALTHCHECK|FROM)' Dockerfile` and inspect: the last USER is not root, HEALTHCHECK exists, and every FROM is pinned.
- [ ] **Compose is isolated and pinned.** Every image pinned (no `:latest`), resource limits set, and the Ollama port NOT published to the host; only the reverse proxy is exposed.
  - *How to verify:* run `grep -nE 'image:|ports:|mem_limit|cpus:' docker-compose.yml`. Ollama must have no `ports:` mapping; services talk over an internal compose network. Then `docker compose config` to confirm it parses.
- [ ] **TLS at the edge.** The stack is fronted by a reverse proxy terminating TLS; plain HTTP is not the entry point.
  - *How to verify:* run `curl -kI https://localhost` (or your proxy port) and confirm a TLS response from the proxy; `curl -I http://localhost:11434` from outside the compose network should fail.

## AI Layer

- [ ] **The agent is guarded.** Tool scopes are limited, output validation is in place, a human gate protects any sensitive tool, and agent actions are traced or logged.
  - *How to verify:* demonstrate one blocked action: send the agent a prompt that tries to trigger a sensitive tool and show the gate or validation stopping it, with the attempt visible in the trace or log.
- [ ] **LLM guardrails are documented.** Prompt-injection defenses and their known limits are written up (in the wiki or threat model), including residual risk you accepted.
  - *How to verify:* the write-up names at least one injection technique you tested, what blocked it, and what still partially works.

## Documentation and Governance

- [ ] **threat-model.md is complete.** STRIDE categories, assets, and mitigations are all filled in, with no TODO markers left.
  - *How to verify:* run `grep -c TODO threat-model.md` and expect 0; confirm the STRIDE table covers assets and mitigations for each category.
- [ ] **The wiki report is done.** The GitHub Wiki contains the final report with Overview, Architecture, Controls, Findings, and Next Steps, plus the governance artifacts: risk register, AI-use policy, and incident-response note.
  - *How to verify:* open the wiki and walk each page; no stubs, no TODO markers, and the controls section maps each control to a CO and an SY0-701 domain.
- [ ] **The Project board is current.** The GitHub Project board reflects real, up-to-date work: done items closed, in-progress items assigned, and a "definition of done for presentation day" issue present.
  - *How to verify:* open the board and confirm no stale cards; the most recent activity should be from this week, not from checkpoint 1.

## Demo

- [ ] **Demo dry-run is done.** The full stack starts clean on the actual presentation machine, the demo path was rehearsed end to end, and display output (HDMI or USB-C) was tested.
  - *How to verify:* run `docker compose down && docker compose up -d`, wait for healthchecks, and walk the exact demo script on the machine you will present from, connected to an external display.
- [ ] **The recorded fallback exists.** A recorded demo video is committed or linked in the repo in case the live demo fails.
  - *How to verify:* the README links the recording and a teammate has confirmed it plays.

## Submission

- [ ] **Links submitted on Canvas.** The GitHub repository and GitHub Project links are submitted through the Capstone Assignment on Canvas before the posted deadline.
  - *How to verify:* open the Canvas assignment and confirm the submission shows both links and a submitted timestamp.
