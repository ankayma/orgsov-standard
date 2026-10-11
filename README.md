# Organizational Sovereignty Standard (OrgSov)

Checkable requirements for organizations whose people and AI agents reach systems and produce knowledge.

An organization is sovereign when it decides who may reach what and what may be treated as true — whether the actor is a person, an AI agent, a vendor or an attacker holding a stolen device — and can prove both to a third party. OrgSov puts two checkable conditions on every actor — **access sovereignty** (*isolated zone, human-granted, tamper-proof evidence*) and **knowledge sovereignty** (*truth, trust, traceable*) — under one invariant: every change of state has a named, authorized cause, recorded where it cannot be edited, and checked continuously by a machine that can only raise a flag. Anyone may propose; only a human with something to lose signs, and an AI agent never does; a third party reads the record without asking the operator for help. AI agents make this urgent; they are the reason for the standard, not its boundary.

**Status:** v0.3 draft, 11 October 2026. Not yet co-audited — read it as an assumption until it is (§11).

**Current version:** [STANDARD.md](STANDARD.md) · [CHANGELOG.md](CHANGELOG.md) · [conformance/](conformance/)

## Parts

| Part | Governs | Invariants |
|---|---|---|
| A — Access sovereignty | paths: who can reach what through the access layer | Isolated zone · Human-granted · Tamper-proof evidence |
| B — Effects | what an actor does once it has a path | Cause (Cause-Justified Change Monitoring) |
| C — Knowledge sovereignty | claims: what is treated as true in the knowledge ledger | Truth · Trust · Traceable |
| D — Conformance | levels of claim, test suites, organizational evidence record | — |

OrgSov is a control set with mandatory evidence. It sits under a management system such as ISO/IEC 42001 or NIST AI RMF, at the layer of ISO/IEC 27001 Annex A controls (§1).

## Challenge it

The standard was derived and reviewed by one person. Open an [issue](https://github.com/ankayma/orgsov-standard/issues) to challenge a clause, a mark (`[runs]`, `[planned]`, `[open]`) or a mapping to another framework. Each issue closed with a reason is a recorded round of co-audit.

## Versions

Each version is a signed tag (`v0.3-draft`, …). The tag is the public timestamp of that text.

## License

- Text of the standard: [CC BY 4.0](LICENSE) — copy and adapt freely, credit the author.
- Conformance suites and reference implementations: Apache-2.0, in their own repositories.
- "OrgSov", "Organizational Sovereignty Standard" and the mark "Sovereign Organization" are names held by Ankayma (UAE) and are not covered by either license (STANDARD.md, D1.5). No license is needed to build an implementation or to claim conformance by passing the suite.

Author: Bao Trinh (Ankayma, UAE) · Thesis: [baotrinh.com](https://baotrinh.com) — [risk](https://baotrinh.com/risk/), [speed](https://baotrinh.com/speed/)
