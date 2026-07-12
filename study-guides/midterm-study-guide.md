# CSEC 2300 Midterm Study Guide

**Course:** CSEC 2300 Foundations of Cyber Security (UIW)
**Instructor:** Dr. Gonzalo D Parra
**Coverage:** Modules M1 through M5 (sessions 1 through 14, Labs 0 through 5)

The midterm has 40 questions, 8 per module. This guide tells you exactly what to know for each module: the terms you must define cold, the processes you must be able to walk through step by step, the commands you must be able to read, and self-check questions to test yourself. Answers to the self-checks are at the end. If you can answer every self-check without peeking, you are ready.

**How to study:** work module by module. First, cover the definitions column and quiz yourself on the terms. Second, write out each process from memory. Third, redo the relevant lab tasks (your graded repo is your best study artifact). Fourth, do the self-checks.

---

## Module 1: InfoSec Foundations (Lectures 1-3, Lab 1)

### Terms to define cold

- **Confidentiality:** only authorized parties can read the data.
- **Integrity:** data is accurate and has not been altered without authorization.
- **Availability:** systems and data are usable when legitimate users need them.
- **Authentication:** proving an identity is who it claims to be.
- **Authorization:** deciding what an authenticated identity is allowed to do.
- **Accounting (auditing):** recording who did what and when, so actions trace back to identities.
- **Non-repudiation:** a party cannot plausibly deny an action they performed.
- **Threat actor:** a person or group that poses a threat; know the motivations of nation-states, organized crime, hacktivists, insiders, and script kiddies.
- **Control:** a safeguard; know both the categories (technical, managerial, operational, physical) and the functional types (preventive, detective, corrective, deterrent, directive, compensating).
- **Compensating control:** an alternative safeguard used when the intended primary safeguard cannot be applied.
- **Defense in depth:** stacking multiple unrelated safeguards so that one failing control never leaves an asset unprotected.
- **NIST Cybersecurity Framework (CSF):** the six functions: Govern, Identify, Protect, Detect, Respond, Recover, and what each one covers.
- **GRC:** governance (direction and accountability), risk (identify and treat), compliance (meet external obligations).

### Processes to walk through

1. **Classify any scenario against the CIA triad:** identify the asset, identify what property was harmed (read, altered, or made unavailable), name the triad element.
2. **Classify any control twice:** first by category (who or what implements it), then by function (what it does relative to an incident: before, during, or after).
3. **Map an incident to NIST CSF functions:** which function was weak, which function is acting now, which function comes next.

### Self-checks (answers at the end)

- **M1.1** A hospital's patient portal is knocked offline for a day by a flood of junk traffic. Separately, an employee emails a spreadsheet of diagnoses to a personal account. Name the CIA element violated in each case.
- **M1.2** A "You are being recorded" sign, a locked server-room door, and a nightly backup job: give the functional control type of each.
- **M1.3** A vendor cannot patch a medical device, so the clinic puts it behind a dedicated firewall segment. What control type is the segmentation, and why does that label apply?
- **M1.4** A former employee leaks internal documents to embarrass the company over a layoff. Which threat actor category fits best, and what is the actor's motivation?
- **M1.5** Your team writes the plan for who calls whom when an alert fires. Which NIST CSF function does that planning belong to?

---

## Module 2: Git and GitHub (Lectures 4-6, Labs 0 and 2)

### Terms to define cold

- **Repository:** the project plus its full history, stored in the `.git` directory.
- **Commit:** a recorded snapshot of the staged changes, with author, timestamp, and message.
- **Staging area (index):** the holding zone between your working files and a commit.
- **Branch:** a movable pointer to a line of development.
- **Merge conflict:** Git cannot automatically combine two edits that touch the same region of a file, so a person must choose the result.
- **Pull request (PR):** a proposal to merge one branch into another, with review before merge.
- **Signed commit:** a commit bound to a cryptographic identity, so authorship can be verified.
- **Audit trail:** the property that history records who changed what and when; `git log` is how you read it.
- **Secrets hygiene:** never commit credentials; a secret committed once lives on in history even after you delete the file.

### Processes to walk through

1. **The add-commit flow:** edit files in the working directory, `git add` to stage the changes you want, `git commit` to record the staged snapshot with a message. Know what state each step changes.
2. **The GitHub collaboration workflow, in order:** branch first, then commit your work and push it, then open the pull request; a reviewer examines the diff, and the branch merges into main after approval.
3. **Resolving a merge conflict:** attempt the merge, Git marks the conflicting regions, edit the file to keep the correct content, stage the resolved file, complete the merge with a commit.
4. **What to do when a secret lands in a repo:** treat the credential as burned, revoke and rotate it immediately, then clean history; deleting the file in a new commit is not enough.

### Commands to read (program, option, argument)

You must be able to read a command line and say what each part is and does.

