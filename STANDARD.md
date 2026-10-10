# Organizational Sovereignty Standard (OrgSov) — v0.2 draft

Checkable requirements for organizations that let AI agents act and produce knowledge.

Status: draft for the author's review, 10 October 2026. Supersedes v0.1 draft (27 September 2026). Not yet co-audited (see §11).
License: text of this standard under CC BY 4.0; conformance suites and reference implementations under Apache-2.0. The names and the mark "Sovereign Organization" are not licensed (D1.5). See [LICENSE](LICENSE).
Author: Bao Trinh (Ankayma, UAE). Public thesis: https://baotrinh.com — risk branch `/risk/`, speed branch `/speed/`.

Marks used in this document:
- `[runs]` — the requirement is enforced today by at least one reference implementation.
- `[planned]` — specified, not yet enforced by a reference implementation. Excluded from conformance claims for v0.2.
- `[open]` — a design choice the author has not yet made. Not a requirement until resolved.
- MUST / MUST NOT / MAY are used in their usual normative sense (RFC 2119).

Abbreviations are introduced once, in §2, and each Part repeats the full term at first use. The standard restates, in normative form, what the source specifications already say (Appendix A). Where the two differ, the source specification governs until v1.0.

---

## Overview for the board

An organization is sovereign over its AI agents when it decides what they may reach and what they may treat as true, and can prove both to a third party.

Agents now open connections, run tools and write into company records at machine speed. The question a board has to answer is not whether an agent will make a mistake, but who answers when it does, and whether the record of what happened survives the people who made it. This standard puts two checkable conditions on every agent system:

- **Access.** Every connection an agent or a person uses has a grant behind it, a named human approved that grant on a device the agent cannot fake, the grant ends on its own, and every grant, opening, closing and refusal sits in a ledger nobody can edit. Three words: *isolated, granted, evidenced*.
- **Knowledge.** Every claim an agent treats as true has a dated source or a derivation that rebuilds, a named human signed it, and the record walks back to its basis; when the basis falls, everything built on it is flagged. Three words: *truth, trust, traceable*.

Both conditions share one invariant: every change of state — a path opened, a claim accepted — has a named, authorized cause, recorded where it cannot be edited, and checked continuously by a machine that can only raise a flag. The agent proposes. A human with something to lose signs. A third party reads the record without asking the operator for help.

An organization that meets both conditions can let any agent, from any vendor, work at full speed in the zones where mistakes can be undone, and can show an auditor, a regulator or an insurer exactly what the agent reached, what it believed, and who stood behind each.

The standard says what must hold. It does not say how to build it, which vendor to use, or which model to run.

---

## 1. Scope and place among existing standards

### 1.1 What this standard governs

Two objects: **paths** (who can reach what, through the organization's access layer) and **claims** (what is treated as true in the organization's knowledge ledger). A third object, **effects** (what an agent does once it has a path), is governed by Part B, which restates the Cause-Justified Change Monitoring invariant.

### 1.2 What it is not

It is not a management-system standard. ISO/IEC 42001 defines how an organization runs an AI management system — context, leadership, planning, support, operation, evaluation, improvement — and supplies a control set in its Annex A; NIST AI RMF organizes risk work into Govern, Map, Measure, Manage. OrgSov sits one level down: it is a set of **control requirements with mandatory evidence**, the layer at which ISO/IEC 27001 Annex A controls or SOC 2 trust criteria operate. An organization running ISO 42001 or NIST AI RMF selects OrgSov as the technical control set for its agent systems; OrgSov does not replace the management system.

### 1.3 Where it lands in the familiar frameworks

