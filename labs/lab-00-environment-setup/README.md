# Lab 0: Environment & Identity Setup

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 90 min  ·  **Autograding:** GitHub Actions + local `autograde/run.sh`

## Objective
Stand up the toolchain and professional identity you will use all semester: a
configured `git`, an SSH key registered with GitHub, a working GitHub account,
and a Docker + GPU smoke test. You will capture proof in a `setup-report.md`
and a captured command-output file.

**Why it matters:** every later lab is delivered as a private GitHub repository and
graded by automation. A security professional (CO5) works from a trusted,
identifiable, reproducible workstation - this lab builds yours.

## Course-Outcome Mapping
| Outcome | Evidence in this lab |
|---------|----------------------|
| CO5 - Activities a security specialist performs | Configure identity, keys, and container/GPU tooling |
| CO6 - Security+ SY0-701 readiness | Practices in Domain 4.0 (Security Operations): secure configuration, identity |

**Security+ SY0-701 domain:** 4.0 Security Operations (secure baseline, identity & access).

## Prerequisites
- A computer with `git`, `ssh`, Docker, and Python 3 installed (lab GPU machines qualify). On Windows, install Python 3 from the Microsoft Store so the `python3` command exists in Git Bash.
- A GitHub account (create one at https://github.com/join if needed - do this yourself; the grader never asks for a password).

## Tasks
1. **Identity** - set `git config --global user.name` and `user.email`, then record them in `setup-report.md`.
2. **SSH key** - generate an ed25519 key (`ssh-keygen -t ed25519`), add the public key to GitHub, and paste your public key fingerprint into the report.
3. **GitHub account** - record your GitHub username and profile URL.
4. **Docker smoke test** - run `docker --version` and `docker run --rm hello-world`; capture output.
5. **GPU smoke test** - run `nvidia-smi` (lab machines) or `system_profiler SPDisplaysDataType` / `sysctl -n machdep.cpu.brand_string` (Mac); capture output.
6. **Capture** - save the combined command output to `env-check.txt` and summarize in `setup-report.md` under the required headings.

## Deliverables
- `setup-report.md` with headings: **Identity**, **SSH**, **GitHub**, **Docker**, **GPU** (all filled, no placeholders).
- `env-check.txt` - captured output of the smoke-test commands.

## How to do this lab (step by step)

The Student Guide on the course site walks every step below with the exact
output you should see:
https://uiwcyber.github.io/csec2300-public/#labs%2Flab-00-environment-setup%2FSTUDENT-GUIDE.md.
The short version follows.

**Step 1. Open a terminal.** Windows: Git Bash (Start menu, type `Git Bash`).
Mac: Terminal. A new terminal starts in your home folder. `pwd` prints the
folder you are in, `ls` lists it, `cd name` enters a folder, and `cd` alone
returns home.

**Step 2. Identity and key**, from any folder:

```
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
ssh-keygen -t ed25519 -C "you@example.com"
cat ~/.ssh/id_ed25519.pub
```

Paste that public key into GitHub (avatar, Settings, SSH and GPG keys, New
SSH key), then confirm with `ssh -T git@github.com`.

**Step 3. Clone into your home folder**, then enter the lab folder. Replace
`yourusername` with your GitHub username:

```
cd
git clone git@github.com:UIWCyber/csec2300-lab00-yourusername.git
cd csec2300-lab00-yourusername
```

**Every command below runs inside this folder.** If `pwd` does not end in
`csec2300-lab00-yourusername`, run `cd ~/csec2300-lab00-yourusername`.

**Step 4. System check:** `bash autograde/run.sh --syscheck` until every line
is `PASS`.

**Step 5. Smoke test:** `bash scripts/smoke-test.sh` writes `env-check.txt`.
Read it with `cat env-check.txt`; do not edit it.

**Step 6. Fill in the report.** Windows: `notepad setup-report.md`. Mac:
`open -e setup-report.md`. Keep the five headings, remove every placeholder
(`_____`, `TODO`, and the angle-bracket sample answers), and write at least
150 words.

**Step 7. Push. The grader runs by itself.**

```
git add setup-report.md env-check.txt
git commit -m "Complete Lab 0 environment setup"
git pull
git push
```

Open your repository at `https://github.com/UIWCyber/csec2300-lab00-yourusername`.
Both files are there, and a yellow dot appears next to your commit while the
grader runs. It turns into a green check or a red X in about a minute. Click
it, then click Details, to read your score line by line. Fix what it names,
push again, and repeat until the score is 100.

**Step 8. Grade it yourself first, if you want** (this needs Python on your
machine and is never required): `bash autograde/run.sh` prints the same SCORE
panel locally.

## Submission
Push `setup-report.md` and `env-check.txt` to your assignment repository before
the deadline. That is the whole submission: nothing is uploaded to Canvas.

The grader runs on every push and shows you the score on the commit, so you can
correct your work as many times as you like before the deadline. The grade of
record is the same grader run against your repository after the deadline.

## Grading
| Criterion | Points |
|-----------|-------:|
| `setup-report.md` present | 5 |
| Git identity (name + email) recorded | 10 |
| SSH key / fingerprint present | 10 |
| GitHub username / profile recorded | 10 |
| `env-check.txt` capture present | 10 |
| Docker smoke output present | 10 |
| GPU / CPU smoke output present | 10 |
| Required report sections present | 15 |
| No leftover placeholders | 10 |
| Report meets minimum length (150 words) | 10 |
| **Total** | **100** |
