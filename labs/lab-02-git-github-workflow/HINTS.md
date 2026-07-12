# Lab 2 - Hints (three tiers)

## Task group A - Branch, merge, tag
- **Tier 1 (nudge):** A feature branch keeps risky work off `main` until it is reviewed. Practice at https://learngitbranching.js.org/ then read https://docs.github.com/en/get-started/using-git
- **Tier 2 (guided):** `git switch -c feature/x`, commit, then `git switch main && git merge --no-ff feature/x`. Tag with `git tag -a v1.0 -m "..."`.
- **Tier 3 (near-solution):**
  ```
  git switch -c feature/____
  git commit -am "____"
  git switch main
  git merge --no-ff feature/____ -m "merge feature"
  git tag -a v1.0 -m "release ____"
  ```

## Task group B - Signed / signed-off commits
- **Tier 1 (nudge):** Commit signing proves who authored a change. https://docs.github.com/en/authentication/managing-commit-signature-verification
- **Tier 2 (guided):** SSH signing is easy: `git config gpg.format ssh` and `git config user.signingkey ~/.ssh/id_ed25519.pub`, then `git commit -S`. If keys are unavailable, `git commit -s` adds a Signed-off-by trailer (the grader accepts either).
- **Tier 3 (near-solution):**
  ```
  git config --global gpg.format ssh
  git config --global user.signingkey ~/.ssh/id_ed25519.pub
  git commit -S -m "signed: ____"      # or:  git commit -s -m "signed-off: ____"
  ```

## Task group C - Secrets hygiene
- **Tier 1 (nudge):** Never commit keys or `.env` files. https://docs.github.com/en/code-security/secret-scanning
- **Tier 2 (guided):** Add patterns to `.gitignore` before creating any secret file. Verify with `git status --ignored`.
- **Tier 3 (near-solution):**
  ```
  # .gitignore
  *.env
  *.pem
  *.key
  secrets/
  ```
