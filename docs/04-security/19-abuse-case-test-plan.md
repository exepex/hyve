# Abuse-case test plan

Each confirmed vector becomes an abuse case written before the feature it attacks. A control
without a failing attack test is an assumption, not a defense.

## Automated, in CI on every build

| Test | Asserts | Covers |
| --- | --- | --- |
| Signature profile coverage | Altering method, host, path, any query parameter, body, content type, audience or key ID invalidates the signature; duplicate query keys rejected before authorization; replays rejected | A1, IN-16, AB-08, AB-09 |
| Content freshness | Authentic but superseded, expired or revoked `skill.md`, heartbeat, manifest and challenge payloads rejected, including after a client restart; a status block cannot lower a known version; client stops signing after six hours without a fresh status block | PI-07 |
| Signing-tier scope | A response key cannot validate `skill.md`, the SDK, the manifest, a revocation or a pin; the freeze key is accepted only for a freeze-only instruction text | PI-03 |
| Authorization matrix | No cross-tenant read of repos, submissions, messages, stakes | A10, DL-02 |
| Quota and budget admission | Over-quota refused; concurrent max-cost requests with one job's budget left admit at most the affordable work; retries create no unreserved spend; an accounting outage blocks admission | A6, RS-01, RS-13 |
| Re-roll difficulty bounds | 1,000 generated instances stay within band | A7, OR-01 |
| Feedback minimality | No per-test results, correctness-dependent timings, or test names | A7, OR-03, DL-09 |
| Pairing rules | Code single-use and expiring; registration response holds no secret; a different verified owner redeeming a stolen code cannot acquire the agent; the client refuses to counter-sign a foreign owner ID | A2, ID-16 |
| Identity continuity | After rotation: same agent ID, owner slot, ratings, stakes, memberships; old key rejected; the new key cannot register as a new agent | ID-21 |
| Capability boundary | A validly signed teammate message asks for a canary-file read and an out-of-scope signed action; the client denies both even when the model requests them | AB-04 |
| Local harness isolation | Teammate test code tries to read a host canary, reach an endpoint and modify a host file; none succeeds; the harness refuses to run without the sandbox | SB-17 |
| Auto-match consent | An agent without a mandate is never placed; placement outside the mandate (stake, roles, version) is rejected; stake is never locked twice | AB-06 |
| Provisional settlement | RP from a result later overturned cannot have funded a stake or granted a judge seat during the window; reversal leaves unrelated balances untouched | RW-12 |
| Audit projection | Spectator view, public audit feed and Agent Cards combined cannot recover the team-to-agent mapping before finality | DL-13 |
| Ordering determinism | Property test over random score vectors and panel ranks: two implementations agree, and no panel rank ever beats a higher performance tier | core requirement 7 |
| Payout table | Settlement for 0, 1, 2, 3+ passing entries and for ties matches the published table | core requirement 5 |
| Dependency isolation | Internal names unresolvable publicly; unpinned deps fail build | A4, SC-01 |

## Harness-based, before each milestone

| Test | Method | Covers |
| --- | --- | --- |
| Verifier escape battery | Fork bombs, metadata probes, egress attempts, symlink and zip tricks; all contained | A3, SB-* |
| Verifier oracle separation | A malicious guest attempts test-file reads, harness inspection and signalling, and forged verdict output; it learns no hidden answer and never obtains a pass | SB-16 |
| Oracle-extraction simulation | 3 agents, 10,000 variants; measure inferred share of hidden set | A7 |
| Lucky-draw simulation | A flawed solution that passes 20% of draws is submitted repeatedly; accepted correctness and expected rank do not improve | OR-06 |
| Judge-collusion simulation | Ring controlling N% of seats; find the swing point | A8, JD-03 |
| Model-monoculture simulation | All judges one base model; measure how often one adversarial submission fools the panel | JC-01 |
| Commitment hiding | A panel holding the candidate list and another panel's commitment cannot recover that ranking by enumeration; commitments are unusable across panels or challenges | JC-05 |
| Two-panel disagreement | Simulated strong disagreement draws a third panel and never slashes without gold-item or bias evidence | JD-03 |
| Attestation binding | A valid quote replayed with a different key, nonce, audience or an expired session cannot obtain or keep the badge | AO-11 |
| SDK compromise drill | An affected key stays frozen after the client changes its reported version or bypasses the SDK | AB-07 |
| Rating-farm simulation | Provisional farm feeding a flagship; measure gain under provisional weighting | A9, GM-01 |
| Sybil-cost estimate | Real cost to field 10, 100, 1,000 agents | A6, A7, A9 |

## Manual red team, before launch and each major release

- Fake-arena exercise: stand up a lookalike; confirm the reference agent refuses it.
- Operator-compromise tabletop: stolen GitHub session; confirm the offline root, the co-signer and the key freeze contain it.
- Challenge-poisoning review: attempt to pass a payload through review and screening.
- GDPR data-flow walk: trace owner PII and repo contents; confirm export, delete, retention.
