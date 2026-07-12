# Capstone Proposal

**CSEC 2300 Foundations of Cyber Security** | Instructor: Dr. Gonzalo D Parra

> Complete every section, replace all bracketed placeholders, and submit through the Capstone Proposal assignment on Canvas by the deadline on the course outline. The proposal is worth 3% of your course grade. No late work is accepted: posted deadline or zero. The instructor must approve this proposal before your team starts building.

---

## 1. Team Roster

Teams are **2 to 3 students**. No solo capstones.

| # | Name | UIW Email | GitHub Username |
|---|------|-----------|-----------------|
| 1 | [name] | [email] | [github] |
| 2 | [name] | [email] | [github] |
| 3 | [name or "N/A (team of 2)"] | [email] | [github] |

**Team name (used for the repo):** [team-name]

### Shared Availability Grid

Before committing to this team, compare schedules: you will collaborate and learn together all semester, so make sure you share workable meeting times. Mark each block every member can meet with an X.

| Time Block | Mon | Tue | Wed | Thu | Fri | Sat | Sun |
|------------|-----|-----|-----|-----|-----|-----|-----|
| Morning (before noon) | | | | | | | |
| Early afternoon | | | | | | | |
| Late afternoon | | | | | | | |
| Evening | | | | | | | |

**Agreed weekly meeting time(s):** [at least one recurring block every member marked]

---

## 2. GitHub Setup

| Item | Value |
|------|-------|
| Repository URL | [https://github.com/...] |
| GitHub Project board URL | [https://github.com/.../projects/...] |
| Collaborators added | [ ] `gdparra-edu` &nbsp; [ ] `cyberknowledge` |
| Wiki enabled (final report lives here) | [ ] Yes |

---

## 3. Stack Configuration

The capstone is a **secure local-AI stack**: Dockerized Ollama + Open WebUI + an AI agent, delivered through a security-gated CI pipeline. State your configuration choices.

| Component | Your Choice | Notes |
|-----------|-------------|-------|
| Ollama model(s) and pinned tag(s) | [e.g., a small instruct model, pinned tag, never `:latest`] | [why this model, hardware fit] |
| Open WebUI version (pinned) | [image tag or digest] | |
| AI agent framework | [e.g., ADK agent from the labs] | [what the agent does] |
| Agent tools and scopes | [tools the agent may call, and their limits] | [which tools require a human gate] |
| Reverse proxy / TLS at the edge | [e.g., Caddy or nginx with a local certificate] | |
| CI pipeline stages | [lint, secret scan, dependency audit, build] | [tools per stage] |
| Host environment | [OS, RAM, GPU if any] | [each member's demo machine] |

---

## 4. Target Security Controls

List the controls you commit to implementing. Each control must map to at least one course outcome and one SY0-701 domain. Add rows as needed; a strong proposal targets 6 to 10 controls across at least three domains.

Course outcomes for reference:

- **CO1**: Describe basic concepts of information systems security, including security technology and principles, software security and trusted platforms, and security management.
- **CO2**: Select appropriate mitigation and deterrent techniques to address network attacks and vulnerabilities.
- **CO3**: Describe how access control, identity management and cryptography can be applied to securing a network and managing risk.
- **CO4**: Identify and analyze privacy and policy issues.
- **CO5**: Engage in activities that an Information Systems Security specialist would normally carry out in the performance of his/her duties.
- **CO6**: Understand the concepts and domains needed for acquiring the CompTIA Security+ (SY0-701) certification exam.

SY0-701 domains for reference: 1.0 General Security Concepts, 2.0 Threats, Vulnerabilities, and Mitigations, 3.0 Security Architecture, 4.0 Security Operations, 5.0 Security Program Management and Oversight.

| # | Control | Type (preventive / detective / corrective) | CO | SY0-701 Domain |
|---|---------|--------------------------------------------|----|----------------|
| 1 | [e.g., non-root containers with pinned base images] | Preventive | CO2 | 3.0 |
| 2 | [e.g., network segmentation: Ollama unreachable from the host network] | Preventive | CO2 | 3.0 |
| 3 | [e.g., TLS termination at the reverse proxy] | Preventive | CO3 | 3.0 |
| 4 | [e.g., CI secret scanning on every push] | Detective | CO5 | 4.0 |
| 5 | [e.g., prompt-injection guardrails with output validation on the agent] | Preventive | CO2 | 2.0 |
| 6 | [e.g., AI-use policy and risk register in the wiki] | Governance | CO4 | 5.0 |
| 7 | [add more] | | | |

---

## 5. Milestone Plan

Align your plan to the two graded checkpoints and the presentation dates posted on the course outline. Fill in what your team will have DONE by each milestone.

| Milestone (see course outline for the posted deadline) | Deliverable state your team commits to |
|---------------------------------------------------------|----------------------------------------|
| Proposal approved | This document approved; repo, board, and wiki created; collaborators added |
| **Checkpoint 1** | [e.g., Ollama + Open WebUI running in compose; CI pipeline with lint and secret scan passing; threat model drafted] |
| **Checkpoint 2** | [e.g., full stack segmented and TLS-fronted; agent scoped, gated, and traced; all CI stages green; governance artifacts drafted in the wiki] |
| Presentation and final submission | [e.g., all controls implemented and mapped; wiki report complete; demo dry-run done; recorded demo fallback in the repo] |

---

## 6. Roles and Contribution Plan

Every member must contribute commits all semester; the grader checks contribution spread. Roles can rotate, but name a starting owner per area.

| Area | Starting Owner | Rotation Plan |
|------|----------------|---------------|
| Containers and compose | [name] | [e.g., swap after checkpoint 1] |
| CI pipeline and repo hygiene | [name] | |
| Agent and guardrails | [name or shared] | |
| Documentation, wiki, and board | [name or shared] | |

---

## 7. Risks and Assumptions

List what could derail the project and what you assume to be true. Be honest; this section seeds the risk register you will keep in the wiki.

| # | Risk or Assumption | Likelihood (L/M/H) | Impact (L/M/H) | Mitigation or Fallback |
|---|--------------------|--------------------|----------------|------------------------|
| 1 | [e.g., demo laptop lacks RAM for the chosen model] | | | [e.g., fall back to a smaller quantized model] |
| 2 | [e.g., a teammate becomes unavailable] | | | [e.g., shared ownership, talk to the instructor early] |
| 3 | [add more] | | | |

---

## 8. Approval

By submitting, every team member affirms they reviewed this proposal and the shared availability grid, and commit to the milestone plan above.

| Team member signatures (typed name and date of signing) |
|----------------------------------------------------------|
| [name] |
| [name] |
| [name or "N/A (team of 2)"] |

**Instructor approval (Dr. Gonzalo D Parra):** ______________________________

**Approval conditions or required changes (instructor use):**

[blank]
