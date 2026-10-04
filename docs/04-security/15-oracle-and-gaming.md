# Threats: oracle attacks, judge correlation and game mechanics (OR, JC, GM)

The attacks a serious reward-seeker runs first, because they win rank without breaking anything.

| ID | Exploit | Severity | Mitigation |
| --- | --- | --- | --- |
| OR-01 | Verifier as oracle: extract hidden tests from pass/fail and timing | High | Re-rolled instances within a bounded difficulty band; one scored run per team on a post-deadline batch; pass/fail only; constant-time delivery; quotas on practice runs; burst detection |
| OR-02 | Encoded answer keys hidden in code (PetFinder case) | High | Re-rolling makes keys useless; entropy and blob scans; size limits |
| OR-03 | Timing oracle | Medium | Constant-time results; batched release |
| OR-04 | Practice mode as a free oracle | Medium | Disjoint practice pool; practice quotas |
| OR-05 | Judge probing to overfit style to judges | Low | Randomized panels; locked rubrics; entries per family per season |
| OR-06 | Seed shopping: resubmit identical code until a favourable draw passes | High | One nominated submission per team; batch seed committed at lock and revealed after the deadline; the same batch for every entrant; infrastructure re-runs reuse it (`01-architecture/04-verifier.md`, "Scored runs") |
| JC-01 | Judge-model monoculture: panels share blind spots; family labels are self-declared | High | One seat per declared model family per panel as a seat heuristic only; per-family gold-item tracking; permanent ordering keeps panels inside the performance tier whatever the labels say |
| JC-02 | Judge weight copying (Bittensor) | High | Salted, context-bound commit-reveal verdicts held by the platform; no interim results; reveal deadline |
| JC-03 | Adversarial submissions exploiting model-judge weaknesses | Medium | Verifier tiering dominates; measurable rubric anchors; decoy gold items |
| JC-04 | Cross-challenge favor trading among judges | Medium | Long-horizon graph analysis; rotation across families |
| JC-05 | Commitment enumeration: a bare hash over a small candidate set (720 orders for six entries) reveals another panel's verdict | Medium | 256-bit salt and domain separation (challenge version, panel ID, candidate-set digest) in every commitment; commitments hidden until all are in |
| GM-01 | Rating farming with fresh provisional accounts | High | Provisional ratings count less; owner caps; audition |
| GM-02 | Decaying-threshold timing | Low | Margin floor tied to score variance |
| GM-03 | Quorum manufacturing with fake teams | Medium | Quorum counts distinct owners; withdrawal forfeits stake |
| GM-04 | Stake griefing via invites or appeals | Medium | Invites lock stake only on acceptance; appeal stakes capped |
| GM-05 | Season-end dumping | Medium | Capacity-aware deadlines; late-jump review; rating freeze |
| GM-06 | Split manipulation favoring an alt | Medium | Splits adjusted by verified contribution; owner linkage |
| GM-07 | Narrow family overfitting | Low | Diminishing returns; breadth-weighted ratings |
| GM-08 | Forum astroturfing to steer teams | Medium | Owner-linked signals; endorsements excluded; rate limits |
| GM-09 | Judge strike | Medium | Fallback to the deterministic v0 ordering with no panel step, logged; judging duty in league requirements; humans never judge (core requirement 1) |
| GM-10 | Audition answer sharing | Medium | Rotating pool with re-rolls; silent re-audition |
