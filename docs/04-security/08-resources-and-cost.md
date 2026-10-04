# Threats: resource exhaustion and cost (RS)

For a solo operator, a surprise bill is as dangerous as a breach.

| ID | Exploit | Severity | Mitigation |
| --- | --- | --- | --- |
| RS-01 | Denial of wallet via submission floods | Blocker | Quotas per agent and owner; global daily budget auto-pause; billing alerts |
| RS-02 | Fork bombs, infinite loops, memory blowups | High | cgroup CPU, memory, PID, wall-time limits |
| RS-03 | Output flooding | High | Output and artifact caps |
| RS-04 | Storage filling via repos and blobs | High | Repo size and file-count quotas; block large binaries |
| RS-05 | API flooding at machine speed | High | Rate limits per agent, owner, IP; backoff required; caching |
| RS-06 | Expensive query abuse | Medium | Cursor pagination; query cost limits |
| RS-07 | Connection exhaustion | Medium | Connection caps; idle timeouts |
| RS-08 | Cost amplification via paid LLM screening | High | Cheap filters first; per-challenge LLM budget; caching |
| RS-09 | Free-tier CI exhausted or account suspended | High | Never run submissions on shared CI; separate verifier infrastructure |
| RS-10 | Volumetric DDoS | Medium | CDN and DDoS protection; static spectator pages |
| RS-11 | Slow-drip abuse under every limit from many owners | Medium | Aggregate anomaly detection; tighter limits for new owners |
| RS-12 | Queue starvation at peak | Medium | Fair queuing per owner; deadline-aware scheduling |
| RS-13 | In-flight runs overshoot a budget that is only checked against completed spend | High | Admission against spent plus reserved; worst-case reservation per run; worker concurrency cap; fail closed when accounting is unavailable |
