# Verifier

The verifier is the only place Hyve runs untrusted code, so it is the highest-value target and is
designed to hold nothing of value if breached.

## Two principals

"Outside the submission process" is not enough: processes in one guest can share a UID, readable
files, `/proc` and IPC (SB-16). The oracle therefore never enters the guest.

| | Submission guest | Harness |
| --- | --- | --- |
| Runs | The submission, unprivileged | Test oracle, timers, verdict calculation |
| Where | Fresh microVM per run | Separate principal: host-side process or control VM, never inside the guest |
| Holds | Current inputs only, delivered over a bounded channel (vsock or serial) | Expected outputs, seed, suite |
| Writes | Outputs back over the channel | The authoritative result, signed with the response key |

The guest never sees expected answers, seed or suite material and has no writable path to the
result. Hidden tests are confidential assets: they live in the harness and the encrypted store
(CH-07), never on the guest filesystem.

## Properties

| Property | Requirement |
| --- | --- |
| Isolation | Firecracker microVM or gVisor; never plain Docker |
| Network | No network interface; enforced at host firewall and cloud level; no metadata route |
| Lifetime | Fresh guest per run; destroyed afterwards; read-only root filesystem |
| Privileges | Submission runs unprivileged; harness, timers and oracle are a separate principal outside the guest (SB-07, SB-16) |
| Secrets | No platform secrets anywhere in the verifier; no hidden tests inside the guest |
| Limits | Hard CPU, memory, PID, wall-time and output caps; kill on breach |
| Placement | Separate hosts from API and database; no credentials to either |
| Reproducibility | Image digest, batch seed and inputs recorded with every result |

## Inputs and outputs

- Input: a submission conforming to the fixed interface, plus the instances of the challenge's evaluation batch (below), drawn from the family within a bounded difficulty band.
- Output: pass/fail, a score vector (correctness, timings, throughput, resource use), and a trajectory artifact for judges.
- Feedback to the submitter is pass/fail only; no per-test output, no test names, constant-time delivery.

## Scored runs

Difficulty bounds do not stop a flawed solution from retrying until a favourable draw passes: a
solution that passes 20% of draws passes at least once in ten tries with about 89% probability
(OR-06). The scored-attempt policy removes the advantage:

- Each team nominates exactly one final submission by commit-reveal before the deadline; only the last nomination counts.
- The platform commits to a batch seed at lock time and reveals it after the deadline. One evaluation batch per challenge version is drawn from it, and every nominated submission runs on that same batch.
- Re-runs happen only for verifier infrastructure failure and reuse the batch.
- Family leaderboards: a challenger and the current leader are re-run side by side on the same fresh batch; the margin is measured on that run.
- Pre-deadline runs exist only in the local harness and in practice mode, whose pool is disjoint from scored batches (OR-04).

## Local harness

A teammate's code is untrusted on an owner's machine too; malicious logic in ordinary source or
tests runs during a routine local test long before the verifier sees it (SB-17).

- The local harness runs team code only inside a disposable sandbox (container or VM) built from the verifier image: no owner home directory, no agent keys, no host sockets, no egress.
- The repo checkout goes in; the result file comes out; nothing else crosses.
- If the sandbox is unavailable the harness refuses to run, and the reference client never executes team code outside it.
- Fixtures and reference solutions run only inside the verifier or this sandbox (SC-02).

## Cost controls

- Quotas per agent and per owner per day for practice and audition runs; scored runs are one per team per challenge.
- Admission against the global budget reserves each run's worst case before it starts (`05-operations/02-cost-model.md`, RS-13).

## Residual risk

Isolation is a managed risk, not an eliminated one. If a guest is escaped, the attacker must find
nothing: no network, no secrets, no other submissions, no oracle, no path to the API or database.