- `git add report.md` - program `git`, subcommand `add`, argument is the file being staged.
- `git commit -m "fix typo"` - `-m` is an option taking the message as its argument.
- `git log --oneline` - `--oneline` is an option changing the output format; no argument.
- `git checkout -b feature/login` - `-b` creates the named branch and switches to it.
- `git push origin main` - arguments are the remote name and the branch name.
- `git clone <url>` - argument is the repository URL to copy locally.

### Self-checks (answers at the end)

- **M2.1** A teammate runs `git commit` and is confused that a file they edited was not included. What step did they skip, and what does that step do?
- **M2.2** You removed an API key from `config.py` and committed the deletion. A week later the key is abused. Explain how the attacker likely got it and what you should have done.
- **M2.3** Put these in the correct order: open PR, merge, push branch, create branch, review.
- **M2.4** Your team requires verified signatures on all commits to main. What attack does this requirement make harder?
- **M2.5** In `git commit -m "add tests"`, identify the program, the subcommand, the option, and the option's argument.

---

## Module 3: DevSecOps and CI/CD (Lectures 6-8, Lab 3)

### Terms to define cold

- **Scrum roles and events:** sprint, sprint planning, daily stand-up (sync on progress, plans, blockers), sprint review (demo the increment), sprint retrospective (improve the process).
- **CI/CD:** continuous integration builds and tests every change; continuous delivery/deployment ships it automatically.
- **Pipeline security gate:** an automated check that fails the run and blocks the merge when it finds a problem.
- **SAST:** static inspection of source code; nothing executes.
- **DAST:** probing the live, deployed app from outside, the way an attacker would.
- **Dependency (SCA) scanning:** checking third-party packages for known CVEs.
- **Secret scanning:** detecting credentials committed to the repo or exposed in workflows.
- **Action pinning:** referencing third-party pipeline code by immutable commit SHA instead of a floating tag.
- **SBOM:** a machine-readable list of every component and library your software is built from.
- **Software supply chain:** everything you depend on but did not write: packages, base images, actions, registries.
- **Branch protection:** rules that force review and passing checks before merge to a protected branch.

### Processes to walk through

1. **A PR through a security-gated pipeline:** push triggers the workflow, it builds, runs tests, runs SAST, scans dependencies and secrets; any failing gate blocks the merge until fixed.
2. **Responding to a vulnerable-dependency disclosure:** consult your SBOM or dependency scan to find which apps include the library, upgrade or mitigate, rebuild, redeploy. This is the Log4Shell lesson: inventory speed determines response speed.
3. **Where CI credentials live:** in the CI platform's secret vault, handed to jobs only at run time, never written into the workflow file or the repo.

### Commands and syntax to read

- Recognize the parts of a GitHub Actions workflow: `on:` (trigger), `jobs:`, `steps:`, `uses: owner/action@<sha>` (a pinned third-party action), `secrets.NAME` (injected credential).
- `pip install requests` versus `pip install requests==2.31.0` - unpinned versus pinned dependency, and why pinning matters.

### Self-checks (answers at the end)

- **M3.1** Your dependency scanner flags a critical CVE in a library your app imports. In a DevSecOps pipeline, what should happen to the PR that introduced it, and why is "log it and merge anyway" wrong?
- **M3.2** SAST and DAST both missed a bug that a reviewer caught by reading the diff. What does that tell you about the relationship between automated scanning and human review?
- **M3.3** A workflow file references `some-org/build-tool@main`. Rewrite the reference the safer way and explain what risk the change removes.
- **M3.4** Which Scrum event is for improving how the team works, and how is it different from the sprint review?
- **M3.5** Why is an SBOM more useful on the day a new library vulnerability is announced than a penetration test report from last quarter?

---

## Module 4: Docker and Containers (Lectures 9-11, Lab 4)

### Terms to define cold

- **Image:** a read-only, layered template containing an app and its dependencies.
- **Container:** a running (or runnable) instance created from an image.
- **Namespaces:** kernel feature that isolates what a process can see (processes, network, filesystem, users).
- **cgroups (control groups):** kernel feature that limits what resources a process can consume.
- **Container vs. VM:** every container rides on the host's kernel (lighter, but a weaker boundary); each VM runs its own kernel under a hypervisor (heavier, stronger boundary).
- **Dockerfile:** the recipe that builds an image, instruction by instruction.
- **Non-root container:** the app runs as an unprivileged user (`USER` instruction), so a compromise does not start with root.
- **Docker socket:** the daemon's control endpoint at `/var/run/docker.sock`; whoever controls it controls the Docker daemon, which is effectively root on the host. Never mount it into a container casually.
- **Image scanning:** checking image contents for known CVEs.
- **Network segmentation:** placing containers on separate networks so only intended paths exist; expose only the public tier.
- **Immutable infrastructure:** you do not patch running containers; you rebuild the image and replace them.

