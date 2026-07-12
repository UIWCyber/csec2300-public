# Handout H11: Design the Segments

**CSEC 2300 Foundations of Cyber Security | Dr. Gonzalo D Parra**
**Used with Lecture 11: Container Networking, Segmentation & Secrets | In-Class Activity: Design the segments**

## Instructions

1. **Pairs (6 minutes).** Read the scenario and requirements. Design the network segmentation: which Docker networks exist, which service joins which network, and which SINGLE port is published to the host.
2. **Compare with a neighbor pair.** Any service that can reach something it does not need to reach is a **finding**. Hunt for findings in each other's designs.
3. **Debrief.** Compare with the canonical answer. This design mirrors the Lab 4 bonus task.

**Design rule:** "can reach" should equal "needs to reach". Two containers can talk if and only if they share at least one network. Publishing a port exposes a container to the host and the outside world.

## The Scenario: Five Services

| Service | Role |
|---------|------|
| `proxy` | Reverse proxy; the only front door, terminates outside connections |
| `webapp` | Public web application served to users through the proxy |
| `api` | Internal API; business logic; the only service that queries the database |
| `db` | Database; holds all persistent data |
| `admin` | Admin dashboard; staff-only interface, also served through the proxy |

## Communication Requirements (who MUST talk to whom)

- The outside world reaches ONLY the reverse proxy, on one published port (443).
- `proxy` must reach `webapp` and `admin` (it forwards user and staff traffic to them).
- `webapp` must reach `api` (all app data flows through the API).
- `admin` must reach `api` (staff actions also go through the API).
- `api` must reach `db` (the only service allowed to touch data).
- Nothing else needs to talk to anything else. In particular: `webapp` and `admin` must NOT reach `db` directly, and `proxy` must NOT reach `api` or `db`.

## Your Design

Networks you will create (name them):

1. ______________________  2. ______________________  3. ______________________ (use fewer or more if you can justify it)

Membership grid: mark X where a service joins a network. Then circle the ONE published port.

| Service | Network 1: ________ | Network 2: ________ | Network 3: ________ | Published port? |
|---------|--------------------|--------------------|--------------------|-----------------|
| proxy   |                    |                    |                    |                 |
| webapp  |                    |                    |                    |                 |
| api     |                    |                    |                    |                 |
| db      |                    |                    |                    |                 |
| admin   |                    |                    |                    |                 |

Self-check before comparing: for every pair of services that share a network, ask "does the requirements list say they NEED to talk?" If not, that is a finding in your own design.

---

*(The instructor keeps the answer key in a separate copy.)*
