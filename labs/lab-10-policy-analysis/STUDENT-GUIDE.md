# Lab 10 Student Guide - Privacy & Compliance Policy Analysis

Course: CSEC 2300 Foundations of Cyber Security, Dr. Gonzalo D Parra

## 1. What you will build

You will write `analysis.md`, a structured privacy and compliance review of
the local AI stack you built in Labs 7-9 (Ollama, Open WebUI, and the agent
layer). You will catalogue every piece of data the stack touches, then check
that handling against two real regulations: GDPR (the EU's General Data
Protection Regulation) and FERPA (the Family Educational Rights and Privacy
Act, the US law that protects student education records). This is a writing
and analysis lab: no Docker, no containers to run. You just need a text
editor, git, and Python 3 to grade your own work.

## 2. Before you start

- Prerequisites: Labs 7-9 completed (you are analyzing that stack, so it
  helps to remember what Ollama, Open WebUI, and the agent actually store).
- The authoritative task list and grading rubric live in `README.md` in this
  folder. This guide only explains the mechanics of doing the work; README.md
  is the assignment.
- If you get stuck on wording or structure, open `HINTS.md`. It has three
  tiers per task group (nudge, guided, near-solution) so you can get just
  enough help without spoiling your own analysis.
- Accept the assignment through the repository invitation posted on
  Canvas, then clone your repository the same way you did for earlier labs:

```
git clone <your-repo-url>
cd <your-repo-folder>
```

## 3. Step 1 - Run the system check first

Before writing anything, confirm your environment can run the grader:

```
bash autograde/run.sh --syscheck
```

> what you'll see:
> ```
> System check (pre-flight) for <your-repo-folder>
> ------------------------------------------------------------------------
> STATUS CHECK                                    FIX HINT
> PASS   python3 available
> PASS   starter files intact
> ------------------------------------------------------------------------
> All preflight checks passed - you can start the lab.
> ```

See `guide-assets/lab-10-syscheck.png` for a real passing run.

**If `python3 available` fails**: install Python 3 (Windows: from
python.org, check "Add to PATH" during setup; Mac: `brew install python3`).

**If `starter files intact` fails**: you deleted or renamed
`starter/analysis-template.md`. Re-clone the repo or restore that file from
your repository's initial commit before continuing.

## 4. Step 2 - Copy the starter template

```
cp starter/analysis-template.md analysis.md
```

(Windows PowerShell: `copy starter\analysis-template.md analysis.md`)

Open `analysis.md` in your editor. It already has the five required
headings: `## Data Inventory`, `## GDPR Analysis`, `## FERPA Analysis`,
`## Risks`, `## Recommendations`. Do not rename or remove any of these
headings, and do not change the `##` level. The grader looks for these exact
section names, so if you retitle a section (for example "Privacy Risks"
instead of "Risks") that section will score zero even if the content is
good.

## 5. Step 3 - Build the Data Inventory table

This is the section students get stuck on most, so here is exactly how the
grader checks it and how to build it correctly.

**What the grader wants**: a markdown table with at least 4 data rows (not
counting the header row), where every row has all 4 columns filled in with
real content: no `TODO`, no blank cells, no `____`, no `...`.

**The four columns, explained**:
- **Component**: the piece of the stack that handles the data (Ollama, Open
  WebUI, the agent/retrieval layer, the grading pipeline, model files, etc).
- **Data Category**: what kind of data it is (chat prompts, account emails,
  uploaded documents, session tokens, logs, model weights).
- **Storage Location**: where it physically lives (a Docker volume, a local
  file, a database inside a container, a GitHub repository).
- **Lawful Basis**: which legal justification applies under GDPR Article 6
  (consent, contract, legitimate interest, legal obligation) or, for
  education records, the FERPA school-official exception.

**One worked example row** (do not copy this verbatim; think through the
other components of your own stack the same way):

| Component | Data Category | Storage Location | Lawful Basis |
|-----------|---------------|-------------------|--------------|
| Ollama runtime | Chat prompts and model responses | Local Docker volume on the workstation disk | Legitimate interest (GDPR Article 6(1)(f)) for course instruction |

Walk through the rest of the stack the same way: what does Open WebUI store
(accounts, chat history, uploads)? What does the agent/retrieval layer log?
What does the autograder or your GitHub assignment repository keep about you? You need at
least 4 rows total (the worked example above only counts as one), and every
cell has to be a real answer, not a placeholder.

> what you'll see if a row is incomplete: the grader's feedback for
> `table_complete` will report a lower row count than you expect, for
> example `"data-inventory table has 2 complete rows; need >=4..."` even
> though you see more rows on screen. That almost always means one of your
> "rows" is still the header, or a cell in that row is blank or still says
> `TODO`.

