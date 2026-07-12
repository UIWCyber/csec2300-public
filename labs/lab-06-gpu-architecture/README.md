# Lab 6: GPU & Computer Architecture

**Course:** CSEC 2300-01 Foundations of Cyber Security (UIW) - Dr. Gonzalo D Parra
**Points:** 100  ·  **Estimated time:** 75 min  ·  **Autograding:** structured-answer grader with tolerance

## Objective
Inspect the machine's GPU/CPU, capture a hardware report, and answer structured
questions on the memory hierarchy, TPM, and secure boot. You submit
`answers.yaml` and a `gpu-report.txt`.

**Why it matters:** hardware roots of trust (TPM, secure boot) and the
performance hierarchy underpin how we secure and accelerate systems (CO1).

## Course-Outcome Mapping
| Outcome | Evidence |
|---------|----------|
| CO1 - Basic concepts of information systems security | Hardware roots of trust, secure boot, memory hierarchy |
| CO6 - Security+ readiness | Domain 3.0 Security Architecture (TPM, secure/measured boot, HSM) |

**Security+ SY0-701 domain:** 3.0 Security Architecture (hardware root of trust, TPM, secure boot).

## Prerequisites
- Access to a machine with a GPU (lab machines) or any workstation for the CPU path.

## Tasks
1. Run `nvidia-smi` (lab machines) or `system_profiler SPDisplaysDataType` / `lscpu` and save output to `gpu-report.txt`.
2. Answer the questions in `answers.yaml` about the memory hierarchy, GPU vs CPU, TPM, and secure boot.

## Deliverables
- `gpu-report.txt` - captured hardware output.
- `answers.yaml` - all fields filled.

## Submission
Push to your repository. Run locally with `bash autograde/run.sh`.

## Grading
| Criterion | Points |
|-----------|-------:|
| `gpu-report.txt` present | 10 |
| Report shows real GPU/CPU output | 10 |
| Fastest memory tier answer | 10 |
| Slowest tier answer | 10 |
| GPU parallelism reason | 10 |
| CPU strength (latency/serial) | 10 |
| TPM purpose | 10 |
| Secure boot purpose | 10 |
| VRAM meaning | 10 |
| Memory hierarchy ordering | 10 |
| **Total** | **100** |