### Processes to walk through

1. **Image-to-container lifecycle:** write a Dockerfile, `docker build` produces an image, the image is tagged and optionally pushed to a registry, `docker run` creates a container from it; to update, edit the Dockerfile or base, rebuild, redeploy, and remove the old containers.
2. **Remediating CVEs found in an image:** update the base image or package versions in the Dockerfile, rebuild, rescan, redeploy. Hand-patching a running container is the wrong answer.
3. **Hardening a Dockerfile:** start from a minimal base, pin base and package versions, add a non-root `USER`, copy only what the app needs, never bake secrets into `ENV` or layers.
4. **Segmenting a three-tier app:** only the web tier faces the public network; the API and database live on internal-only networks, and the database accepts connections solely from the API.

### Commands to read (program, option, argument)

- `docker build -t myapp:1.0 .` - `-t` names and tags the image; the `.` argument is the build context.
- `docker run -d -p 8080:80 --name web myapp:1.0` - `-d` detached, `-p host:container` publishes a port, `--name` labels the container, final argument is the image.
- `docker ps -a` - list containers; `-a` includes stopped ones.
- `docker images` / `docker pull nginx:1.25` - list local images; pull a pinned tag from a registry.
- `USER appuser` in a Dockerfile - subsequent instructions and the running app use this unprivileged account.

### Self-checks (answers at the end)

- **M4.1** In one sentence each: what do namespaces isolate, and what do cgroups limit?
- **M4.2** A teammate proposes `docker run -v /var/run/docker.sock:/var/run/docker.sock ...` so their monitoring container can "see everything." What is the risk?
- **M4.3** Your image scan shows fixable critical CVEs in the base image. Describe the correct remediation path in three steps.
- **M4.4** In `docker run -p 5000:80 myapi:2.1`, which side of `5000:80` is the host port, and what does the final argument name?
- **M4.5** Why does a kernel exploit threaten every container on a host but not every VM on a hypervisor?

---

## Module 5: Cryptography and IAM (Lectures 12-14, Lab 5)

### Terms to define cold

- **Symmetric encryption:** one shared key encrypts and decrypts; fast, but the key must be exchanged securely.
- **Asymmetric encryption:** a key pair; what one key locks only the other unlocks; removes the key-exchange problem and enables signatures, at the cost of speed.
- **Hash function:** one-way fixed-length fingerprint of data; any change to the input changes the hash.
- **Salt:** random value added before hashing a password so identical passwords produce different hashes and precomputed tables fail.
- **Digital signature:** hash of the message encrypted with the sender's private key; verifying with the public key proves origin and integrity.
- **Certificate:** a CA-signed binding between an identity and a public key, valid for a limited window.
- **Certificate authority (CA) and chain of trust:** root CA signs intermediates, intermediates sign server (leaf) certificates; your browser walks the chain.
- **TLS:** the protocol securing traffic in transit; uses asymmetric crypto to establish a shared symmetric session key.
- **Hybrid encryption:** asymmetric for key exchange, symmetric for bulk data; how TLS actually works.
- **MFA:** factors from different categories: something you know, have, or are; two of the same category is not MFA.
- **Access control models:** DAC (owner decides), MAC (system-enforced labels), RBAC (permissions via roles), ABAC (policy over attributes).
- **Least privilege:** grant only the access needed to do the job.

### Processes to walk through

1. **Hybrid encryption (the TLS idea):** client and server use certificates and asymmetric crypto to authenticate and agree on a session key, then all application data flows under fast symmetric encryption with that key.
2. **Verifying a download with a published hash:** compute the hash of your copy and compare it to the vendor's published value; a match shows your copy is byte-identical to what the vendor hashed, but it says nothing about whether that file is benign, and without a signature it cannot prove who published it.
3. **Creating and verifying a digital signature:** sender hashes the message, encrypts the hash with their private key; receiver decrypts with the sender's public key and compares against a fresh hash of the message.
4. **Certificate validation in the browser:** check the signature chain up to a trusted root, check the validity window, check the name matches the site, check revocation.

### Commands to read

- `sha256sum ubuntu.iso` - compute a file's SHA-256 fingerprint (you did the equivalent in Lab 5).
- `openssl genrsa -out key.pem 2048` - generate a private key; `-out` names the output file; final argument is the key size.
- `openssl req -new -x509 -key key.pem -out cert.pem` - create a self-signed certificate from a key.
- `openssl s_client -connect example.com:443` - open a TLS connection and show the certificate chain.

### Self-checks (answers at the end)

