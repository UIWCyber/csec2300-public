# Lab 0 - Hints (three tiers per task group)

## Task group A - Git identity & SSH key
- **Tier 1 (nudge):** Git needs to know who you are before it can attribute commits. See the "First-Time Git Setup" chapter: https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup and GitHub's SSH docs: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
- **Tier 2 (guided):** Use `git config --global user.name` and `git config --global user.email`. Generate a key with `ssh-keygen -t ed25519 -C "you@example.com"`. Show its fingerprint with `ssh-keygen -lf ~/.ssh/id_ed25519.pub`.
- **Tier 3 (near-solution):**
  ```
  git config --global user.name "_____"
  git config --global user.email "_____@_____"
  ssh-keygen -t ed25519 -C "_____"
  ssh-keygen -lf ~/.ssh/id_ed25519.pub   # paste this SHA256:____ line into the report
  ```

## Task group B - GitHub account & smoke tests
- **Tier 1 (nudge):** Confirm the toolchain actually runs, not just that it is installed. Docker: https://docs.docker.com/get-started/  ·  NVIDIA SMI: https://developer.nvidia.com/nvidia-system-management-interface
- **Tier 2 (guided):** Capture `docker --version` and `docker run --rm hello-world`. For GPU use `nvidia-smi`; on a Mac without NVIDIA use `system_profiler SPDisplaysDataType`.
- **Tier 3 (near-solution):**
  ```
  { docker --version; docker run --rm hello-world; nvidia-smi || system_profiler SPDisplaysDataType; } | tee env-check.txt
  ```

## Task group C - Report structure
- **Tier 1 (nudge):** The grader looks for specific section headings; skim the Grading table in the README.
- **Tier 2 (guided):** Use markdown `##` headings named exactly Identity, SSH, GitHub, Docker, GPU. Remove every `TODO`/`<...>` placeholder.
- **Tier 3 (near-solution):**
  ```
  ## Identity
  Name: _____   Email: _____
  ## SSH
  Fingerprint: SHA256:_____
  ## GitHub
  Username: _____   Profile: https://github.com/_____
  ## Docker
  _____ (paste version + hello-world confirmation)
  ## GPU
  _____ (paste nvidia-smi / system_profiler summary)
  ```
