# Handout H13: Cert Autopsy Worksheet

**CSEC 2300 Foundations of Cyber Security | Dr. Gonzalo D Parra**
**Used with Lecture 13: PKI, TLS & Certificates | In-Class Activity: Cert Autopsy**

## Instructions

1. On your own laptop or phone, open **three HTTPS sites you use daily** and view each site's certificate (steps below).
2. For each site, fill one row of the worksheet: subject, issuer organization, days until expiry, number of SANs, and chain length.
3. **Pair up and compare.** Same issuer? A small number of CAs (Let's Encrypt, DigiCert) dominate; be ready to discuss CA market concentration as a systemic risk.
4. Find the **strangest SAN** among your three sites. Two students will report theirs; the class discusses why one certificate carries many names.

## How to View a Certificate

**Chrome (desktop):** click the icon to the left of the address bar (tune/lock icon) -> **Connection is secure** -> **Certificate is valid**. A viewer opens with General and Details tabs. SANs are in Details under "Subject Alternative Name". The chain appears at the top of the viewer.

**Firefox (desktop):** click the padlock in the address bar -> **Connection secure** -> **More information** -> **View Certificate**. A full-page viewer opens with one tab per certificate in the chain; SANs are listed under "Subject Alt Names".

**Counting tips**

- **Days until expiry:** subtract today from the "Valid To / Expires On" date; a rough count is fine.
- **Number of SANs:** count every DNS name listed under Subject Alternative Name (wildcards like `*.example.com` count as one).
- **Chain length:** count the certificates from the site's own (leaf) up to and including the root the viewer shows. Most public sites show 2 or 3.

## Worksheet

| | Site (URL) | Subject (CN) | Issuer organization | Days until expiry | Number of SANs | Chain length |
|---|-----------|--------------|--------------------|-------------------|----------------|--------------|
| Ex. | `www.example.com` (illustrative) | `www.example.com` | DigiCert Inc | 143 | 2 (`www.example.com`, `example.com`) | 3 (leaf -> intermediate -> root) |
| 1 | | | | | | |
| 2 | | | | | | |
| 3 | | | | | | |

**Pair-compare notes:** issuers in common: ______________  strangest SAN found: ______________

---

*(The instructor keeps the answer key in a separate copy.)*