- **M5.1** Why do real systems encrypt bulk traffic symmetrically even though asymmetric crypto exists? What does each half of the hybrid contribute?
- **M5.2** A login database stores salted hashes. An attacker steals the whole table. What can they NOT do directly, and what does the salt specifically defeat?
- **M5.3** You verify a signature on a message using your colleague's public key and it checks out. State the two properties you have established.
- **M5.4** A site's certificate is valid, unexpired, and chains to a trusted root, but the name on it does not match the domain you typed. Should the browser trust it? Why?
- **M5.5** A system requires a password plus a code from a hardware token. A second system requires a password plus a security question. Which one is MFA, and why?

---

## Exam-day logistics

- **Format:** 40 questions, each worth one point: mostly multiple choice, plus a few true/false and two multiple-answer ("select all that apply") items. On multiple-answer items, read every option; partial patterns from the stem are not enough.
- **Coverage:** 8 questions per module, M1 through M5, drawn from lecture, labs, and quizzes 1 through 5.
- **Delivery:** taken in class on Canvas during the exam window posted on Canvas. Bring your laptop charged and your Canvas login working before exam day.
- **Policy:** per the course policy, no late or makeup exams; a missed exam is a zero. For a documented emergency, contact Dr. Gonzalo D Parra before the exam window.
- **Best preparation:** your quiz results (quizzes 1 through 5 preview the style), your lab repos, and the self-checks above.

---

## Self-check answers

**M1.1** The junk-traffic outage attacks availability; the emailed diagnoses violate confidentiality.
**M1.2** Sign: deterrent. Locked door: preventive (and physical by category). Nightly backup: corrective (it enables recovery after damage).
**M1.3** A compensating control: it substitutes alternative protection because patching, the intended control, cannot be applied here.
**M1.4** Malicious insider; motivation is revenge or grievance, and insiders are dangerous because they start with legitimate access and knowledge.
**M1.5** Respond (planning response communications and roles); the exercise of preparing plans in advance also touches Govern and Identify, but the plan itself belongs to Respond.

**M2.1** They skipped `git add`. Commits record only what is staged; `git add` moves changes from the working directory into the staging area.
**M2.2** The key is still in the repository history; anyone with clone access can check out the earlier commit. You should have revoked and rotated the key immediately and treated it as compromised, then cleaned history.
**M2.3** Create branch, push branch, open PR, review, merge.
**M2.4** Forged authorship: an attacker impersonating a trusted developer's commits. Signatures bind each commit to a verified cryptographic identity.
**M2.5** Program: `git`. Subcommand: `commit`. Option: `-m`. Option's argument: the message string `"add tests"`.

**M3.1** The gate should fail and the merge should be blocked until the dependency is fixed or replaced. Logging and merging defeats the purpose of a gate: the vulnerability ships to the protected branch and inherits all downstream trust.
**M3.2** Scanners match known patterns; humans catch logic flaws, malicious intent, and design errors. Automated scanning and human review are complementary layers, not substitutes.
**M3.3** Pin to a full commit SHA, for example `some-org/build-tool@<40-hex-sha>`. This removes the risk that a compromised or malicious update to the action is silently pulled into your pipeline.
**M3.4** The retrospective improves the team's process; the review demonstrates the completed increment for stakeholders. Retrospective is about how you work, review is about what you built.
**M3.5** The SBOM tells you today, immediately, whether the newly announced vulnerable component is inside your software and where. A pen test report is a snapshot of past findings and says nothing about a component disclosed after it was written.

**M4.1** Namespaces isolate what a process can see (its view of processes, network, filesystem, users); cgroups limit what it can consume (CPU, memory, IO).
**M4.2** Whoever controls the socket controls the Docker daemon: the container could start a privileged container and take over the host. It is effectively granting root on the host.
**M4.3** Update the base image (or the affected package versions) in the Dockerfile; rebuild and rescan the image; redeploy new containers and retire the old ones. Never patch running containers in place.
**M4.4** `5000` is the host port, `80` is the container port; the final argument `myapi:2.1` names the image (and tag) the container is created from.
**M4.5** All containers on a host share that host's kernel, so one kernel exploit reaches them all. Each VM has its own guest kernel behind the hypervisor, so the same exploit is confined to one VM.

**M5.1** Symmetric is fast enough for bulk data but cannot solve key distribution alone; asymmetric handles key distribution and authentication but is slow. The hybrid uses asymmetric to establish a shared session key, then symmetric for everything after.
**M5.2** They cannot reverse the hashes to recover the passwords, because hashing is one-way. The salt defeats precomputed (rainbow) tables and makes identical passwords hash differently, forcing per-account cracking.
**M5.3** Authenticity: the message was produced by the holder of that private key. Integrity: it has not been altered since signing. Together these support non-repudiation.
**M5.4** No. The certificate binds a key to a specific name; a name mismatch means the CA never vouched for this site under that name, which is exactly the pattern of an impersonation or man-in-the-middle attempt.
**M5.5** The first: password (know) plus hardware token (have) are different factor categories. Password plus security question is two of the same category (both something you know), so it is not MFA.
