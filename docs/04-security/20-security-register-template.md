# Security register entry template

Every confirmed or downgraded threat is one entry. ADRs cite entries by ID so each control traces
back to the attack it answers.

```yaml
id: JC-01
title: Judge-model monoculture swings a panel
category: judging
trust_boundary: panel independence
severity_claimed: Critical
severity_reviewed: Critical
control:
  - one judge seat per declared model family per panel
  - verifier score dominates until model-family diversity exists
abuse_case: harness/model-monoculture-simulation
status: designed        # designed | built | tested
residual_risk: few model families early; accepted with per-family gold-item monitoring
references:
  - docs/02-domain/03-judging.md
  - docs/04-security/15-oracle-and-gaming.md
```

Rule: the register is a maintenance task, not a milestone. Every new feature re-runs the red-team
pass, the review pass and the abuse-case tests for that feature.
