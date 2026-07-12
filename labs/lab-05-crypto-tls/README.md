# Lab 5: Cryptography & TLS

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 100 min  ·  **Autograding:** hash verify + openssl key/cert checks

## Objective
Compute cryptographic hashes, generate an asymmetric keypair, create a
self-signed X.509 certificate with `openssl`, and serve HTTPS from a container.

**Why it matters:** hashing, keys, and TLS are the mechanics of confidentiality,
integrity, and identity (CO3).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO3 - Access control, identity, cryptography | Generate keys, issue a cert, terminate TLS |
| CO6 - Security+ readiness | Domain 1.0 Cryptographic solutions (PKI, certificates, hashing) |

**Security+ SY0-701 domain:** 1.0 General Security Concepts (cryptographic solutions, PKI).

## Prerequisites
- `openssl` installed (standard on macOS/Linux and the lab machines).

## Per-student hash inputs
Your three hash inputs are personalized to your repository (anti-copy). First run:
```
bash starter/show-inputs.sh
```
Then hash **your** three strings. A classmate's digests will not match yours.

## Tasks
1. Run `starter/show-inputs.sh`, compute the **SHA-256** hex digests of your three inputs, and record them in `answers.yaml`.
2. Generate a keypair: `key.pem` (RSA >= 2048 or ed25519).
3. Create a self-signed certificate `cert.pem` for that key (matching public key).
4. (Optional, Tier C) Serve HTTPS with your cert on port 8443; the grader checks the served cert fingerprint equals your committed `cert.pem`.

## Deliverables
- `answers.yaml` with `sha256_1/2/3` filled (from your personalized inputs).
- `key.pem` (private key) and `cert.pem` (self-signed certificate) at the repo root.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh` (and `--syscheck` first).
**Do not** commit real production keys - these are throwaway lab keys.

## Grading
| Criterion | Points |
|-----------|-------:|
| `answers.yaml` sha256_1 correct (your input) | 10 |
| `answers.yaml` sha256_2 correct (your input) | 10 |
| `answers.yaml` sha256_3 correct (your input) | 10 |
| `key.pem` is a private key | 12 |
| `cert.pem` is a certificate | 12 |
| Certificate is self-signed & valid (openssl) | 14 |
| key.pem/cert.pem public keys correspond | 12 |
| Key strength adequate (RSA>=2048 / ed25519) | 10 |
| TLS handshake + served cert == committed cert | 10 |
| **Total** | **100** |

*openssl and TLS-handshake criteria degrade to "skipped (environment unavailable)" without openssl / a
running server; the self-signed, correspondence, and handshake checks depend on a valid `cert.pem`
(shown as "blocked by cert_is_cert" if it is missing).*
