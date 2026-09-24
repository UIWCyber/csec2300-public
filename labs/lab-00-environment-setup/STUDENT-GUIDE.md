# Lab 0 Student Guide: Environment and Identity Setup

## What you will build

You will turn your laptop or lab workstation into a working, identifiable
development machine: git configured with your name and email, an SSH key
registered with GitHub, and a Docker install that can pull and run a
container. You will prove it worked with two files: `setup-report.md` and
`env-check.txt`. Every lab for the rest of the semester assumes this
baseline is in place, so getting it right now saves you time later.

This guide assumes you have never used a terminal. Every step shows the
command to type and the output you should see. Type the commands yourself
rather than pasting whole blocks; you learn the shape of each one that way.

## Before you start

- **Tools.** You need a computer with `git`, `ssh` and Docker installed. The campus GPU lab workstations already have all of them (they run Windows with Docker Desktop and an NVIDIA GPU). On your own laptop, install [Git](https://git-scm.com/downloads) and [Docker Desktop](https://www.docker.com/products/docker-desktop/) first; `ssh` ships with Windows 10/11, macOS, and Linux already.
- **Python 3, only if you want to grade yourself.** The grader runs on GitHub after every push, so you do not need Python to finish this lab. For the optional local run in Step 9, Windows users install Python 3 from the Microsoft Store and Mac users already have it.
- **A GitHub account.** If you do not have one, create it yourself at https://github.com/join. Choose a professional username; you will show this account to employers. The grader never asks for your password; do not type your GitHub password into any script or terminal.
- **Where the rules are.** The graded assignment, the repository invitation, and the exact point values live in the **Lab 0** assignment on Canvas and in your repository's `README.md`. This guide walks you through the mechanics; README.md and HINTS.md are the authoritative source for what is graded. If you get stuck, open `HINTS.md` in your repository for a three-tier hint ladder before asking the instructor.

## Step 0: Open a terminal and find your way around

Every command in this lab is typed into a terminal.

- **Windows:** open the Start menu, type `Git Bash`, and open it. Git Bash installs with Git for Windows. Do not use PowerShell or Command Prompt for this lab: the grader is a bash script and only runs in Git Bash.
- **Mac:** press Command+Space, type `Terminal`, and press Return.

You now have a window with a blinking cursor waiting for a command. Three
commands tell you where you are and move you around.

**`pwd`** prints the folder you are standing in ("print working directory"):

```
pwd
```

> what you'll see on Windows: `/c/Users/yourname`. On a Mac: `/Users/yourname`. This is your **home folder**. A new terminal always starts here. If `pwd` prints something else, type `cd` on its own and press Enter; that returns you home from anywhere.

**`ls`** lists what is inside the current folder:

```
ls
```

> what you'll see: the folders you know from the desktop, such as `Desktop  Documents  Downloads  Pictures`, one name per column.

**`cd`** changes into a folder ("change directory"). Try it, then come back:

```
cd Desktop
pwd
cd ..
pwd
```

> what you'll see: `/c/Users/yourname/Desktop` (or `/Users/yourname/Desktop`) after the first `pwd`, and your home folder again after `cd ..`. Two dots mean "the folder above this one".

Three habits that save time: the Tab key completes a folder or file name
after you type its first letters; the Up arrow brings back the previous
command; `clear` wipes the screen. Windows users: the Windows path
`C:\Users\yourname` is written `/c/Users/yourname` inside Git Bash. They
are the same folder.

## Step 1: Set your git identity

Git stamps every commit with a name and email. Set both globally so every
repository on your machine uses them. Type each line and press Enter:

```
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

Use the email address attached to your GitHub account so later
criteria can cross-check it. Confirm it stuck:

```
git config --global user.name
git config --global user.email
```

> what you'll see: your name on one line, your email on the next. If either line is blank, the `git config --global` command above did not run, or you mistyped it.

## Step 2: Generate an SSH key and add it to GitHub

An SSH key lets your computer prove who it is to GitHub without a
password. Once the key is registered, cloning and pushing need nothing
else. Ed25519 is the modern, recommended key type.

**1. Generate the key.** Press Enter at the "Enter file in which to save
the key" prompt to accept the default location. At the passphrase prompt
you may press Enter for no passphrase on your own laptop; on a shared
workstation, type a passphrase (git will ask for it on every push).

```
ssh-keygen -t ed25519 -C "you@example.com"
```

> what you'll see: `Your identification has been saved in /c/Users/yourname/.ssh/id_ed25519` (Mac: `/Users/yourname/.ssh/id_ed25519`), then `Your public key has been saved in ...id_ed25519.pub`, a fingerprint line, and a box of random characters called the randomart.

**2. Print the fingerprint** you will paste into your report:

```
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```

> what you'll see: a line like `256 SHA256:7Kq2mXo0Vb9cP4hZ1sTf6yLwR8nDgU3jE5aH0iCkQ2M you@example.com (ED25519)`

**3. Print the public key** and copy the whole line. It starts with
`ssh-ed25519` and ends with your email. Select it with the mouse; in Git
Bash, selecting text copies it, and in Terminal press Command+C.

```
cat ~/.ssh/id_ed25519.pub
```

The file that ends in `.pub` is the **public** key and is safe to share.
The file without `.pub` is your **private** key. Never copy, paste, or
upload the private key anywhere.

**4. Register it on GitHub.** In your browser: click your avatar (top
right), then Settings, then SSH and GPG keys, then New SSH key. Paste the
public key into the Key box, give it a title such as `Lab 0 laptop`, and
click Add SSH key.

**5. Test the connection:**

```
ssh -T git@github.com
```

> what you'll see the first time: `The authenticity of host 'github.com' can't be established ... Are you sure you want to continue connecting (yes/no/[fingerprint])?` Type `yes` and press Enter. Then: `Hi yourusername! You've successfully authenticated, but GitHub does not provide shell access.` That message is success, not an error.

If you see `Permission denied (publickey)` instead, the key on GitHub does
not match the key on this computer. Repeat items 3 and 4, pasting the
whole line from `cat ~/.ssh/id_ed25519.pub`.

## Step 3: Accept the invitation and clone your repository

**1. Accept the invitation.** Your instructor created a private repository
for you named `UIWCyber/csec2300-lab00-yourusername`, where `yourusername`
is your GitHub username in lower case. GitHub emailed you an invitation to
it. Open that email and click View invitation, then Accept invitation. You
can also open the repository address posted on Canvas in your browser; it
shows the same Accept button. Sign in with your own GitHub account.

**2. Clone it into your home folder.** Replace `yourusername` with your
GitHub username:

```
cd
git clone git@github.com:UIWCyber/csec2300-lab00-yourusername.git
```

> what you'll see:

```
Cloning into 'csec2300-lab00-yourusername'...
remote: Enumerating objects: 14, done.
...
Receiving objects: 100% (14/14), done.
```

This works with no password because of the SSH key from Step 2. If it
fails with `Permission denied (publickey)`, go back to Step 2. If it fails
with `Repository not found`, you have not accepted the invitation yet, or
the username in the address is misspelled.

**3. Move into the new folder** and confirm you are in the right place:

```
cd csec2300-lab00-yourusername
pwd
ls
```

> what you'll see: `pwd` ends in `csec2300-lab00-yourusername`, and `ls` prints `HINTS.md  README.md  autograde  scripts  setup-report.md`.

**Every command from here to the end of this guide runs inside this
folder.** Before each step, glance at `pwd`. If it does not end in
`csec2300-lab00-yourusername`, type:

```
cd ~/csec2300-lab00-yourusername
```

The `~` is a shortcut for your home folder, so this command works from
anywhere. If you close the terminal and come back later, do this first.

## Step 4: Run the system check

Before doing any work, ask the grader whether your machine is ready.
This does not grade your submission; it only checks that the tools you
need are installed and reachable. Run it from the lab folder:

```
bash autograde/run.sh --syscheck
```

> what you'll see:

```
System check (pre-flight) for csec2300-lab00-yourusername
------------------------------------------------------------------------
STATUS CHECK                                    FIX HINT
PASS   python3 available
PASS   git identity configured
PASS   git installed
PASS   docker installed
PASS   starter files intact
------------------------------------------------------------------------
All preflight checks passed - you can start the lab.
```

A copy of a clean syscheck run is saved at
`guide-assets/lab-00-syscheck.png` so you know what "all green" looks
like.

If instead you see `bash: autograde/run.sh: No such file or directory`,
you are not inside the lab folder. Run `cd ~/csec2300-lab00-yourusername`
and try again.

If you see a `FAIL` line, fix only that item and re-run the same command:

- **`python3 available` FAILS.** Install Python 3 as described under "Before you start", open a new terminal window, and try again.
- **`git identity configured` FAILS.** Step 1 did not stick. Repeat it.
- **`git installed` or `docker installed` FAILS.** The tool is missing or not on your PATH. Reinstall it, open a new terminal window, and try again. On Windows, make sure you are in Git Bash, opened after the install finished.
- **`starter files intact` FAILS.** `setup-report.md` or `scripts/smoke-test.sh` was deleted or renamed. Restore it with `git checkout -- setup-report.md` (or the script's path).

Do not move on until this table is all `PASS`.

## Step 5: Run the Docker and GPU/CPU smoke test

Docker Desktop must be running before this step. Open the Docker Desktop
application and wait until the whale icon in the system tray (Windows) or
menu bar (Mac) stops animating. On the lab workstations it is already
running.

This lab ships a script that captures everything the grader looks for in
one shot: `scripts/smoke-test.sh`. Run it from the lab folder:

```
bash scripts/smoke-test.sh
```

The script prints its output on screen and writes the same text to
`env-check.txt` in the lab folder. That file is the one the grader reads.

> what you'll see on a Mac laptop (a workstation shows an `NVIDIA-SMI` table under `== gpu ==` instead of the Apple lines):

```
== git ==
git version 2.45.2
Alex Cardinal
alex.cardinal@example.com
== ssh key ==
256 SHA256:7Kq2mXo0Vb9cP4hZ1sTf6yLwR8nDgU3jE5aH0iCkQ2M alex.cardinal@example.com (ED25519)
== docker ==
Docker version 28.3.2, build 578ccf6

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
...
== gpu ==
Graphics/Displays:

    Apple M4 Pro:

      Chipset Model: Apple M4 Pro
      Type: GPU
...
```

If the Docker lines are missing or the script stops with an error:

- **`docker: command not found`.** Docker is not installed or not on PATH. Install Docker Desktop and open a new terminal window.
- **`Cannot connect to the Docker daemon`.** Docker is installed but not running. Open the Docker Desktop application, wait for the whale icon, then re-run the script.
- **`no ed25519 key yet` under `== ssh key ==`.** Step 2 was skipped. Do it, then re-run the script.
- **On a lab machine, `nvidia-smi` prints nothing or errors.** The script falls back to a CPU summary on its own. Nothing to do.
- **On a Windows laptop with no NVIDIA graphics card**, the `== gpu ==` section stays empty, because the fallback commands are Mac commands. Add one line of CPU information yourself, from the lab folder, with the command below. It is the only case where you add to `env-check.txt` by hand.

```
echo "cpu: $(powershell -NoProfile -Command "(Get-CimInstance Win32_Processor).Name")" >> env-check.txt
```

> what you'll see: nothing on screen. The command appends a line such as `cpu: 12th Gen Intel(R) Core(TM) i7-1255U` to the end of the file.

Now look at the file. `cat` prints a file to the screen:

```
cat env-check.txt
```

You can also open it in an editor to read it (Windows:
`notepad env-check.txt`, Mac: `open -e env-check.txt`), but do not type
into it. Confirm it contains the Docker version line, the "Hello from
Docker!" message, and a GPU or CPU line. If any of the three is missing,
fix the cause above and re-run the script. A captured command is stronger
evidence than typed-in text, so the grader expects the script's output.

## Step 6: Fill in setup-report.md

`setup-report.md` is a plain text file written in Markdown. The lines that
start with `##` are headings; the grader looks for five of them by exact
name. Open the file in an editor, from the lab folder.

**Windows:**

```
notepad setup-report.md
```

Notepad opens the file. Edit, press Ctrl+S to save, and close Notepad. If
Notepad offers to change the encoding or the file type, keep the defaults:
the file must stay `setup-report.md`, not `setup-report.md.txt`.

**Mac:**

```
open -e setup-report.md
```

TextEdit opens the file as plain text. Edit, press Command+S to save, and
close TextEdit.

**Either system, if you installed VS Code:**

```
code setup-report.md
```

Fill in every section, following these rules:

- **Keep the five headings** exactly as they are: `## Identity`, `## SSH`, `## GitHub`, `## Docker`, `## GPU`. The `## Reflection` heading is where most of your words go.
- **Delete every placeholder marker:** the underscores `_____`, the word `TODO`, and the sample answers wrapped in angle brackets. A leftover marker anywhere in the file costs points even if the rest of the section is correct.
- **Write at least 150 words** in the whole file. One-line answers do not get there; write two or three sentences under Docker, GPU, and Reflection.
- **Paste the `SHA256:` fingerprint** from Step 2, never the private key.

Here is a complete example of a finished report. Alex Cardinal is
invented; every value in your file must be your own.

```
# Setup Report - Lab 0

## Identity
Name: Alex Cardinal
Email: alex.cardinal@example.com

## SSH
Fingerprint: SHA256:7Kq2mXo0Vb9cP4hZ1sTf6yLwR8nDgU3jE5aH0iCkQ2M
Generated with ssh-keygen -t ed25519 and registered on GitHub under the
title "Lab 0 laptop". The ssh -T test greeted me by username.

## GitHub
Username: alexcardinal-uiw
Profile: https://github.com/alexcardinal-uiw

## Docker
docker --version printed Docker version 28.3.2, build 578ccf6. The
hello-world container ran and printed "Hello from Docker!" followed by the
four steps Docker took to run it. The first run pulled the image from
Docker Hub, which took a few seconds on campus wifi.

## GPU
My laptop is a MacBook Pro with an Apple M4 Pro chip, so nvidia-smi is not
available. The system_profiler command reported Chipset Model: Apple M4
Pro with 20 GPU cores and Metal 3 support. On the lab workstation the same
script prints the NVIDIA-SMI table instead.

## Reflection
I did this lab on my own laptop from the Terminal app. Setting the git
identity and generating the key went smoothly. The first clone failed with
Permission denied (publickey) because I had pasted only half of the public
key into GitHub; pasting the whole line from cat ~/.ssh/id_ed25519.pub
fixed it. Docker Desktop had to be started before the smoke test would
run, and the grader told me my report was under 150 words until I wrote
this section. Everything is now in my home folder under
csec2300-lab00-alexcardinal-uiw.
```

After saving, print the file to check that your edits are really in it:

```
cat setup-report.md
```

## Step 7: Commit and push. The grader runs by itself.

Your two files exist only on your computer until you push them. Pushing is
how you hand the lab in: there is nothing to upload to Canvas.

**1. See what changed:**

```
git status
```

> what you'll see: `modified:   setup-report.md` under "Changes not staged for commit", and `env-check.txt` under "Untracked files".

**2. Stage both files, then commit them** with a message:

```
git add setup-report.md env-check.txt
git commit -m "Complete Lab 0 environment setup"
```

> what you'll see: `[main 3f2a9c1] Complete Lab 0 environment setup` and `2 files changed`. The seven characters after `main` are your commit id and will differ.

**3. Bring down anything your instructor changed, then push:**

```
git pull
git push
```

> what you'll see from `git pull`: either `Already up to date.` or a short merge summary. Then from `git push`: several `Writing objects` lines, and the two lines below. No password is asked, because of the SSH key.

```
To github.com:UIWCyber/csec2300-lab00-yourusername.git
   a1b2c3d..3f2a9c1  main -> main
```

## Step 8: Read your score on GitHub

Open `https://github.com/UIWCyber/csec2300-lab00-yourusername` in your
browser. Both `setup-report.md` and `env-check.txt` are listed, and next to
your commit message there is a small **yellow dot**: the grader is running.
It takes about a minute.

- A **green check** means the grader finished. Click it, then click **Details**, to see your score.
- A **red X** means the grader finished and something is missing. Click it the same way to find out what.

Either way the page you land on lists every criterion with its points and a
`feedback` line saying exactly what the grader looked for and whether it
found it. Fix what it names, save, then commit and push again exactly as in
Step 7. The grader runs again on every push, and you may push as many times
as you like before the deadline. The last score before the deadline is your
grade.

> what a finished report looks like:

```
Autograde: 100/100 points

- [OK] report_exists - 5/5: setup-report.md present
- [OK] git_identity - 10/10: name and email recorded
- [OK] ssh_key - 10/10: key fingerprint present
- [OK] github_user - 10/10: username and profile recorded
- [OK] smoke_file - 10/10: env-check.txt capture present
- [OK] docker_smoke - 10/10: docker output found
- [OK] gpu_smoke - 10/10: GPU or CPU output found
- [OK] sections - 15/15: found 5/5 required headings
- [OK] no_placeholder - 10/10: no placeholders left
- [OK] wordcount - 10/10: report meets the minimum length
```

## Step 9: Run the grader yourself, if you want to

This step is optional and needs Python 3 on your own machine. It tells you
the score before you push instead of after. From the lab folder:

```
bash autograde/run.sh
```

It prints the same criteria, then a panel with your score and two
verification codes: `WORK-FP`, a fingerprint of your files, and `ATTEST`, a
code tying that fingerprint to your repository. An example of the finished
panel is saved at `guide-assets/lab-00-completion.png`.

Nothing about this step is submitted. The score that counts is the one on
GitHub, from the files you pushed.

## Troubleshooting

- **I closed the terminal and every command fails with "No such file".** A new terminal starts in your home folder. Run `cd ~/csec2300-lab00-yourusername` first.
- **`git push` asks for a username and password.** Your repository was cloned with an HTTPS address, not SSH. Switch it to SSH once with the command below, then push again. If you must stay on HTTPS, Windows opens a "Connect to GitHub" window; choose "Sign in with your browser". On a Mac, GitHub no longer accepts your account password here; use the SSH switch instead.

```
git remote set-url origin git@github.com:UIWCyber/csec2300-lab00-yourusername.git
git push
```

- **My `git_identity` criterion is 0 even though I set my name/email.** The grader reads the email out of `setup-report.md`, not out of your git config directly. Make sure the exact email you typed after `Email:` under `## Identity` is a real address (`name@domain.tld` shape) and matches what you used in Step 1.
- **My `ssh_key` criterion is 0.** The grader looks for a real `ssh-ed25519 AAAA...` public key line or a `SHA256:` fingerprint of at least 20 characters in `setup-report.md`. Paste the actual output of `ssh-keygen -lf ~/.ssh/id_ed25519.pub`, not the literal text `SHA256:_____` left over from the template.
- **My `no_placeholder` criterion is 0.** Somewhere in `setup-report.md` a `_____`, a `TODO`, or an angle-bracket sample answer is still there, often in a line you thought you deleted. Open the file and search for each marker.
- **`docker run --rm hello-world` hangs or fails to pull the image.** You need an internet connection the first time, since Docker pulls the image from Docker Hub. On a restricted network, connect to a different network (or campus wifi instead of a VPN) and try again.
- **My word count is under 150 even though I filled every section.** Short one-line answers in Docker/GPU/Reflection usually do not reach 150 words on their own. Add two or three more sentences describing what you saw and any problem you solved, in your own words.
- **I do not have an NVIDIA GPU on my laptop.** That is expected on most laptops. On a Mac the script falls back to `system_profiler` and then to the CPU name on its own. On a Windows laptop, add the CPU line shown in Step 5.
- **Notepad saved my report as `setup-report.md.txt`.** Rename it back from the lab folder: `mv setup-report.md.txt setup-report.md`.
- **I did the lab on a shared workstation.** Your SSH key is stored on that machine under the account you used. When you are done, delete the key from GitHub (Settings, SSH and GPG keys, Delete) and generate a fresh one on your own computer for the next lab.