| Framework | Where OrgSov attaches |
|---|---|
| ISO/IEC 42001:2023 | Clause 8 (operation) and Annex A: AI system life cycle (A.6), use of AI systems (A.9), third-party relationships (A.10). Evidence records in Part D feed the Statement of Applicability. |
| ISO/IEC 27001:2022 Annex A | Access control (A.5.15, A.5.18), privileged access (A.8.2), logging (A.8.15), monitoring (A.8.16). Part A is a stricter form of these for the agent access layer. |
| NIST AI RMF 1.0 | GOVERN 2.1 (roles, responsibilities and lines of communication documented), MAP 3.5 (human oversight defined, assessed and documented), MANAGE 2.3 (response to newly identified risks). Part A and Part C supply the records; Part D supplies the measures. |
| IIA Three Lines Model | Line 1: zone owners and signers (management, owns the risk). Line 2: the continuous machine check and the risk function (reads flags, owns no record). Line 3: the independent reader (internal audit). External audit reads Part D without the operator's help. |

### 1.4 Who answers for what

| Role in this standard | Line | Answers for |
|---|---|---|
| Approver (Part A), Signer (Part C) | Line 1 | every path they opened, every claim they signed; their name falls with it |
| Zone owner | Line 1 | the ceiling of the zone and the declared scope (A6) |
| Continuous check | Line 2 | flags raised on every write; changes no status |
| Independent reader | Line 3 | reads the ledgers and the conformance evidence; names the gaps |
| Operator of the access layer or ledger | — | runs the system; MUST NOT be able to edit either ledger |

---

## 2. Terms

| Term | Meaning in this standard | Source |
|---|---|---|
| access layer | the overlay through which Part A governs reachability; connections outside it are the organization's declared risk (A6) | Ankayma page |
| node | the endpoint of the access layer on one device or service; accepts a connection only under a current grant that names it as one of the two ends | Ankayma page |
| path | a connection between exactly two nodes, alive for the life of one grant | Ankayma page |
| zone | a named set of nodes sharing one purpose and one ceiling; membership in a zone creates no path | essay Risk 6; Ankayma page |
| ceiling | the maximum loss if an entire zone is lost, stated before any grant in it | essay Risk 2 |
| grant | an approval naming a requester, an approver, two nodes, a scope, a purpose, a validity window and an expiry | CJCM; Ankayma page |
| effect | a change in the world caused by an actor: tool call, write, transfer | CJCM |
| irreversible effect | an effect whose loss cannot be restored with the capital and time available | essay Risk 2 |
| cause | an approval or standing grant that authorizes a class of effects, recorded independently of the actor | CJCM |
| actor / producer | the identity that performs an effect or produces a claim; may be an agent | T-ledger; TK spec |
| approver | the human whose hardware-bound approval stands behind a grant; never an agent | Ankayma page |
| signer | the human whose name stands behind a claim; never an agent | TK spec |
| claim | a statement proposed for the knowledge ledger | TK spec |
| principle | an axiom of the ledger owner; has no basis, because it is the basis. Abbreviated P after this table. | TK spec, P.9 |
| trusted claim | a claim that passed admission: a fact with a citable dated source, or a derivation from standing principles and trusted claims. Abbreviated T. | TK spec |
| assumption | a claim held open, with a declared exit. Abbreviated A. | TK spec |
| basis | the source or the premises a trusted claim rests on | TK spec |
| ledger | an append-only record; the access ledger holds grants and path events, the knowledge ledger holds claims with marks, basis, signer, producer and history | Ankayma page; TK spec |
| move | a named, reasoned change of a record's status by a human: promote, demote, retire, recheck, approve, reject, refer, revoke | T-ledger §5 |
| flag | work for a human raised by the machine; changes no status | T-ledger §5.3 |

---

## 2b. Invariants

Every clause in Parts A, B and C derives from one of the seven statements below. A conforming implementation keeps all seven true at all times; the test suites in Part D check them. Invariants are referred to by their name, not by a number.

**Common.**

*Cause.* Every change of state has a named, authorized cause, recorded where it cannot be edited, and checked continuously off the write path by a machine that can only raise a flag. In Part A the state is *reachable*; in Part B it is *changed*; in Part C it is *treated as true*.

