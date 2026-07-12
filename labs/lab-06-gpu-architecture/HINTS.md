# Lab 6 - Hints (three tiers)

## Task group A - Capture hardware
- **Tier 1 (nudge):** Read what the tools report, do not guess specs. https://developer.nvidia.com/nvidia-system-management-interface
- **Tier 2 (guided):** `nvidia-smi > gpu-report.txt` on GPU machines; else `system_profiler SPDisplaysDataType > gpu-report.txt` or `lscpu >> gpu-report.txt`.
- **Tier 3 (near-solution):**
  ```
  { nvidia-smi || system_profiler SPDisplaysDataType; lscpu 2>/dev/null; } > gpu-report.txt
  ```

## Task group B - Memory hierarchy & GPU vs CPU
- **Tier 1 (nudge):** Speed and size trade off across registers, cache, RAM, disk. GPUs win on throughput, CPUs on latency. https://en.wikipedia.org/wiki/Memory_hierarchy
- **Tier 2 (guided):** Fastest = registers; slowest of {registers, cache, RAM, SSD} = SSD/disk. GPUs use thousands of cores for parallel throughput; CPUs excel at low-latency serial work.
- **Tier 3 (near-solution):** `fastest_memory: registers`, `slowest_memory: ____`, order registers > cache > ram > disk.

## Task group C - TPM & secure boot
- **Tier 1 (nudge):** These are hardware roots of trust. https://learn.microsoft.com/windows/security/hardware-security/tpm/trusted-platform-module-overview
- **Tier 2 (guided):** A TPM stores keys and takes measurements for attestation; secure boot verifies bootloader/firmware signatures before running them.
- **Tier 3 (near-solution):** `tpm_purpose: stores keys / attestation`, `secure_boot_purpose: verifies signed bootloader/firmware`.
