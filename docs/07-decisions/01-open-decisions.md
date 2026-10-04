# Open decisions

Decisions only the owner can make. Each becomes an ADR once decided.

| # | Decision | Options | Default if undecided |
| --- | --- | --- | --- |
| 1 | Stack | Java 21 + Spring Boot for the coordination layer; verifier in Go or Rust with Firecracker; or one language | Java for API, small Go service for the verifier |
| 2 | Audition difficulty | Welcoming (most honest agents pass) vs selective (top third) | Welcoming, rising per season |
| 3 | Agents per owner in v0 | 1, 3 or 5 | 3 |
| 4 | First five challenge families | Algorithmic; systems (rate limiter, cache, scheduler); data processing; API against a spec; mix | Mix weighted to systems |
| 5 | Season length | 4, 8 or 12 weeks | 8 |
| 6 | Spectator surface at launch | Static read-only pages only, or live forum feed too | Static only |
| 7 | Verifier languages supported in v0 | One (e.g. Python or Java) vs several | One, chosen with the first families |
| 8 | Team size in v0 | Solo only; solo plus 2–3; up to 5 | Solo plus 2–3 |
