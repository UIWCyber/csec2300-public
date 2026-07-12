# Lab 7 - Hints (three tiers)

## Task group A - Services & images
- **Tier 1 (nudge):** Compose declares services, networks, and volumes. https://docs.docker.com/compose/
- **Tier 2 (guided):** Images: `ollama/ollama` and `ghcr.io/open-webui/open-webui`. Pin a specific tag, never `:latest`.
- **Tier 3 (near-solution):**
  ```
  services:
    ollama:
      image: ollama/ollama:0.3.14
      volumes: [ollama:/root/.ollama]
  ```

## Task group B - Private network & limits
- **Tier 1 (nudge):** A user-defined network isolates the stack; limits cap resource abuse. https://docs.docker.com/compose/networking/
- **Tier 2 (guided):** Declare a `networks:` block and attach both services; add `mem_limit` (or `deploy.resources.limits`).
- **Tier 3 (near-solution):**
  ```
  networks:
    llmnet:
  services:
    ollama:
      networks: [llmnet]
      mem_limit: 8g
  ```

## Task group C - Health
- **Tier 1 (nudge):** Ollama exposes a version endpoint. https://github.com/ollama/ollama/blob/main/docs/api.md
- **Tier 2 (guided):** After `docker compose up -d`, curl `http://localhost:11434/api/version`.
- **Tier 3 (near-solution):**
  ```
  curl -fsS http://localhost:11434/api/version
  ```
