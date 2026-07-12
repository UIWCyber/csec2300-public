# Lab 6 Student Guide - GPU & Computer Architecture

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra

This guide walks you through the lab step by step. It does not give you the graded
answers - it shows you how to run the tools, read their output, and where to look
up the concepts so you can answer in your own words.

## What you will build / prove

You will capture a real hardware report from a machine (GPU workstation or your own
laptop) and answer structured questions about the memory hierarchy, GPU vs CPU
design, and two hardware roots of trust (TPM and secure boot). You submit two files:
`gpu-report.txt` and `answers.yaml`. Everything is graded automatically by
`autograde/run.sh`.

## Before you start

- You do not need Docker, Ollama, or a GPU to finish this lab on your own laptop -
  the collector script automatically falls back to CPU-only tools if there is no
  NVIDIA GPU.
- The authoritative task list is `README.md` in your repo; the hint ladder (three
  tiers per task group, from a nudge to a near-solution) is in `HINTS.md`. Use
  `HINTS.md` before asking for help - try Tier 1 first, then Tier 2, then Tier 3.
- Assignment access: accept the Lab 6 invite link posted for this lab on Canvas
  (your GitHub assignment repository). That creates your private repo with this lab's files already
  in it.

## Step 1 - Accept and open the lab

1. Click the repository invitation on Canvas for Lab 6 and accept it. This
   creates your own private repository, for example
   `github.com/uiw-csec2300/lab-06-gpu-architecture-yourusername`.
2. Clone it to your machine (Terminal on Mac/Linux, Git Bash or PowerShell on
   Windows):
   ```
   git clone <your repository URL>
   cd lab-06-gpu-architecture-yourusername
   ```
3. Confirm you see `README.md`, `HINTS.md`, `autograde/`, and `starter/`.

## Step 2 - Run the system check first

Before doing any work, confirm your environment is ready:

```
bash autograde/run.sh --syscheck
```

> **What you'll see:**
> ```
> System check (pre-flight) for lab-06-gpu-architecture-yourusername
> ------------------------------------------------------------------------
> STATUS CHECK                                    FIX HINT
> PASS   python3 available
> PASS   starter files intact
> ------------------------------------------------------------------------
> All preflight checks passed - you can start the lab.
> ```

See `guide-assets/lab-06-syscheck.png` for a real passing run.

This lab's syscheck only needs Python 3 and the two starter files
(`starter/answers-template.yaml`, `starter/capture.sh`) to be present. If either
check fails:

| FAIL | Fix |
|------|-----|
| `python3 available` | Install Python 3 (macOS/Linux usually already have it; on Windows install from python.org and make sure "Add to PATH" is checked during install, then open a new terminal). |
| `starter files intact` | You deleted or renamed a starter file. Re-clone the repo, or `git checkout -- starter/` to restore it from your last commit. |

## Step 3 - Capture your hardware report

This is where the machine you are on matters.

### On a GPU workstation (lab machines, Windows with an NVIDIA card)

The collector tries `nvidia-smi` first. On these machines it succeeds and gives you
real GPU telemetry: model, driver version, VRAM, temperature, running processes.

Run the provided script from the repo root:

```
bash starter/capture.sh
```

> **What you'll see (GPU workstation):**
> ```
> +-----------------------------------------------------------------------------+
> | NVIDIA-SMI 5xx.xx       Driver Version: 5xx.xx       CUDA Version: 12.x     |
> |-------------------------------+----------------------+----------------------+
> | GPU  Name        Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
> | ...
> == CPU ==
> ...
> ```

If you are on Windows and `bash` is not available, open Git Bash (installed with
Git for Windows) and run the same command from there, or run
`nvidia-smi > gpu-report.txt` directly in PowerShell/cmd and then separately append
CPU info.

### On your own machine (no NVIDIA GPU - Mac, most laptops)

`nvidia-smi` is not installed, so the script automatically falls back to
cross-platform tools:
- macOS: `system_profiler SPDisplaysDataType` (graphics/display info) plus
  `sysctl -a | grep machdep.cpu` (CPU info, since `lscpu` is Linux-only).
- Linux without an NVIDIA card: `system_profiler` will not exist either, so the
  script falls straight to `lscpu`.

Run the same command either way:

```
bash starter/capture.sh
```

> **What you'll see (Apple Silicon Mac, no discrete GPU):**
> ```
> Graphics/Displays:
>     Apple M4 Pro:
>       Chipset Model: Apple M4 Pro
>       Type: GPU
>       Total Number of Cores: 20
>       ...
> == CPU ==
> machdep.cpu.core_count: 14
> machdep.cpu.brand_string: Apple M4 Pro
> ```

This is expected and fine - the grader's "real hardware output" check looks for
common hardware-report keywords (things like `chipset`, `vram`, `cpu`, `core`,
`nvidia`, `cuda`) and matches against whatever your machine legitimately reports.
You are not penalized for not having an NVIDIA GPU; you are graded on capturing
your *actual* hardware, whatever it is.

Either way, confirm the file was written:

```
cat gpu-report.txt
```

You should see real numbers and model names, not an empty file. If `gpu-report.txt`
is empty or missing, re-read `HINTS.md` Task group A and re-run the capture
command; do not hand-type fake hardware specs into the file.

