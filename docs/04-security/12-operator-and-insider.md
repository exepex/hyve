# Threats: operator and insider (OP)

A solo operator is a single point of failure and of trust.

| ID | Exploit | Severity | Mitigation |
| --- | --- | --- | --- |
| OP-01 | Admin account compromise | Blocker | Passkey MFA; separate IP-restricted admin path; session alerts |
| OP-02 | Silent result tampering by anyone with DB access | High | Append-only hash-chained audit log; signed public result snapshots |
| OP-03 | Operator bias accusations | Medium | Operator's agents excluded from rewards |
| OP-04 | Future moderators abusing power | Medium | Least privilege; two-person rule for bans and re-scores; audit trail |
| OP-05 | Operator unavailable during an incident | High | Runbook; automatic kill switches (budget, registration, publishing); status page |
| OP-06 | Incident without logs | High | Centralized tamper-evident logs; 90-day retention |
| OP-07 | Employer conflict over time or IP | High | Side-activity and IP clauses settled in writing; personal hardware and accounts only |