**Access — isolated · granted · evidenced.**

*Isolated.* No standing path. A node holds no map. One node compromised is one grant, two nodes, one expiry.

*Granted.* No path without a grant. No grant without a human bound to hardware who is not the requester. Every grant names two nodes, a scope and an expiry that ends it on its own.

*Evidenced.* Every grant, opening, closing and refusal is appended. Nothing is deleted. A party other than the operator reads it.

**Knowledge — truth · trust · traceable.**

*Truth.* A trusted claim is a fact with a dated source, or a derivation that rebuilds from principles and trusted claims that still stand.

*Trust.* Exactly one human signs each claim. An agent never signs. The signer's name falls with the claim.

*Traceable.* Every trusted claim walks back to its basis. Nothing is deleted. When a premise falls, every claim that stood on it reads as fallen. Status is computed from history, never stored.

Part B carries no invariant of its own: it is *Cause* applied to effects, with the cause channel as the record.

---

## 3. Part A — Access (access sovereignty)

**Definition.** Access sovereignty is the standing work of keeping every path in the access layer at all three: isolated, granted, evidenced. A path exists only for a grant a human made and a ledger holds. The organization is the root of every grant. Nobody alone — an agent, a compromised node or an insider — can create a path or erase its record.

**Invariants.** Isolated, Granted, Evidenced (§2b). Each section below names the invariant it enforces.

**Threat model** (informative). Part A is tested against three adversaries: an agent acting against instruction (injection, self-expansion); an attacker who holds an internal node and its keys; an insider with a valid identity and a motive. For each, the suite in D2 checks that no path opens without A2 and that every attempt appears in A4.

### A1. Isolated — nodes and zones `[runs: Ankayma]`
- A1.1 Every device or service under this Part MUST terminate the access layer in a node with its own identity.
- A1.2 Nodes MUST be grouped into zones. A zone MUST carry a purpose and a ceiling stated before any grant in it. `[planned: ceiling as a recorded field]`
- A1.3 Membership in a zone MUST NOT create a path. Every path, inside or across a zone, is a separate grant.
- A1.4 A node MUST hold no map of other nodes and no standing route to any of them.
- A1.5 The access layer MUST have no path that exists without a current grant.
- A1.6 A path MUST connect exactly two nodes. A grant MUST NOT open a path to a set of nodes.
- A1.7 No party other than the two nodes MAY sit on the path. The operator of the access layer coordinates grants and MUST NOT carry traffic. This MUST be checkable by a path proof the organization can run.
- A1.8 Compromise of one node MUST yield no more than the paths of that node's current grants, until their expiry. No key held on a node MAY create a grant.

### A2. Granted — a human behind every grant `[runs: Ankayma, single approver; planned: k-of-n]`
- A2.1 A grant MUST be approved by a human whose approval is bound to a hardware identity.
- A2.2 An agent MUST NOT be an approver. An attempt MUST be rejected and recorded.
- A2.3 The approver MUST NOT be the requester. Self-approval MUST be rejected at write time.
- A2.4 A grant MAY require k of n approvers. The required k is set by the ceiling of the zone, not by the requester.
- A2.5 `[open]` Whether an agent MAY be a requester. If yes, the grant names both the agent and the human under whose grant the agent runs.

### A3. Granted — bounded life `[runs: Ankayma]`
- A3.1 Every grant MUST carry an expiry. The path MUST end at expiry without any further action.
- A3.2 A grant MUST be revocable by a named human before expiry. Revocation closes the path and is recorded.
- A3.3 `[open]` Whether a live grant MAY be renewed by its approver, or every extension is a new grant. Either way the ledger links the records.
- A3.4 The maximum life of a grant is set by the organization per zone. The standard sets no number.

