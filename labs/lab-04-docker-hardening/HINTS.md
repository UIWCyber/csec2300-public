# Lab 4 - Hints (three tiers)

## Task group A - Base image & size
- **Tier 1 (nudge):** `latest` is a moving target and full base images ship things you do not need. https://docs.docker.com/develop/develop-images/instructions/
- **Tier 2 (guided):** Pin to a specific slim tag such as `python:3.12-slim` or a digest. Distroless is even smaller.
- **Tier 3 (near-solution):**
  ```
  FROM python:3.12-slim@sha256:____   # or at least python:3.12-slim, never :latest
  ```

## Task group B - Non-root user & secrets
- **Tier 1 (nudge):** Containers run as root by default; drop privilege. Secrets in `ENV` end up in image layers. https://docs.docker.com/engine/security/
- **Tier 2 (guided):** `RUN adduser` then `USER appuser`. Delete `ENV API_KEY=...`; pass secrets with `--env` or a mounted secret at runtime.
- **Tier 3 (near-solution):**
  ```
  RUN useradd --create-home --uid 10001 appuser
  USER appuser
  # remove:  ENV API_KEY=... / ENV DB_PASSWORD=...
  ```

## Task group C - Health check & build
- **Tier 1 (nudge):** Orchestrators need a signal that the app is alive. https://docs.docker.com/reference/dockerfile/#healthcheck
- **Tier 2 (guided):** Add `HEALTHCHECK` that curls or execs a liveness probe. Verify UID with `docker run --rm img id -u` (should not be 0).
- **Tier 3 (near-solution):**
  ```
  HEALTHCHECK --interval=30s --timeout=3s CMD ____ || exit 1
  ```
