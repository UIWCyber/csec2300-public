# Lab 9 - Hints (three tiers)

## Task group A - Allowlist
- **Tier 1 (nudge):** An allowlist is default-deny: only listed tools may run. https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html
- **Tier 2 (guided):** Keep tool functions in a dict and derive `ALLOWED_TOOLS` from the safe subset. Delete `shell`.
- **Tier 3 (near-solution):**
  ```
  TOOLS = {"get_time": _get_time, "calculator": _calc}
  ALLOWED_TOOLS = set(TOOLS)      # note: no "shell"
  ```

## Task group B - Enforcement & refusal
- **Tier 1 (nudge):** Check authorization before dispatch, not after. https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
- **Tier 2 (guided):** In `run_tool`, if `name not in ALLOWED_TOOLS` raise `PermissionError`. Otherwise call the tool.
- **Tier 3 (near-solution):**
  ```
  def run_tool(name, **kw):
      if name not in ALLOWED_TOOLS:
          raise PermissionError(f"refused: {name} not allowed")
      return TOOLS[name](**kw)
  ```

## Task group C - Model loop (optional)
- **Tier 1 (nudge):** The model proposes a tool; your code decides whether to run it. https://github.com/ollama/ollama/blob/main/docs/api.md
- **Tier 2 (guided):** Parse the model's requested tool name and pass it through `run_tool` so the allowlist still gates it.
- **Tier 3 (near-solution):** `resp = ollama(...); run_tool(resp["tool"], **resp["args"])`