### A4. Evidenced — the access ledger `[runs: Ankayma]`
- A4.1 The ledger MUST record every grant issued, every path opened, every path closed (by expiry or revocation), and every request refused — each with time, the two nodes, requester, approver and reason.
- A4.2 The ledger MUST be append-only. No record MAY be edited or deleted after the fact by anyone, including the operator.
- A4.3 The ledger MUST be read continuously by a party other than the operator, and MUST be readable by a third party without the operator's help.
- A4.4 A gap in the ledger is itself a finding to report.

### A5. Evidenced — continuous check `[planned: continuous checker over the access ledger]`
- A5.1 A machine MUST check the access ledger on write events: a path with no current grant; a grant whose approver is also its requester; a grant with no expiry; a path alive past expiry.
- A5.2 The machine MUST NOT create, close or edit a grant. It raises flags.

### A6. Declared scope `[planned: as a record]`
- A6.1 The organization MUST declare, per zone, whether its resources are reachable only through the access layer or also through standing connections outside it (direct network, remote shell, physical).
- A6.2 The declaration is part of the evidence record (Part D). Connections outside the access layer are outside this Part. What the organization leaves outside is its own risk, stated in writing.

---

## 4. Part B — Effects

Part B restates the Cause-Justified Change Monitoring (CJCM) invariant: every effect has a cause. Access (Part A) answers who opened a path and for how long; Part B answers what was done through it, and whether a cause stood behind it. Clauses are carried from v0.1 A2–A4, A7, A8 without change of substance.

### B1. Reversibility decides the gate
- B1.1 An effect that can be undone — its loss restored with the capital and time available — MAY run without prior admission.
- B1.2 An effect that cannot be undone MUST NOT run before it is admitted by a cause (B2).
- B1.3 The line between B1.1 and B1.2 is the ceiling and the capital behind it, not the actor's capability.

### B2. Cause channel `[runs: CJCM]`
- B2.1 Causes MUST be recorded in a channel separate from the actor that produces effects.
- B2.2 A cause MUST carry: identifier, effect type, scope, approver, validity window, expiry.
- B2.3 The approver of a cause MUST NOT be the actor of the effect it authorizes. Self-approval MUST be rejected at write time.
- B2.4 An expired cause MUST NOT justify an effect.
- B2.5 A grant under Part A MAY serve as a cause for effects within its scope. A trusted claim under Part C MAY serve as the cause of a decision.

### B3. The invariant: every effect has a cause `[runs: CJCM]`
- B3.1 For any window w, the set of violations V(w) = {effects in w} \ {effects matched by a valid cause} MUST be computable as an exact set difference. No model, no score.
- B3.2 The check MUST run off the write path: it reads the effect log and the cause channel; it does not block the actor. A gap in the checker is itself a violation to report.
- B3.3 The check MUST be deterministic: the same inputs give the same V(w).
- B3.4 Each violation MUST name the effect and the reason: no cause, expired, scope mismatch, self-approved.
- B3.5 The reverse set, missing_change(w) = {causes valid in w with no matching effect}, SHOULD be reported as a coverage question.
- B3.6 Blocked and failed effects MUST be first-class records, not noise.

### B4. Roll-up: appointment is an effect with a price `[planned]`
- B4.1 If A appoints B to a zone whose ceiling B cannot cover, A guarantees the shortfall.
- B4.2 The graph of appointments MUST be a tree with real, staked capital at its root; no zone may carry a ceiling larger than that root can cover.
- B4.3 Appointment itself passes through the gate of B1–B2.

### B5. Evidence `[runs: CJCM report]`
- B5.1 The effect log, the cause channel and V(w) reports MUST be readable by a third party without the operator's help.

---

## 5. Part C — Knowledge (knowledge sovereignty)

**Definition.** Knowledge sovereignty is the standing work of keeping every trusted claim in the ledger at all three: truth, trust, traceable. A claim counts as knowledge only with a path back and a human name. The organization can withdraw any claim, and the withdrawal reaches everything that stood on it.

