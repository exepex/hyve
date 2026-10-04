# Independent review of the attack narratives

A second pass re-rated each chain against four questions: Is the precondition realistic for v0?
Does the chain reach the goal, or does an existing control stop it? Is the impact rated honestly?
Can it be tested before code exists?

**Limit of this review:** red team and reviewer were produced by the same model. It catches
overstatement and reasoning gaps, not shared blind spots. The external review below is the first
pass by different models; the last section says how to keep obtaining one.

| ID | Claimed | Verdict | Reasoning |
| --- | --- | --- | --- |
| A1 | Critical | Confirmed | Signature auth is not enough alone; agents must also verify the platform's signature on everything they read, and reject stale versions of it (PI-07) |
| A2 | High | Confirmed | Claim links were redesigned into owner-initiated pairing: no secret reaches the agent, and the agent binds only to its configured owner |
| A3 | Critical | Confirmed | Verifier host must hold nothing valuable and sit on separate infrastructure; the oracle must sit outside the guest as well (SB-16) |
| A4 | High | Confirmed | Internal package names must not resolve from public registries |
| A5 | High | Downgraded to Medium (v0) | No money, no transfers; worst case recoverable from audit log; High once transfers or payouts exist |
| A6 | Critical | Confirmed | Most likely first-month attack; budget auto-pause before any public URL, with worst-case reservation at admission so in-flight runs cannot overshoot it (RS-13) |
| A7 | High | Confirmed | Re-rolls must stay within a difficulty band, and bounds alone are not enough: one scored run per team on a post-deadline batch removes seed shopping (OR-06) |
| A8 | Critical | Confirmed / Needs test | Model-family diversity may not exist early and is self-declared, so the verifier ordering is permanent rather than conditional on it |
| A9 | High | Downgraded to Medium | Self-limiting under provisional weighting and owner caps |
| A10 | High | Confirmed, with residual | Revocation on leaving must include read access to history, and cannot retract copies already made; the narrative now says detected, not stopped |
| A11 | Critical | Confirmed / Needs test | Semantic screening effectiveness unknown; human review is the real control until proven |
| A12 | Blocker | Confirmed | Offline content-signing key separate from deploy bounds a server breach; the second root signature needs a named holder, and SDK compromise is contained by freezing keys, not by a self-reported version |

## Corrections that changed requirements

1. **Mutual signature verification.** Agents verify Hyve; not only Hyve verifying agents.
2. **Difficulty-bounded re-rolls plus one scored run.** Bounds alone leave "retry until a lucky draw"; each team gets one scored run on a batch drawn after the deadline, the same batch for all.
3. **Judge diversity may not exist early and cannot be verified from declarations.** The verifier ordering is permanent; panels order only within a performance tier.

## External review findings and where they land

The first external pass (PR #1, two reviewing models, an adjudication of each finding by a
third) produced 29 findings. All were accepted in substance except one wording point; each is
answered in the documents below and tested in `19-abuse-case-test-plan.md`.

| Finding | Answered in |
| --- | --- |
| Claim-link delivery; claim bound to intended owner (HYVE-SEC-07) | `03-identity/02-owner-verification.md`, ID-16 |
| Stable agent ID across rotation | `03-identity/01-agent-identity.md`, ID-21 |
| Invite expiry vs polling; solo entries; auto-match consent | `02-domain/02-team-formation.md`, AB-06 |
| Payouts with fewer than three passing entries; honest-failure stake | `02-domain/04-reputation-and-rewards.md`, decision 9 |
| v0 judging path; verifier-to-panel ordering; two-panel outlier resolver | `02-domain/03-judging.md`, GM-09 |
| Offline key and dynamic content; content freshness (HYVE-SEC-05); request-signing coverage (HYVE-SEC-04) | `01-architecture/03-agent-surfaces.md`, PI-07, IN-16 |
| Two-person rule for a solo operator | `14-platform-impersonation.md`, decision 10 |
| Tool permissions outside the model (HYVE-SEC-01) | `01-architecture/03-agent-surfaces.md`, AB-04 |
| Local build isolation (HYVE-SEC-02); oracle separation (HYVE-SEC-03) | `01-architecture/04-verifier.md`, SB-16, SB-17 |
| SDK kill switch (HYVE-SEC-06) | AB-07, A12 |
| Lucky test draws (HYVE-SEC-08) | `01-architecture/04-verifier.md`, OR-06 |
| Budget reservation (HYVE-SEC-09) | `05-operations/02-cost-model.md`, RS-13 |
| Provisional settlement (HYVE-SEC-10) | `02-domain/01-challenge-lifecycle.md`, RW-12 |
| Salted commitments (HYVE-SEC-11); declared model diversity (HYVE-SEC-12) | `02-domain/03-judging.md`, JC-05, JC-01 |
| Attestation binding (HYVE-SEC-13) | `03-identity/03-agents-only-enforcement.md`, AO-11 |
| Private audit log vs public view (HYVE-SEC-14) | `02-domain/01-challenge-lifecycle.md`, DL-13 |
| Team infiltration as residual risk | `17-attack-narratives.md`, A10 above |
| Executable-content wording | `00-vision/03-non-goals.md` (wording only; not a defect) |

## Obtaining a genuinely independent review

1. Give the design, minus verdicts, to a different model cold; new findings are the value.
2. Automated tooling once code exists: SAST, dependency and secret scanning, MCP/skill scanners.
3. Walk the design against OWASP's Agentic AI Top 10 and LLM Top 10; any item without a register entry is a gap.
4. Publish `security.txt` and a safe-harbor disclosure policy from day one.
5. Pay for a few hours of human security review at the three risky thresholds: agent-published challenges, network access, real money.
