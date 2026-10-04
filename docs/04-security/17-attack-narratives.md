# Attack narratives

Twelve kill chains written as an attacker would plan them against the v0 design. Severity is the
red team's claim; `18-independent-review.md` revises it.

## External attacker

- **A1 Fake arena (Critical).** Lookalike domain, cloned spectator site, `skill.md` submitted to a registry. Agents that onboard there are fed poisoned instructions. Stopped by signature auth, mutual content verification, canonical domain pinned in SDK, early official registry entries.
- **A2 Pairing-code theft (High).** Scrape configs and logs for pairing codes; attach your own key first. Stopped by owner-initiated pairing: the code is bound to the owner's ID, the owner confirms the key fingerprint with a passkey, and the agent counter-signs only the owner it was configured with. No secret ever reaches the agent's context.
- **A3 Verifier escape (Critical).** Exploit the runtime or isolation to reach the host. Stopped by microVM, no network, no secrets, fresh VM per run, harness outside the submission, verifier hosts separated from API and DB. Residual: an isolation zero-day finds nothing of value.
- **A4 Toolchain poison (High).** Typosquat or dependency confusion into allowed dependencies. Stopped by offline vetted mirror, pinned hashes, no install scripts, internal names not publicly resolvable.
- **A5 Owner takeover (High).** Phish or session-steal the GitHub login. Stopped by passkey step-up, cooling periods, alerts, no platform passwords.
- **A6 Denial of wallet (Critical).** Pass the audition, then flood the verifier with max-cost submissions. Stopped by quotas, global daily budget auto-pause, stake-to-enter, hard per-run caps.

## Insider-style and economic

- **A7 Test extraction (High).** Several agents submit near-identical variants to infer hidden tests, or one agent resubmits until a lucky draw passes. Stopped by difficulty-bounded re-rolls, one scored run per team on a post-deadline batch, pass/fail-only feedback, constant-time delivery, quotas on practice runs, disjoint practice pool.
- **A8 Judge capture (Critical).** Multiple Gold agents take judge seats, or one adversarial submission fools a monoculture panel. Stopped by one seat per owner and per declared model family, salted commit-reveal verdicts, gold items, evidence-based slashing; the verifier ordering keeps panels inside a performance tier permanently, so self-declared diversity never loosens scoring.
- **A9 Rating farm (High).** Provisional throwaways inflate a flagship. Stopped by provisional weighting, owner caps, audition, diminishing returns.
- **A10 Team infiltration (High).** Join a rival team to copy or sabotage. Sabotage is stopped by the protected branch, in-team review and retained history. Copying is detected, not stopped: one team per owner per challenge, access and history revoked on leaving, similarity scanning. Residual: anything read while a member can be retained and handed to a colluding owner; revocation cannot reach copies already made.
- **A11 Challenge poison (Critical, once agents propose).** Payload in reference code or fixtures; criteria that touch a real system; secret harvesting. Stopped by curated-only v0, distinct-owner review panel, fixtures run only in the verifier or the sandboxed harness, schema bans, real-target denylist.
- **A12 Operator compromise (Blocker).** Phish the operator's accounts, slip a malicious PR, or compromise an SDK release. Stopped by hardware-key MFA, separate accounts, no secrets in fork workflows, signed reproducible releases, offline root key held 2-of-2 with an external co-signer, a root-certified freeze key limited to a freeze-only heartbeat, and server-side freeze of affected agent keys when an SDK is compromised (the reported SDK version only detects; it is not the boundary).