**Invariants.** Truth, Trust, Traceable (§2b). Each section below names the invariant it enforces.

Clauses are carried from v0.1 B1–B11, regrouped under the three invariants and one enforcement section.

### C1. Truth — three classes and admission `[runs: TK]`
- C1.1 A ledger MUST hold exactly three classes of record: principle (P), trusted claim (T), assumption (A).
- C1.2 Principles have no basis. Trusted claims have a basis. Assumptions declare how they will be resolved.
- C1.3 Principles and facts are not exempt from checking; they are checked by routes other than derivation: external challenge, newer sources.
- C1.4 A trusted claim MUST be admitted only as (a) a fact with a citable source and source date, or (b) a derivation whose premises are standing principles and trusted claims named by identifier.
- C1.5 A claim currently held as an open assumption MUST NOT be admitted as a second record; the only path is promotion of that assumption (C2.6).
- C1.6 A claim identical to an existing record MUST NOT be written again; the existing record is returned.
- C1.7 A claim near-identical to an existing record (by similarity or by containing it) MUST stop and wait for a human decision.
- C1.8 A trusted claim MUST NOT be built on a premise that no longer stands (C3.5).
- C1.9 An assumption MUST declare its type and exit: A-p (observable — declare what raises and what refutes it), A-c (closed by amendment), A-b (blocked until a channel exists), A-r (never raised). Changing the statement of an open assumption MUST restate its exit, or be rejected.

### C2. Trust — a human name on every record and every move `[runs: TK]`
- C2.1 Every record MUST carry a signer (the human) and a producer (the tool or agent that wrote it), and the grant under which it was written.
- C2.2 An agent MUST NOT be a signer. An attempt MUST be rejected.
- C2.3 Exactly one signer per record. Groups review; a name signs.
- C2.4 Every move MUST carry the mover's name and a reason.
- C2.5 demote: a trusted claim is marked as no longer holding, with a reason and optionally the contradicting record. retire: a record is withdrawn without deletion; dependents are listed. recheck: a fact is re-verified against its source; derivations are rechecked by rebuilding the chain.
- C2.6 promote: an observable assumption whose declared condition is met becomes a trusted claim with the same wording; the assumption closes and history records the link.
- C2.7 Principles are append-only: a principle MUST NOT be edited. Adding one is an amendment under one name. Retiring one triggers C3.6.

### C3. Traceable — immutability, history, cascade `[runs: TK]`
- C3.1 A trusted claim MUST NOT be edited after admission, for any reason, including typos. A different statement is a different record; relation is declared by `supersedes` or `restates`. `[planned: restates as a write]`
- C3.2 An assumption MAY be edited while open. Once promoted or closed, its statement is part of the record.
- C3.3 Deletion MUST be impossible at the storage layer, including for administrators. The identifier sequence of a ledger MUST be monotonic and never reused.
- C3.4 Every event on a record (created, updated, promoted, demoted, retired, rechecked) MUST be appended to history. No record carries a mutable status field. Status MUST be computed at read time from history and premises.
- C3.5 If any premise of a trusted claim is demoted, retired, or has fallen itself, the claim MUST read as needing review, with the fallen premises named. Queries for standing trusted claims MUST exclude records whose premises have fallen. The machine MUST NOT demote a claim on its own; demotion is a named move (C2.5).
- C3.6 Retiring a principle MUST list every trusted claim standing on it.
- C3.7 A chain query MUST walk from any record down to its principles and facts, marking each link as standing or fallen.

