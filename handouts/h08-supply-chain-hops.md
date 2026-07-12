# Handout H08: Supply-Chain Threat Mapping Hop Cards

**CSEC 2300 Foundations of Cyber Security | Dr. Gonzalo D Parra**
**Used with Lecture 8: Supply Chain & Branch Protection | In-Class Activity: Supply-chain threat mapping (groups of 3)**

## Instructions

1. Your group is assigned ONE hop of the software supply chain: **Source**, **Build**, **Registry**, or **Consumer**. Read only your card below.
2. **Attack (about 3 minutes).** For your hop, list **two realistic attacks** against it.
3. **Defend (about 2 minutes).** For each attack, name **one control** that addresses it and tag the control **preventive** or **detective**.
4. **Report (60 seconds per group).** Present your hop, your attacks, and your controls. The instructor fills gaps and marks which controls already exist in the class capstone stack.

**The chain:** Maintainer writes code -> Source repo -> Build system -> Registry -> Your install (consumer). Every hop is an attack surface.

---

## Card 1: SOURCE (the repository and its maintainers)

**Scenario.** Your team depends on an open-source library maintained by two volunteers. Anyone can propose changes; the maintainers merge them. The code that everyone downstream trusts starts here.

- How would an attacker get malicious code INTO this hop?
- How would you defend it? One control per attack, tagged preventive or detective.

## Card 2: BUILD (the CI system that turns source into artifacts)

**Scenario.** A CI pipeline checks out the source, pulls build tools and dependencies, compiles, and signs the output. Whatever the build produces is what ships, whether or not it matches the source.

- How would an attacker make the build EMIT something the source does not contain?
- How would you defend it? One control per attack, tagged preventive or detective.

## Card 3: REGISTRY (where packages and images are published and fetched)

**Scenario.** Built artifacts are published to a public registry (npm, PyPI, Docker Hub). Millions of installs pull from it by name and version. Names are cheap and anyone can publish.

- How would an attacker get a malicious artifact SERVED from this hop?
- How would you defend it? One control per attack, tagged preventive or detective.

## Card 4: CONSUMER (your project's install and update process)

**Scenario.** Your project runs `pip install` and `docker pull` in CI on every build. Dependency versions are not pinned; whatever is "latest" at build time is what ships to your users.

- How would an attacker exploit YOUR side of the chain, even if every upstream hop behaves?
- How would you defend it? One control per attack, tagged preventive or detective.

---

*(The instructor keeps the answer key in a separate copy.)*
