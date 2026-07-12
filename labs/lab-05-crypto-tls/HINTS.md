# Lab 5 - Hints (three tiers)

## Task group A - Hashing
- **Tier 1 (nudge):** SHA-256 is a one-way fixed-length fingerprint. https://en.wikipedia.org/wiki/SHA-2
- **Tier 2 (guided):** `sha256sum` (Linux) or `shasum -a 256` (macOS) or `openssl dgst -sha256`. Hash the exact bytes of each line (no trailing newline differences).
- **Tier 3 (near-solution):**
  ```
  printf '%s' "the-input-string" | shasum -a 256
  ```

## Task group B - Keys & certificates
- **Tier 1 (nudge):** A self-signed cert binds a public key to an identity you vouch for yourself. https://www.openssl.org/docs/manmaster/man1/openssl-req.html
- **Tier 2 (guided):** Generate `key.pem` then a `req -x509` cert in one command, or split key generation and signing.
- **Tier 3 (near-solution):**
  ```
  openssl req -x509 -newkey rsa:2048 -nodes \
    -keyout key.pem -out cert.pem -days 365 \
    -subj "/CN=____"
  ```

## Task group C - Serve HTTPS
- **Tier 1 (nudge):** Terminate TLS at the edge of the container. https://docs.docker.com/
- **Tier 2 (guided):** Mount `cert.pem`/`key.pem` into an nginx/openssl container and expose 8443.
- **Tier 3 (near-solution):**
  ```
  openssl s_server -accept 8443 -cert cert.pem -key key.pem -www
  # verify:  openssl s_client -connect localhost:8443 </dev/null
  ```