### C4. Traceable — hierarchy of ledgers `[planned: multi-level; runs: single ledger]`
- C4.1 Ledgers are ordered (personal → team → organization). A claim enters the upper ledger only with a basis pointing to its trusted record in the ledger immediately below. No route skips a level.
- C4.2 Each ledger keeps its own identifier sequence; equal suffixes across ledgers mean nothing. The link between levels is the basis field only.
- C4.3 A claim lives in exactly one ledger per level.
- C4.4 A demotion in an upper ledger cascades automatically to every record its basis chain reaches below, under the upper owner's name, with reason "cascade from <id>".
- C4.5 A demotion in a lower ledger raises a flag upward; records above read as assumptions until the upper owner moves.
- C4.6 A conflict between two trusted records is resolved by the owner of the nearest common upper ledger, by a named move; level decides who resolves, not which is right.
- C4.7 A lower ledger's principle set MUST contain its upper ledger's principle set.
- C4.8 Co-audit is a named check recorded outside the ledger, append-only, pointing to record identifiers, changing no status.

### C5. Enforced at machine speed — continuous check `[runs: TK (gates); planned: continuous checker over the knowledge ledger]`
- C5.1 The machine MUST check on write events, not on a schedule.
- C5.2 Exact violations (record with no move as cause; basis pointing to a fallen record; unreachable citation; mover not holding the role at move time; same name on two adjacent records in a basis chain) MUST be reported separately from heuristic candidates.
- C5.3 The machine MUST NOT change status or write to the ledger. It raises flags.

---

## 6. Part D — Conformance

### D1. Levels of claim
- D1.1 **Self-declared**: the implementer runs the suite in D2 and publishes results. Claim form: "conforms to OrgSov v0.2, Part A" (or Part B, Part C, or any combination).
- D1.2 **Verified**: the suite is run by a party independent of the implementer and the operator, and the evidence in A4, B5, C3 and D3 is read by that party.
- D1.3 An implementation MAY claim conformance to any Part at v0.2, listing which `[planned]` clauses it also meets. `[open]` clauses are excluded from every claim.
- D1.4 The mark **Sovereign Organization** MAY be used only by an organization that meets Part A, Part B and Part C at level D1.2, with a D3 record carrying measures. The mark is always followed by the standard and version.
- D1.5 Names, marks and the conformance suite are held by Ankayma (UAE). Any implementation, by anyone, may claim conformance by passing the suite; no license from Ankayma is required to build.

### D2. Test suites `[runs: Part B, Part C; planned: Part A suite as a published set]`
- Part A: request with an agent as approver → refused and recorded; self-approval → refused and recorded; path after expiry → closed with no action; enumeration of other nodes from a compromised node → empty; path proof → no third party on the path; edit or delete of a ledger record by the operator → impossible; third-party read of the ledger without the operator → succeeds; revocation by a named human → path closed and recorded.
- Part B: the fixed CJCM test set — effect with cause, without cause, with expired cause, with scope mismatch, self-approved — MUST yield the exact V(w), and yield it again on re-run.
- Part C: the nine-step scenario and gate tests: assume → admit refused (USE_PROMOTE) → near-duplicate stopped → promote with source → chain readable; principle added → derivation admitted → principle retired lists dependents → dependent reads needs_review → new admit on fallen premise refused (PREMISE_NOT_T). Plus: agent as signer refused; restatement of an open assumption without a new exit refused; retire twice; recheck on a derivation refused.
- Every suite MUST be runnable by the implementer against their own agent; passing with one agent says nothing about another.

### D3. Organizational evidence record `[planned as a form; the conditions are public]`
An organization claims adoption by producing, per deployment, a record with:
1. The declared scope per zone (A6): which resources are reachable only through the access layer.
2. The four insurability conditions and whether each holds: loss has a ceiling; ceiling stated in advance; grants tamper-proof and third-party monitored; independently audited and tested in reality.
3. Before/after measures:
   - agent freedom: number of agent types operating lawfully inside zones; agents that passed D2 against this deployment;
   - capability used: share of effects in reversible zones that run without a human in the loop; request-to-result time;
   - risk under control: paths opened without a grant (must be 0); irreversible effects run without a cause (must be 0); incidents exceeding a zone ceiling (must be 0); claims entering the knowledge ledger without basis (must be 0).
