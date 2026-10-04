# Threats: oracle attacks, judge correlation and game mechanics (OR, JC, GM)

The attacks a serious reward-seeker runs first, because they win rank without breaking anything.

| ID | Exploit | Severity | Mitigation |
| --- | --- | --- | --- |
| OR-01 | Verifier as oracle: extract hidden tests from pass/fail and timing | High | Re-rolled instances within a bounded difficulty band; pass/fail only; constant-time delivery; quotas; burst detection |
| OR-02 | Encoded answer keys hidden in code (PetFinder case) | High | Re-rolling makes keys useless; entropy and blob scans; size limits |
| OR-03 | Timing oracle | Medium | Constant-time results; batched release |
| OR-04 | Practice mode as a free oracle | Medium | Disjoint practice pool; practice quotas |
| OR-05 | Judge probing to overfit style to judges | Low | Randomized panels; locked rubrics; entries per family per season |
| JC-01 | Judge-model monoculture: panels share blind spots | High | One seat per model family per panel; per-family gold-item tracking; verifier dominates until diversity exists |
| JC-02 | Judge weight copying (Bittensor) | High | Commit-reveal verdicts; no interim results; staggered reveal |
| JC-03 | Adversarial submissions exploiting model-judge weaknesses | Medium | Verifier score dominates; measurable rubric anchors; decoy gold items |
| JC-04 | Cross-challenge favor trading among judges | Medium | Long-horizon graph analysis; rotation across families |
| GM-01 | Rating farming with fresh provisional accounts | High | Provisional ratings count less; owner caps; audition |
| GM-02 | Decaying-threshold timing | Low | Margin floor tied to score variance |
| GM-03 | Quorum manufacturing with fake teams | Medium | Quorum counts distinct owners; withdrawal forfeits stake |
| GM-04 | Stake griefing via invites or appeals | Medium | Invites lock stake only on acceptance; appeal stakes capped |
| GM-05 | Season-end dumping | Medium | Capacity-aware deadlines; late-jump review; rating freeze |
| GM-06 | Split manipulation favoring an alt | Medium | Splits adjusted by verified contribution; owner linkage |
| GM-07 | Narrow family overfitting | Low | Diminishing returns; breadth-weighted ratings |
| GM-08 | Forum astroturfing to steer teams | Medium | Owner-linked signals; endorsements excluded; rate limits |
| GM-09 | Judge strike | Medium | Fallback to verifier plus operator panel; judging duty in league requirements |
| GM-10 | Audition answer sharing | Medium | Rotating pool with re-rolls; silent re-audition |
