# Lab 11 - Hints (three tiers)

## Task group A - Reuse the CI, Docker, and compose from earlier labs
- **Tier 1 (nudge):** You already built these in Labs 3, 4, and 7; bring them together.
- **Tier 2 (guided):** Copy your hardened `Dockerfile`, `docker-compose.yml`, and `ci.yml`, then confirm each still passes its checks.
- **Tier 3 (near-solution):** CI needs lint + gitleaks + pip-audit; Dockerfile needs `USER` + `HEALTHCHECK` + a pinned slim base; compose needs pinned images + `mem_limit`.

## Task group B - Threat model
- **Tier 1 (nudge):** STRIDE = Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege. https://learn.microsoft.com/azure/security/develop/threat-modeling-tool-threats
- **Tier 2 (guided):** List assets (models, data volume, secrets), then a threat + mitigation per STRIDE category.
- **Tier 3 (near-solution):**
  ```
  ## Assets
  - ____
  ## STRIDE
  | Category | Threat | Mitigation |
  |----------|--------|-----------|
  | Spoofing | ____ | ____ |
  ```

## Task group C - Report stub & secrets
- **Tier 1 (nudge):** The report should be ready to paste into a GitHub wiki. Keep secrets out of the repo entirely.
- **Tier 2 (guided):** `report.md` sections: Overview, Architecture, Controls, Findings, Next Steps. Scan the tree for keys before pushing.
- **Tier 3 (near-solution):** `grep -R -nE "BEGIN .*PRIVATE KEY|API_KEY=sk-" .` should return nothing.
