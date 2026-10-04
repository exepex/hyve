# Threats: submissions, sandbox and verifier (SB)

Assume every submission is designed to escape, cheat the tests, or burn money.

| ID | Exploit | Severity | Mitigation |
| --- | --- | --- | --- |
| SB-01 | Container or runtime escape | Blocker | MicroVM/gVisor; patched hosts; verifier isolated from API and DB; nothing valuable in the VM |
| SB-02 | Network egress from the verifier | Blocker | No network interface; host and cloud firewall |
| SB-03 | Cloud metadata credential theft | Blocker | No network; metadata route blocked |
| SB-04 | Reading other submissions or tests on disk | Critical | Fresh VM; tests injected and wiped; read-only rootfs |
| SB-05 | Hardcoded expected outputs | High | Hidden tests; re-rolled inputs; property-based tests |
| SB-06 | Environment detection (behaves only under test) | Medium | Indistinguishable environments; randomized data and timing |
| SB-07 | Tampering with harness or timer | Critical | Harness outside submission process; host-side measurement |
| SB-08 | Benchmark spoofing via caching or skipping work | High | Validate outputs per request; randomized payloads; checksums |
| SB-09 | Plagiarism | High | Similarity checks; first-commit tie-break |
| SB-10 | Copying a rival's commits and submitting first | Medium | Private repos until close; commit-reveal |
| SB-11 | Zip bombs, symlinks, path traversal | High | Sandboxed extraction with limits; reject symlinks and absolute paths |
| SB-12 | Malicious build steps | High | Build inside no-network sandbox; vetted offline mirror |
| SB-13 | Log injection and UI XSS from output | Medium | Escape and truncate; structured logs; strict output encoding |
| SB-14 | Timing side channels on shared hardware | Low | Dedicated cores per run |
| SB-15 | Submission is malware others download | High | No public executable downloads; scan artifacts; text-only viewing |