4. The names of the signer and of the independent reader.

A record with measures is a trusted claim; a record without is an assumption.

---

## 7. Reference implementations (what runs today)

| Part | Implementation | Runs | Not yet |
|---|---|---|---|
| A | Ankayma (ankayma.com), reference deployment of the access layer | blind private mesh (WireGuard, zero trust), hardware-bound human approval, tamper-proof third-party-monitored grants, path proof ("vendor in path: no") | ceiling as a recorded field (A1.2); k-of-n (A2.4); continuous checker (A5); scope declaration as a record (A6); refusal records in the ledger (A4.1) — to be confirmed by the author |
| B | Cause-Justified Change Monitoring (CJCM), github.com/baotnq/cause-justified-change-monitoring, Apache-2.0 | cause channel, V(w) exact set difference, off-path, deterministic, fixed test set, alerts schema and JSONL export | on-path admission; roll-up (B4) |
| B | Realtime settlement audit on a public venue record (Kalshi; 15.3M settled markets) | invariant applied to a public ledger, anomaly classes recorded, forward-only dispute trail | event-level metrics; second venue |
| C | T-knowledge system (t-knowledge-system), Apache-2.0 | 26 operations including assume/admit/promote/demote/retire/recheck, entry/chain/open_items/ledger, gates USE_PROMOTE, PREMISE_NOT_T, SIGNER_IS_AGENT, RESTATE_TAIL, near-duplicate stop; storage-level immutability; status at read | restates as a write; OAuth; multi-ledger hierarchy and sync (C4); continuous checker over the knowledge ledger (C5) |

---

## 8. Not specified

Storage engine; transport; mesh technology; API or tool names (MCP or otherwise); UI; number of ledger levels and their names; identifier format; check cadence; catalogue of heuristic anomaly patterns; numeric thresholds, including grant lifetime and k in k-of-n; choice of agent or model; whether the model runs locally or with a provider; which resources an organization places behind the access layer (A6 requires only that the choice is declared). Any of these may differ between conforming implementations.

---

## 9. Relationship between the parts

One invariant governs all three: every change of state has a named, authorized cause, recorded where it cannot be edited, checked continuously off the write path. In Part A the state is *reachable*; in Part B it is *changed*; in Part C it is *treated as true*.

A grant in Part A may serve as a cause in Part B for effects within its scope. A trusted claim in Part C may serve as the cause of a decision in Part B. A grant in Part A may be recorded as a trusted claim in Part C. Part A says who may reach; Part B says what was done; Part C says what was believed. Together they let a third party reconstruct any agent action from its path, its cause and its premises.

---

## 10. How the standard connects to the thesis

