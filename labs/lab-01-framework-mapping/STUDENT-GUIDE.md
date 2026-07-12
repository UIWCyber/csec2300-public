# Student Guide: Lab 1 - Framework Mapping (NIST CSF & CIS Controls)

This guide walks you through the mechanics of completing and submitting Lab 1.
It does not give you the analysis answers - those come from reading your
scenario carefully and using `README.md` and `HINTS.md`. Follow the steps
below in order.

## 1. What you will build / prove

You will read a short breach-scenario writeup (assigned to you personally,
either Scenario A or Scenario B), classify its events against the five NIST
CSF 2.0 functions, name the relevant CIS Controls v8 numbers, and identify
the primary CIA-triad impact. Your answers go into one file, `answers.yaml`,
at the root of your repository. An automated grader checks that file and
gives you a score out of 100.

## 2. Before you start

You need:
- A web browser and a GitHub account (from Lab 0).
- `git` installed and configured (from Lab 0).
- `python3` available on your machine (this lab's grader is pure Python,
  no Docker or GPU required).

The authoritative instructions for what to analyze and how to answer live in
two files inside your repo once you accept the assignment:
- **`README.md`** - the objective, the tasks, and the exact grading table.
- **`HINTS.md`** - a three-tier hint ladder (nudge -> guided -> near-solution)
  for the CSF functions, the CIS Controls, and the CIA/YAML format.

This guide only covers *how to run things*. For *what the right answer is*,
read those two files and think through your assigned scenario.

## 3. Step 1 - Accept and open the lab

1. Open the Lab 1 assignment link posted on Canvas. It is a your GitHub assignment repository
   invite.
2. Click **Accept this assignment**. GitHub creates a personal copy of the
   repository for you (this is what makes your scenario variant unique to
   you - see Step 4).
3. Clone your repository to your computer. Copy the clone URL from the green
   **Code** button on your repo page, then in a terminal:
   ```
   git clone <your-repo-clone-url>
   cd <your-repo-folder-name>
   ```
   On Windows, use **Git Bash** (installed with Git for Windows) for all
   commands in this guide - it gives you the same `bash`/`ls`/`cd` commands
   shown here.

## 4. Step 2 - Find out your scenario variant

Your scenario (A or B) is derived from your repository's name, so every
student gets a consistent, personal variant. Run:
```
bash starter/which-scenario.sh
```
> **what you'll see:**
> ```
> Your assigned scenario variant: B
> Read starter/scenario-B.md
> ```
> (Your letter may be A instead of B - that is expected and normal.)

Open the file it names (`starter/scenario-A.md` or `starter/scenario-B.md`)
and read it carefully. Do not read the other scenario file - it belongs to a
different variant and its answers will not match yours.

## 5. Step 3 - Run the system check first

Before doing any analysis, confirm your environment is ready:
```
bash autograde/run.sh --syscheck
```
> **what you'll see:**
> ```
> System check (pre-flight) for <your-repo-name>
> ------------------------------------------------------------------------
> STATUS CHECK                                    FIX HINT
> PASS   python3 available
> PASS   starter files intact
> ------------------------------------------------------------------------
> All preflight checks passed - you can start the lab.
> ```

See the syscheck screenshot in `guide-assets/lab-01-syscheck.png` for a
worked example.

If anything shows `FAIL`:
- **`python3 available` fails** - install Python 3 from
  https://www.python.org/downloads/ (Windows: check "Add python.exe to PATH"
  during install) and reopen your terminal.
- **`starter files intact` fails** - you (or a tool) deleted or renamed a
  file under `starter/`. Do not edit or move anything in `starter/`; if a
  file is missing, re-clone the repo into a fresh folder rather than trying
  to recreate it by hand.

## 6. Steps 4-6 - Do the analysis

Work through the **Tasks** section of `README.md` in order:

1. **Read your scenario file** end to end. It numbers a sequence of events
   (phishing/misuse, detection, containment, impact, recovery, and a
   post-incident gap) and lists three control questions plus one CIA
   question.
2. **Classify each event against a NIST CSF 2.0 function.** The five
   functions are Identify, Protect, Detect, Respond, Recover - they form a
   lifecycle from "know what you have" to "bounce back after an incident."
   `HINTS.md` Task Group A gives you verb-matching cues (for example, which
   verbs typically signal a detection versus a containment action) if you
   get stuck.
