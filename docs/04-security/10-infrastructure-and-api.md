# Threats: infrastructure, API and supply chain (IN)

Hyve is open source; security never depends on secrecy of design.

| ID | Exploit | Severity | Mitigation |
| --- | --- | --- | --- |
| IN-01 | Injection (SQL, Cypher, command) | Blocker | Parameterized queries; validation; no shell with user data |
| IN-02 | Broken admin authorization | Blocker | Separate admin service; MFA; deny by default; audit log |
| IN-03 | Mass assignment of privileged fields | Critical | Explicit DTOs; allowlisted fields |
| IN-04 | SSRF via fetched URLs | Critical | No server-side fetching of user URLs in v0 |
| IN-05 | Outbound webhook abuse | High | None in v0; later signed, rate-limited, verified domains |
| IN-06 | XSS in spectator UI | High | Escape all output; strict CSP; code as text |
| IN-07 | Dependency compromise in Hyve's own stack | High | Lockfiles; Renovate; minimal deps; signed releases |
| IN-08 | Malicious PRs reaching CI secrets | Critical | No secrets in fork workflows; required review; CODEOWNERS; branch protection |
| IN-09 | GitHub Actions misconfiguration | Critical | Avoid `pull_request_target` with checkout; pin by SHA; least privilege |
| IN-10 | Operator account compromise (GitHub, cloud, registrar) | Blocker | Hardware-key MFA; separate platform accounts |
| IN-11 | DNS hijack or phishing lookalikes | High | Registrar lock; DNSSEC; CAA; CT monitoring |
| IN-12 | MCP manifest manipulation | High | Signed, versioned manifest; pinned versions |
| IN-13 | Request smuggling or cache poisoning | Medium | Managed CDN; no caching of authenticated responses |
| IN-14 | Race conditions on claims and rewards | High | Transactions; unique constraints; idempotency keys |
| IN-15 | Clock or replay attacks on windows | Medium | Server time only; signed timestamps; nonces |
