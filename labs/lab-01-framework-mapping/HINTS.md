# Lab 1 - Hints (three tiers)

## Task group A - NIST CSF functions
- **Tier 1 (nudge):** The five functions form a lifecycle from knowing your assets to bouncing back. Read the CSF 2.0 overview: https://www.nist.gov/cyberframework
- **Tier 2 (guided):** Match verbs - inventorying assets = **Identify**; MFA/patching = **Protect**; SIEM alert = **Detect**; isolating a host = **Respond**; restoring backups = **Recover**.
- **Tier 3 (near-solution):** A SIEM alarm firing on anomalous logins is `Detect`. Pulling the infected laptop off the network is `Respond`. Restoring files from last night's backup is `______`.

## Task group B - CIS Controls v8
- **Tier 1 (nudge):** CIS Controls are numbered 1–18. Browse the list: https://www.cisecurity.org/controls/cis-controls-list
- **Tier 2 (guided):** Access Control Management is Control **6**; Email and Web Browser Protections is Control **9**; Data Recovery is Control **11**; Audit Log Management is Control **8**.
- **Tier 3 (near-solution):** Enforcing MFA on VPN belongs to CIS Control `___` (Access Control Management). Answer with just the number.

## Task group C - CIA impact & YAML format
- **Tier 1 (nudge):** Ransomware encrypts files in place - which leg of the CIA triad does that hit first? https://csrc.nist.gov/glossary/term/cia_triad
- **Tier 2 (guided):** Use plain `key: value` lines. Answer CIA with one word: confidentiality, integrity, or availability.
- **Tier 3 (near-solution):**
  ```
  ransomware_primary_impact: ____________   # one of: confidentiality / integrity / availability
  ```
