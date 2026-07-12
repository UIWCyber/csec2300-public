# Handout H14: Midterm Review Rapid Rounds

**Course:** CSEC 2300 Foundations of Cyber Security · Dr. Gonzalo D Parra
**Used in:** Lecture 14 (IAM + Midterm Review), In-Class Activity
**Format:** Twenty timed questions, one at a time on the projector (or loaded into any quiz tool).
Students answer solo on phones or laptops; thirty-second explanation after each question.
Four questions per module, Modules 1 through 5.

## Round 1: Module 1 - InfoSec Foundations

1. Ransomware encrypts a hospital's patient records so staff cannot open them. Which CIA property is MOST directly violated?
   a) Confidentiality  b) Integrity  c) Availability  d) Non-repudiation
2. Proving who you are vs. what you are allowed to do: which pair is correct?
   a) Authorization / Authentication  b) Authentication / Authorization  c) Accounting / Authentication  d) Authentication / Accounting
3. A warning banner on a login screen is best classified as which control function?
   a) Preventive  b) Corrective  c) Deterrent  d) Compensating
4. Which NIST CSF function does an incident-response runbook primarily support?
   a) Identify  b) Protect  c) Detect  d) Respond

## Round 2: Module 2 - Git and Collaborative Security

5. Which Git area holds changes after `git add` but before `git commit`?
   a) Working directory  b) Staging area  c) Remote  d) Stash
6. Every Git commit ID is a hash of its content AND its parent commit. What security property does that chain give the history?
   a) Confidentiality  b) Availability  c) Tamper evidence (integrity)  d) Least privilege
7. A signed commit provides which security concept?
   a) Availability  b) Non-repudiation  c) Segmentation  d) Obfuscation
8. You accidentally committed an API key and then deleted the file in a new commit. Is the key gone?
   a) Yes, deleted  b) No, it remains in history; rotate the key  c) Only if you push  d) Only on GitHub

## Round 3: Module 3 - CI/CD and DevSecOps

9. "Shift left" means:
   a) Move security checks earlier in development  b) Move servers to the cloud  c) Deploy faster  d) Reduce logging
10. Which scan type analyzes source code WITHOUT running it?
    a) DAST  b) SAST  c) Fuzzing  d) Pen test
11. A dependency with a known CVE is flagged by which scan?
    a) Secret scanning  b) SCA (software composition analysis)  c) DAST  d) Linting
12. Branch protection that requires a passing CI run before merge is which control function?
    a) Detective  b) Corrective  c) Preventive  d) Deterrent

## Round 4: Module 4 - Docker and Containers

13. Image vs. container:
    a) Same thing  b) Image is the running instance  c) Image is the template; container is the running instance  d) Container is the template
14. Containers isolate processes using which kernel features?
    a) Hypervisor and firmware  b) Namespaces and cgroups  c) TPM and secure boot  d) VLANs and ACLs
15. Which Dockerfile line most reduces blast radius if the app is compromised?
    a) `FROM ubuntu:latest`  b) `USER appuser`  c) `ENV API_KEY=...`  d) `EXPOSE 80`
16. Why is `FROM ubuntu:latest` a supply-chain risk?
    a) Ubuntu is insecure  b) The tag moves, so builds are not reproducible or reviewable  c) It is too small  d) It blocks HEALTHCHECK

## Round 5: Module 5 - Cryptography and IAM

17. Hybrid encryption (like TLS) uses asymmetric crypto to:
    a) Encrypt all the data  b) Exchange the symmetric session key  c) Hash passwords  d) Compress traffic
18. A password plus a PIN is:
    a) Two-factor authentication  b) One factor used twice (both are something you know)  c) Biometric MFA  d) Passwordless
19. Access decided by rules over user and resource attributes (department, time of day, data label) is:
    a) DAC  b) MAC  c) RBAC  d) ABAC
20. What does a digital certificate bind together?
    a) A password and a username  b) A public key and an identity, vouched by a CA  c) Two symmetric keys  d) A hash and a salt

*(The instructor keeps the answer key in a separate copy.)*