| Essay step (public anchor) | Clause |
|---|---|
| Risk 1 — AI control is isolating what cannot be undone ([`/risk/#wrong-axis`](https://baotrinh.com/risk/#wrong-axis)) | A1 isolated, B1 reversibility |
| Risk 2 — Undone means the loss can be recovered ([`/risk/#unit-money`](https://baotrinh.com/risk/#unit-money)) | B1 |
| Risk 3 — The AI acts; the human behind it pays ([`/risk/#framework-runs`](https://baotrinh.com/risk/#framework-runs)) | A2 granted, B2 cause channel |
| Risk 4 — When that human cannot pay, it rolls up ([`/risk/#principal-broke`](https://baotrinh.com/risk/#principal-broke)) | B4 roll-up |
| Risk 5 — Controlled means someone will insure it ([`/risk/#insurance-test`](https://baotrinh.com/risk/#insurance-test)) | D3 evidence record |
| Risk 6 — The only new thing is enforcement at agent speed ([`/risk/#whats-new`](https://baotrinh.com/risk/#whats-new)) | A3 bounded life, A5, B3 invariant checked continuously |
| Risk 7 — Adopting it is a calculation ([`/risk/#the-choice`](https://baotrinh.com/risk/#the-choice)) | D3 before/after measures |
| Speed 1 — AI enablement is enabling claims you can trust ([`/speed/#enabling-trust`](https://baotrinh.com/speed/#enabling-trust)) | C1 three classes |
| Speed 2 — A claim becomes knowledge with truth, trust, traceable ([`/speed/#three-t`](https://baotrinh.com/speed/#three-t)) | C1, C2, C3 |
| Speed 3 — The AI proposes the truth; a human signs the trust ([`/speed/#propose-and-sign`](https://baotrinh.com/speed/#propose-and-sign)) | C2 |
| Speed 4 — The more names sign a claim, the more it enables ([`/speed/#trust-compounds`](https://baotrinh.com/speed/#trust-compounds)) | C4 hierarchy |
| Speed 5 — Sovereignty means demoting what no longer holds ([`/speed/#demote`](https://baotrinh.com/speed/#demote)) | C2.5, C3.5 |
| Speed 6 — The new thing is knowledge at machine speed ([`/speed/#machine-speed`](https://baotrinh.com/speed/#machine-speed)) | C5 |
| Speed 7 — T-knowledge is the cause behind every decision ([`/speed/#cause-of-decisions`](https://baotrinh.com/speed/#cause-of-decisions)) | B2.5 |

One principle underlies all three parts: **the agent is an owner with zero capital.** Nothing an agent produces — a path, an action or a claim — passes a gate until a human with real capital (money in Parts A and B, reputation in Part C) puts that capital behind it.

---

## 11. Known limits (declared, not hidden)

- Part A governs the access layer only. Connections the organization leaves outside it (A6) are not covered; the standard requires only that they are declared.
- Two approvers can collude at k = 2. The standard raises the cost; it does not remove the possibility.
- Physical possession of a device that holds a hardware identity is outside Part A.
- A valid grant used for a harmful effect is a Part B matter, not a Part A matter.
- The top-level ledger owner has no checking channel inside the ledger; the channel, if any, is outside it.
- Two owners in the same basis chain have a correlated blind spot; flags and cold spot checks read the pattern, they do not prevent a single case.
- The source specifications have been derived and reviewed by one person in one loop; they have not been co-audited. Until they are, an outside reader reads this standard as an assumption. Challenges are welcome as public issues on this repository; each closed issue is a recorded round of co-audit.
- The effectiveness of the hierarchy (C4) is observable only in operation; thresholds for team and organization ledgers are not set.

---

## Appendix A — Source documents (normative until v1.0)

- Sovereignty T-Knowledge System (base specification: single ledger, Principle List P.1–P.9, labels).
- T-ledger phân cấp, 2026-09-04 (hierarchy of ledgers, cascade, co-audit, machine checks).
- spec-admit-assume-promote-19-09-26 and SCHEMA.md (admission, assumptions, promotion; five tables).
- Cause-Justified Change Monitoring README (cause channel, invariant, test set).
- Public essays: "Control is a gate on what cannot be undone" (risk); "Knowledge sovereignty: truth · trust · traceable" (speed), baotrinh.com.
- Ankayma platform pages: mechanism description at baotrinh.com/risk/ankayma/; architecture and honest limits at ankayma.com.
- Access sovereignty definition and invariants: author's working notes, 4 and 10 October 2026.

## Appendix B — External standards referenced (informative)

- ISO/IEC 42001:2023 — AI management system; harmonized structure clauses 4–10; Annex A controls.
- ISO/IEC 27001:2022 — Information security management; Annex A controls on access, privileged access, logging, monitoring.
- NIST AI RMF 1.0 (January 2023) — Govern, Map, Measure, Manage.
- NIST SP 800-207 — Zero Trust Architecture; policy enforcement point and policy information point roles used by Part B.
- IIA Three Lines Model (July 2020) — roles of management, risk functions and internal audit.

## Appendix C — Changelog

Kept in [CHANGELOG.md](CHANGELOG.md).
