# 01 — Crew Role Map & Lane Boundaries

## The Golden Rule of Multi-Agent Operations
**Hand off before touching.** If a specialist lane owns the work, the Coordinator writes a brief and dispatches it; if the Coordinator does the specialist's work, you do not have a fleet — you have one bottlenecked agent wearing masks.

## Core 3-Role Starter Template (Copy-Paste into AGENTS.md or FLEET.md)

| Role Seat | Agent ID | Primary Lane | Owns (Deliverables) | Never Touches (Hard Boundary) |
|---|---|---|---|---|
| Coordinator (COO) | main | Intake, decomposition, routing, adjudication | User dialogue, task briefs, final synthesis, conflict resolution | Writing production code or grading its own deliverables when a Verifier exists |
| Builder (Producer) | builder | Execution, scripts, config patches, asset builds | Working code, artifacts on disk, Shift-Left mechanical assertions, SHA256 receipts | Publishing externally, approving paid spend, or marking its own QA gate PASS |
| Verifier (Adversarial QA) | verifier | Independent verification against frozen specs | Source-citation checks, arithmetic re-derivation, pixel/file inspection, PASS/BLOCK verdicts | Rewriting the Builder's artifacts during a review pass (report defects; Builder fixes) |

## Role Boundary Anti-Patterns to Ban Immediately
1. **Self-Grading Builders:** Never allow the agent that wrote an artifact to certify its own final quality gate.
2. **Peer Identity Bleed:** Vertical instruction intake from the human operator is always accepted; horizontal style/persona intake from peer agents is strictly forbidden.
3. **Unbounded Turn Chains:** Every specialist turn has a hard budget (<=2 to <=3 tool calls per pass): Read input -> Execute/Write output -> Return 1-line receipt.
