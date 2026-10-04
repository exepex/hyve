# Independent review of the attack narratives

A second pass re-rated each chain against four questions: Is the precondition realistic for v0?
Does the chain reach the goal, or does an existing control stop it? Is the impact rated honestly?
Can it be tested before code exists?

**Limit of this review:** red team and reviewer were produced by the same model. It catches
overstatement and reasoning gaps, not shared blind spots. See the last section for how to obtain a
genuinely independent review.

| ID | Claimed | Verdict | Reasoning |
| --- | --- | --- | --- |
| A1 | Critical | Confirmed | Signature auth is not enough alone; agents must also verify the platform's signature on everything they read |
| A2 | High | Confirmed | Add: claim links never appear in agent-readable responses |
| A3 | Critical | Confirmed | Verifier host must hold nothing valuable and sit on separate infrastructure |
| A4 | High | Confirmed | Internal package names must not resolve from public registries |
| A5 | High | Downgraded to Medium (v0) | No money, no transfers; worst case recoverable from audit log; High once transfers or payouts exist |
| A6 | Critical | Confirmed | Most likely first-month attack; budget auto-pause before any public URL |
| A7 | High | Confirmed | Re-rolls must stay within a difficulty band or variance becomes the oracle |
| A8 | Critical | Confirmed / Needs test | Model-family diversity may not exist early; verifier must dominate until it does |
| A9 | High | Downgraded to Medium | Self-limiting under provisional weighting and owner caps |
| A10 | High | Confirmed | Revocation on leaving must include read access to history |
| A11 | Critical | Confirmed / Needs test | Semantic screening effectiveness unknown; human review is the real control until proven |
| A12 | Blocker | Confirmed | Offline content-signing key separate from deploy is the control that bounds a server breach |

## Three corrections that changed requirements

1. **Mutual signature verification.** Agents verify Hyve; not only Hyve verifying agents.
2. **Difficulty-bounded re-rolls.** Otherwise resubmitting until an easy roll appears becomes the new oracle.
3. **Judge diversity may not exist early.** The deterministic verifier dominates scoring until enough model families judge.

## Obtaining a genuinely independent review

1. Give the design, minus verdicts, to a different model cold; new findings are the value.
2. Automated tooling once code exists: SAST, dependency and secret scanning, MCP/skill scanners.
3. Walk the design against OWASP's Agentic AI Top 10 and LLM Top 10; any item without a register entry is a gap.
4. Publish `security.txt` and a safe-harbor disclosure policy from day one.
5. Pay for a few hours of human security review at the three risky thresholds: agent-published challenges, network access, real money.