## 6. Step 4 - Write the GDPR and FERPA sections

**Citations requirement**: the grader scans your whole document for
specific regulation citations and needs at least 2, matching patterns like
`GDPR Article 6`, `Article 30`, `34 CFR § 99`, `Recital 26`. A vague
sentence like "GDPR requires consent" does not count; you must name an
actual article or section number. HINTS.md tier 2 for task group C lists
the concepts to anchor each citation to (lawful basis, data minimization,
data-subject rights for GDPR; education records and consent for FERPA).

For GDPR, work through: what lawful basis applies to each component in your
inventory (Article 6)? Does the stack minimize what it keeps (Article 5)?
Could a student exercise their access or erasure rights (Articles 15-17)?

For FERPA, work through: which of your inventoried items counts as an
education record (34 CFR § 99.3)? Who is allowed to see it under the school
official exception (§ 99.31)? What would count as an improper disclosure?

Aim for real analysis, several paragraphs per section, not just a citation
dropped into one sentence. The whole document needs to be at least 600
words combined across all sections, so thin one-line sections will not
reach the length bar even if every section heading is present.

## 7. Step 5 - Risks and Recommendations

The grader looks for at least 3 risk/mitigation pairs: it counts how many
times the word "risk" and the word "mitigat..." (mitigation, mitigate)
appear in your document and needs both counts at 3 or higher, with the
lower of the two treated as your pair count.

The cleanest way to satisfy this and produce genuinely useful analysis is
one risk per numbered item, each with an explicit `Risk:` and `Mitigation:`
line, for example:

```
1. Risk: <what could go wrong, and which data/component is exposed>.
   Mitigation: <the concrete fix, not just "be careful">.
```

Write at least 3 of these (more is fine and stronger). Then use the
Recommendations section to turn each mitigation into an action item, ideally
referencing back to which risk it addresses. Tie at least a couple of your
risks or recommendations back to the specific article citations from your
GDPR/FERPA sections so the whole document reads as one connected analysis
instead of three disconnected lists.

## 8. Step 6 - Clean up placeholders

Before you validate, search your file for anything you have not replaced:
`TODO`, `<your`, `_____`, `placeholder`, or `lorem ipsum`. Any of these
remaining anywhere in `analysis.md` zeroes out the "no placeholder" check,
even if the rest of the document is complete. Do a find-in-editor pass for
the word `TODO` specifically since the starter template uses it as every
blank marker.

## 9. Final step - Validate and capture your proof

Run the full grader from your repo root:

```
bash autograde/run.sh
```

This prints a JSON report with one entry per rubric criterion, a `total`
score, and two codes at the bottom: `WORK-FP` (a fingerprint of your
submitted file) and `ATTEST` (your attestation code). **Screenshot this
output** (the whole terminal window, including the JSON and both hash
lines) - this is what you submit as your proof of completion, alongside
your pushed `analysis.md`.

See `guide-assets/lab-10-completion.png` for what a complete, 100/100 run
looks like, including the `WORK-FP` and `ATTEST` lines in red at the bottom.

Read the per-criterion feedback for anything below its max points; each
entry tells you exactly what is missing (a section name, a row count, a
citation count, a word count). Fix that specific thing and re-run
`bash autograde/run.sh` again - it is safe to run as many times as you like.

Finally, commit and push:

```
git add analysis.md
git commit -m "Complete Lab 10 policy analysis"
git push
```

## 10. Troubleshooting

- **Section shows 0 points even though I wrote it**: check the exact
  heading text and level. It must be `## Data Inventory`, `## GDPR
  Analysis` (or any heading starting with GDPR), `## FERPA Analysis`,
  `## Risks`, `## Recommendations` - one `#`-count is fine as long as it
  starts with one or more `#` followed by that keyword.
- **Table says fewer rows than I see on screen**: a row is only counted if
  it is not the header/separator row and all of its first 4 cells have
  content with no `TODO`, `____`, or `...`. Double check you did not leave
  a half-finished row, and that your separator row (`|---|---|---|---|`)
  is not being miscounted (it never is, but a row with only dashes and no
  real header words might be misread as a data row - keep the header row
  exactly as the template has it).
- **Citations count is below 2 even though I mentioned GDPR and FERPA
  several times**: naming the law is not enough; you need a specific
  article or section number in the text, like "Article 6" or "34 CFR §
  99.31", not just the word "GDPR" or "FERPA" by itself.
- **Word count is short**: run a word count on the file locally (most
  editors show this in the status bar) before you validate; 600 words is
  not a lot for 5 sections, but a few one-sentence sections will not clear
  it.
- **`bash: command not found` on Windows**: run these commands inside Git
  Bash (installed with Git for Windows) or WSL, not the plain Command
  Prompt or PowerShell.
