# Lab 3 - Hints (three tiers)

## Task group A - Workflow scaffolding
- **Tier 1 (nudge):** A workflow is YAML under `.github/workflows/`. Start here: https://docs.github.com/en/actions/writing-workflows/quickstart
- **Tier 2 (guided):** Give it `on: [push, pull_request]` and one `jobs.security` block `runs-on: ubuntu-latest` with sequential steps.
- **Tier 3 (near-solution):**
  ```
  name: ci
  on: [push, pull_request]
  jobs:
    security:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v4
        - name: lint
          run: pipx run ruff check . || true
        - name: secret scan
          uses: gitleaks/gitleaks-action@v2
        - name: dependency audit
          run: pipx run pip-audit || true
  ```

## Task group B - Secret & dependency scanning
- **Tier 1 (nudge):** Secret scanners look for high-entropy strings and known key formats. https://github.com/gitleaks/gitleaks  ·  https://pypi.org/project/pip-audit/
- **Tier 2 (guided):** Use the `gitleaks/gitleaks-action@v2` action; run `pip-audit` (Python) or `npm audit` (Node) for dependencies.
- **Tier 3 (near-solution):** See the `secret scan` and `dependency audit` steps in the Tier-3 snippet above.

## Task group C - Fix the seeded secret
- **Tier 1 (nudge):** `starter/app/config.py` contains a hardcoded API key. Secrets belong in environment variables, never in source. https://12factor.net/config
- **Tier 2 (guided):** Replace the literal with `os.environ.get("API_KEY")` and add `.env` to `.gitignore`.
- **Tier 3 (near-solution):**
  ```
  import os
  API_KEY = os.environ.get("API_KEY", "")   # was: API_KEY = "sk-live-...."
  ```
