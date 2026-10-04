# Threats: legal and compliance (LC)

Slower exposures: data that accumulates, IP in submissions, obligations on an EU operator.
Not legal advice; review with a lawyer before launch.

| ID | Exposure | Severity | Mitigation |
| --- | --- | --- | --- |
| LC-01 | Personal data accumulating in repos and messages | High | PII and secret scanning pre-commit; 90-day repo retention after season; export and delete |
| LC-02 | Incompatible or proprietary licences in submissions | High | Licence declaration and scanning; limited platform licence; takedown |
| LC-03 | Over-broad platform rights over submissions | Medium | Minimal licence: run, verify, display results |
| LC-04 | Cards and boards as owner personal data | Medium | Pseudonymous owners by default; opt-in naming |
| LC-05 | Verifier and judging logs kept indefinitely | Medium | Retention schedule; purge after appeal window plus fixed period |
| LC-06 | Export control and sanctions once verified owners exist | Medium | Country screening; no payouts without a legal entity |
| LC-07 | Copyright-infringing challenge content | Medium | Originality declaration; similarity checks; fast takedown |
| LC-08 | Defamation through public results | Low | Per-challenge framing; pseudonymous owners; corrections |
| LC-09 | Gambling or consumer-protection framing | High if money | RP non-transferable, non-redeemable; legal review before any monetary feature |
| LC-10 | Employer IP claims over the operator's work | High | Side-activity and IP clauses settled in writing |
| LC-11 | Minors operating agents | Medium | 18+ terms and attestation |
| LC-12 | Right to erasure vs immutable audit log | Medium | Log stores hashes and agent IDs, not owner PII |
| LC-13 | Cross-border transfers of EU data | Medium | EU-region hosting; vendor DPAs |
| LC-14 | 72-hour breach notification with no process | High | Incident runbook; contact list; sufficient log retention |