3. **Name the CIS Control number** for each of the three control questions
   in your scenario file (primary access-control question, a
   scenario-specific secondary question, and the recovery/backups
   question). `HINTS.md` Task Group B lists several named CIS Controls
   v8 areas to help you narrow down the right number; the official list is
   linked there too.
4. **Answer the CIA question** with exactly one of: `confidentiality`,
   `integrity`, or `availability` - whichever property the incident's impact
   statement in your scenario primarily describes. `HINTS.md` Task Group C
   walks through the reasoning.
5. **Fill in `answers.yaml`.** Copy the template so you don't miss a field:
   ```
   cp starter/answers-template.yaml answers.yaml
   ```
   Open `answers.yaml` in a text editor (VS Code, Notepad++, or even
   Notepad) and replace every empty `""` with your answer. Two formatting
   rules the grader relies on:
   - CSF answers are plain words: `identify`, `protect`, `detect`,
     `respond`, or `recover` (lowercase is fine; the grader is
     case-insensitive).
   - CIS Control answers are just the **number** (for example `6`), not a
     control name.
   - Keep the `key: value` shape on one line per field. If you want to keep
     a value in quotes, put it as `field: "value"` with nothing else after
     the closing quote on that line - trailing text after a quoted value can
     get folded into your answer by the simple parser this grader uses.

   `answers.yaml` must live at the **root** of your repository (next to
   `README.md`), not inside `starter/`.

## 7. Final step - Validate and capture your proof

Run the grader:
```
bash autograde/run.sh
```
This prints a JSON report with one entry per grading criterion (10 points
each, 100 total), plus two verification codes at the bottom:
```
WORK-FP  : <a short hash of your submitted files>
ATTEST   : <a short hash tying your score to your repo and commit>
```

> **what a fully passing run looks like:** see
> `guide-assets/lab-01-completion.png`. Your own file names, hashes, and
> exact feedback text will differ - what matters is `"total": 100` and a
> `WORK-FP` / `ATTEST` pair at the bottom.

**This screenshot (or a copy/paste of your own terminal output showing the
score, `WORK-FP`, and `ATTEST`) is what you submit** as proof of completion,
in addition to committing and pushing `answers.yaml`. Commit and push:
```
git add answers.yaml
git commit -m "Complete Lab 1 framework mapping"
git push
```
your GitHub assignment repository's Actions workflow re-runs the same grader on your pushed
repo automatically; you can check the result under the **Actions** tab on
your repo page.

If your score is below 100, read the `feedback` field for each criterion
that shows `0` points - it tells you exactly which field did not match and
what CSF function or CIS Control number was expected for your variant.
Re-check your scenario file and `HINTS.md`, fix the field in `answers.yaml`,
and re-run `bash autograde/run.sh`.

## 8. Troubleshooting

- **My score does not match a friend's even though our `answers.yaml` look
  similar.** This is expected. Each repository gets its own scenario
  variant (A or B). Two students on different variants have different
  correct CIS Control numbers and a different correct CIA answer - copying
  a classmate's file will actively hurt your score if they are on the other
  variant. Always confirm your variant with `starter/which-scenario.sh`.
- **`answers.yaml missing or empty at repo root` even though I filled it
  in.** You likely edited `starter/answers-template.yaml` instead of a copy
  at the repo root, or saved the file with a different name/extension (some
  editors add `.txt`). Confirm the file is named exactly `answers.yaml` and
  sits next to `README.md`, run `ls` (or `dir` on Windows) to check.
- **A field I filled in still shows as wrong.** Open `answers.yaml` in a
  plain text editor and check for typos, extra words, or a trailing comment
  stuck onto the same line as a quoted value (see the formatting rule in
  Step 6.5). The grader looks for your answer word or number inside the
  field's value, so stray extra text can still cause a mismatch if it
  changes what is on that line.
- **`bash: command not found` on Windows.** Make sure you are using **Git
  Bash**, not the plain Windows Command Prompt or PowerShell, for every
  command in this guide.
- **I do not know which CSF function or CIS Control fits an event.** Do not
  guess randomly - work through `HINTS.md` tier by tier (nudge, then
  guided, then near-solution) before asking your instructor or TA.
