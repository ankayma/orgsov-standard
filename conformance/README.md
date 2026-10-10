# Conformance

How to test an implementation against [OrgSov v0.2](../STANDARD.md), Part D.

The suites live with the reference implementations and are licensed Apache-2.0 there. This directory points to them; it holds no code yet.

| Part | Suite | Where | State |
|---|---|---|---|
| A — Access | agent as approver refused and recorded; self-approval refused and recorded; path closes at expiry with no action; node enumeration from a compromised node is empty; path proof shows no third party; operator cannot edit or delete a ledger record; third party reads the ledger without the operator; revocation by a named human closes the path and is recorded | — | `[planned]` — not yet published as a set |
| B — Effects | fixed CJCM test set: effect with cause, without cause, with expired cause, with scope mismatch, self-approved → exact V(w), identical on re-run | [cause-justified-change-monitoring](https://github.com/baotnq/cause-justified-change-monitoring) | `[runs]` |
| C — Knowledge | nine-step scenario: assume → admit refused (USE_PROMOTE) → near-duplicate stopped → promote with source → chain readable; principle added → derivation admitted → principle retired lists dependents → dependent reads needs_review → admit on fallen premise refused (PREMISE_NOT_T). Plus: agent as signer refused; restatement of an open assumption without a new exit refused; retire twice; recheck on a derivation refused | t-knowledge-system | `[runs]` |

## Rules (D1, D2)

- Run every suite against your own agent. Passing with one agent says nothing about another.
- **Self-declared** claim: run the suite, publish the results. Form: "conforms to OrgSov v0.2, Part A" (or B, C, any combination).
- **Verified** claim: a party independent of the implementer and the operator runs the suite and reads the evidence in A4, B5, C3 and D3.
- List which `[planned]` clauses you also meet. `[open]` clauses are excluded from every claim.
- The mark **Sovereign Organization** requires Parts A, B and C at the verified level, with a D3 record carrying measures, and is always followed by the standard and version.

## Reporting results

Until a results format is published, open an issue titled `Conformance: <implementation> — Part <X>` with the suite version, the agent tested, the run output and who ran it.