## Step 4 - Answer the concept questions

Copy the template into place if you have not already (the grader reads
`answers.yaml` at the repo root, not the template):

```
cp starter/answers-template.yaml answers.yaml
```

Open `answers.yaml` in a text editor (VS Code, Notepad, nano - anything that saves
plain text) and fill in each field **in your own words**. The grader checks for the
underlying *concept*, not an exact phrase, so write full sentences that show you
understand the idea rather than copying a single keyword.

The fields you need to fill in, and where to study each one:

| Field | What it is asking | Where to study it |
|-------|--------------------|--------------------|
| `fastest_memory` | Which tier of the memory hierarchy has the lowest latency | `HINTS.md` Task group B; Wikipedia "Memory hierarchy" |
| `slowest_memory` | Which tier (of registers/cache/RAM/SSD) is slowest | same |
| `gpu_strength` | Why GPUs are fast for ML/graphics workloads | `HINTS.md` Task group B; think about core count and workload type |
| `cpu_strength` | What CPUs are better at than GPUs | same - think about instruction-level dependencies and branching |
| `tpm_purpose` | What a Trusted Platform Module does | `HINTS.md` Task group C; Microsoft Learn "Trusted Platform Module overview" |
| `secure_boot_purpose` | What secure boot checks before letting firmware/OS code run | same; NIST/Microsoft docs on secure boot |
| `vram_meaning` | What VRAM is and how it differs from system RAM | your `gpu-report.txt` output plus general GPU architecture reading |
| `hierarchy_order` | The full fastest-to-slowest ordering of the memory tiers | Task group B |

Study tip: read the linked material in `HINTS.md` first, then write your answer
from memory in your own sentence. If you get stuck, open the next hint tier - Tier
1 is a nudge and a link, Tier 2 names the concept, Tier 3 is close to the literal
answer. Try to stop as early in the ladder as you can; you learn the material
better that way and it is the whole point of the lab.

Save the file when you are done. All eight fields must be non-empty for full
credit on this section.

## Step 5 - Validate and capture your proof

Run the grader:

```
bash autograde/run.sh
```

> **What you'll see (partial credit example, one field still off-concept):**
> ```
> {
>   "total": 90,
>   ...
>   "criteria": [
>     ...
>     {
>       "id": "vram_meaning",
>       "max": 10,
>       "points": 0,
>       "feedback": "vram_meaning = '...'; expected one of: video, gpu memory, graphics"
>     }
>   ],
>   "work_fp": "...",
>   "attest": "..."
> }
> ```

Read the `feedback` string on any criterion showing `"points": 0` - it tells you
which field is missing the expected concept, without telling you the answer
itself. Revise that field in `answers.yaml` and re-run `bash autograde/run.sh`
until you are satisfied with your score.

When you are done, the output ends with two verification lines:

```
WORK-FP  : <12 hex characters>
ATTEST   : <12 hex characters>
```

**Take a screenshot of the full terminal output showing your score, the
per-criterion PASS/FAIL breakdown, and these two codes.** This screenshot (or the
full text output) is what you submit alongside your pushed repo as proof of your
run. An example of what a completed, full-credit run looks like is in
`guide-assets/lab-06-completion.png` (scores and hashes only - not the answer
text, since your answers should be your own words).

Finally, commit and push:

```
git add gpu-report.txt answers.yaml
git commit -m "Complete Lab 6: GPU and computer architecture"
git push
```

Pushing triggers the same grader automatically through your assignment repository
(`.github/workflows/classroom.yml`); check the Actions tab on your repo to confirm
it ran and matches your local score.

## Troubleshooting

1. **`gpu-report.txt` is empty or the "report_real" check fails.**
   Your capture command probably ran in the wrong directory, or a tool errored out
   silently. Re-run `bash starter/capture.sh` from the repo root and `cat
   gpu-report.txt` to confirm it has real text in it before moving on.

2. **On Windows, `bash` or `system_profiler`/`lscpu` are "not recognized".**
   Use Git Bash (installed with Git for Windows) to get a `bash` shell. On a
   non-GPU Windows laptop, `system_profiler` (macOS-only) and `lscpu` (Linux-only)
   will both be unavailable; that is expected. Ask in office hours or check
   `HINTS.md` Task group A for a Windows-appropriate capture command, or use the
   GPU workstation for this step instead.

3. **A concept field keeps scoring 0 even though you feel your answer is right.**
   The grader looks for specific concept keywords inside your sentence (see the
   `feedback` line it prints). Reread the relevant `HINTS.md` tier and make sure
   your sentence actually uses words like "parallel," "latency," "signed
   firmware," etc. rather than a synonym the grader was not told to look for.

4. **You are not on a GPU machine and worry you will be penalized for a
   CPU-only report.** You will not be. The grader accepts any real hardware
   report; the fallback path (`system_profiler`/`sysctl` on Mac, `lscpu` on
   Linux) is a legitimate, expected result on non-GPU machines, not an error.

5. **`answers.yaml` does not exist / grader says fields are empty.**
   You edited `starter/answers-template.yaml` instead of copying it to
   `answers.yaml` at the repo root first. Run `cp starter/answers-template.yaml
   answers.yaml`, then edit the copy.
