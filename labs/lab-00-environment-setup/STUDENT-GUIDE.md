# Lab 0 Student Guide: Environment and Identity Setup

## What you will build

You will turn your laptop or lab workstation into a working, identifiable
development machine: git configured with your name and email, an SSH key
registered with GitHub, and a Docker install that can pull and run a
container. You will prove it worked with two files: `setup-report.md` and
`env-check.txt`. Every lab for the rest of the semester assumes this
baseline is in place, so getting it right now saves you time later.

## Before you start

- You need a computer with `git`, `ssh`, and Docker installed. The campus
  GPU lab workstations already have all three (they run Windows with
  Docker Desktop and an NVIDIA GPU). On your own laptop, install
  [Git](https://git-scm.com/downloads) and
  [Docker Desktop](https://www.docker.com/products/docker-desktop/) first;
  `ssh` ships with Windows 10/11, macOS, and Linux already.
- You need a GitHub account. If you do not have one, create it yourself at
  https://github.com/join. The grader never asks for your password; do not
  type your GitHub password into any script or terminal.
- The graded assignment, the repository invitation, and the exact
  point values live in the **Lab 0** assignment on Canvas and in this
  repository's `README.md`. This guide walks you through the mechanics of
  doing the work; it does not replace README.md or HINTS.md, which are the
  authoritative source for what is being graded. If you get stuck, open
  `HINTS.md` in this folder for a three-tier hint ladder before asking the
  instructor.

## Step 1: Accept and open the lab

1. Click the repository invitation posted on Canvas for Lab 0.
   Accept it with your own GitHub account. Your instructor has created a private
   repository for you named something like
   `lab-00-environment-setup-yourusername`.
2. Clone your repository to your machine. Replace the URL with the one
   GitHub shows you after you accept the invitation:
   ```
   git clone git@github.com:your-org/lab-00-environment-setup-yourusername.git
   cd lab-00-environment-setup-yourusername
   ```
   If you have not set up an SSH key yet, clone with the HTTPS URL instead
   (you will still add an SSH key as part of this lab):
   ```
   git clone https://github.com/your-org/lab-00-environment-setup-yourusername.git
   ```
3. Confirm you are in the right folder. You should see `README.md`,
   `HINTS.md`, `setup-report.md`, and an `autograde/` folder.
   ```
   ls
   ```

## Step 2: Run the system check first

Before doing any work, ask the grader whether your machine is even ready.
This does not grade your submission; it only checks that the tools you
need are installed and reachable.

```
bash autograde/run.sh --syscheck
```

> what you'll see:
> ```
> System check (pre-flight) for lab-00-environment-setup-yourusername
> ------------------------------------------------------------------------
> STATUS CHECK                                    FIX HINT
> PASS   python3 available
> PASS   git identity configured
> PASS   git installed
> PASS   docker installed
> PASS   starter files intact
> ------------------------------------------------------------------------
> All preflight checks passed - you can start the lab.
> ```

A copy of a clean syscheck run is saved at
`guide-assets/lab-00-syscheck.png` so you know what "all green" looks
like.

If you see a `FAIL` line, fix only that item and re-run the same command:

- **`git identity configured` FAILS** - you have not set your name/email
  yet. Do Step 3 below first.
- **`git installed` / `docker installed` FAILS** - the tool is missing or
  not on your PATH. Reinstall it, restart your terminal, and try again. On
  Windows, make sure you are using the terminal that Git Bash or Docker
  Desktop set up (a fresh terminal window after install usually fixes a
  stale PATH).
- **`starter files intact` FAILS** - you (or a stray script) deleted or
  renamed `setup-report.md` or `scripts/smoke-test.sh`. Restore them by
  re-cloning the repo into a new folder and copying the missing file back,
  or `git checkout -- <file>` if you have not committed over it.

Do not move on to Step 3 until this table is all `PASS`.

## Step 3: Set your git identity

Git stamps every commit with a name and email. Set both globally so every
repository on your machine uses them:

```
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

Use the email address associated with your GitHub account so later
criteria can cross-check it. Confirm it stuck:

```
git config --global user.name
git config --global user.email
```

> what you'll see: your name on one line, your email on the next. If
> either line is blank, the `git config --global` command above did not
> run, or you mistyped it.

## Step 4: Generate an SSH key and add it to GitHub

An SSH key lets you authenticate to GitHub without typing a password every
time you push. Ed25519 is the modern, recommended key type.

1. Generate the key (press Enter through the prompts to accept the
   default file location; a passphrase is optional but recommended):
   ```
   ssh-keygen -t ed25519 -C "you@example.com"
   ```
2. Print the fingerprint you will paste into your report:
   ```
   ssh-keygen -lf ~/.ssh/id_ed25519.pub
   ```
   > what you'll see: a line like
   > `256 SHA256:AbCdEf...restofthefingerprint you@example.com (ED25519)`
3. Print the public key itself and copy the whole line (starts with
   `ssh-ed25519`):
   ```
   cat ~/.ssh/id_ed25519.pub
   ```
4. On GitHub: click your avatar > **Settings** > **SSH and GPG keys** >
   **New SSH key**. Paste the public key, give it a title (for example
   "Lab 0 workstation"), and save.
5. Test the connection:
   ```
   ssh -T git@github.com
   ```
   > what you'll see: `Hi yourusername! You've successfully
   > authenticated, but GitHub does not provide shell access.` That
   > message is success, not an error.

Windows users: run these same commands from Git Bash, which installs with
Git for Windows and gives you the `ssh-keygen`/`ssh` commands used above.

## Step 5: Record your GitHub account

In `setup-report.md`, under the `## GitHub` heading, write your GitHub
username and your profile URL in the form `https://github.com/yourusername`.
This is how the grader confirms you have a real GitHub identity attached
to the submission.

## Step 6: Run the Docker and GPU/CPU smoke test

This lab ships a script that captures everything the grader looks for in
one shot: `scripts/smoke-test.sh`. Run it from the repository root:

```
bash scripts/smoke-test.sh
```

> what you'll see: the script prints git version/identity, your SSH key
> fingerprint (or "no ed25519 key yet" if you skipped Step 4), the Docker
> version followed by the "Hello from Docker!" message, and either an
> `nvidia-smi` table (GPU lab machines) or a `system_profiler`/CPU summary
> (Mac laptops without a discrete GPU). All of that output is written to
> `env-check.txt` in the same folder - that is the file the grader reads.

If the Docker lines are missing or the script stops with an error:

- **`docker: command not found`** - Docker is not installed or not on
  PATH. Install Docker Desktop and reopen your terminal.
- **`Cannot connect to the Docker daemon`** - Docker is installed but not
  running. Open the Docker Desktop application and wait for the whale
  icon in the menu bar/system tray to say it is running, then re-run the
  script.
- **On a lab machine, `nvidia-smi` prints nothing or errors** - that is
  fine; the script automatically falls back to a CPU/GPU summary command.
  You do not need to do anything extra.

Open `env-check.txt` afterward and confirm it actually contains the
Docker version line, the "Hello from Docker!" message, and a GPU or CPU
line. If any of those three are missing, re-run the script - do not hand
edit `env-check.txt`, since a captured command is stronger evidence than
typed-in text.

## Step 7: Finish setup-report.md

Open `setup-report.md` and fill in every section. Keep the exact heading
names (`## Identity`, `## SSH`, `## GitHub`, `## Docker`, `## GPU`); the
grader looks for those exact words. Delete every placeholder marker
(`_____`, `<your ...>`, `TODO`) as you fill each section in - a leftover
placeholder anywhere in the file costs you points even if the rest of the
section is correct.

- **Identity**: your name and email, matching Step 3.
- **SSH**: the `SHA256:...` fingerprint from Step 4 (not the whole private
  key - never paste a private key anywhere).
- **GitHub**: your username and profile URL from Step 5.
- **Docker**: a short written confirmation that `docker --version` and
  `docker run --rm hello-world` worked, in your own words.
- **GPU**: a short written summary of what your GPU/CPU smoke test showed.
- **Reflection**: a few sentences on your workstation and anything you had
  to troubleshoot. This section, combined with the rest of the file, needs
  to add up to at least 150 words total, so do not leave it as one line.

## Final step: Validate and capture your proof

Run the real grader (not `--syscheck` this time):

```
bash autograde/run.sh
```

This prints a JSON report with one entry per graded criterion, a `total`
out of 100, and two verification codes at the bottom: `WORK-FP` (a
fingerprint of your submitted files) and `ATTEST` (a code tying that
fingerprint to your repository and commit). Read the `feedback` field on
any criterion that is not at full points; it tells you exactly what the
grader could not find.

> what you'll see when everything is correct:
> ```
> {
>   "total": 100,
>   "max": 100,
>   ...
>   "work_fp": "9258835520f0",
>   "attest": "6cf0bfc32a8d"
> }
>
> WORK-FP  : 9258835520f0
> ATTEST   : 6cf0bfc32a8d
> ```
> An example of this finished output is saved at
> `guide-assets/lab-00-completion.png` - your codes will be different
> since they are derived from your own files and repository.

**Take a screenshot of your terminal showing this full result, including
the `WORK-FP` and `ATTEST` lines and the `total` score.** That screenshot
is what you submit as proof of completion, alongside committing and
pushing `setup-report.md` and `env-check.txt`:

```
git add setup-report.md env-check.txt
git commit -m "Complete Lab 0 environment setup"
git push
```

Pushing triggers the same grader automatically in GitHub Actions; check
the Actions tab on your repository to confirm it also reports your score.

## Troubleshooting

- **My `git_identity` criterion is 0 even though I set my name/email.**
  The grader reads the email out of `setup-report.md`, not out of your
  git config directly. Make sure the exact email you typed after `Email:`
  under `## Identity` is a real address (`name@domain.tld` shape) and
  matches what you used in Step 3.
- **My `ssh_key` criterion is 0.** The grader looks for a real
  `ssh-ed25519 AAAA...` public key line or a `SHA256:` fingerprint of at
  least 20 characters in `setup-report.md`. Paste the actual output of
  `ssh-keygen -lf ~/.ssh/id_ed25519.pub`, not the literal text
  `SHA256:_____` left over from the template.
- **`docker run --rm hello-world` hangs or fails to pull the image.** You
  need an internet connection the first time, since Docker pulls the
  image from Docker Hub. On a restricted network, connect to a different
  network (or campus wifi instead of a VPN) and try again.
- **My word count is under 150 even though I filled every section.** Short
  one-line answers in Docker/GPU/Reflection usually do not reach 150
  words on their own. Add two or three more sentences describing what you
  saw and any problem you solved, in your own words.
- **I do not have an NVIDIA GPU on my laptop.** That is expected on most
  laptops. Use the Mac fallback (`system_profiler SPDisplaysDataType`) or,
  if that also fails, `sysctl -n machdep.cpu.brand_string` for CPU info.
  The smoke-test script already tries these in order, so you usually do
  not need to run them by hand.
