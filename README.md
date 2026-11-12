# OpenClaw Multi-Agent Starter (`openclaw-multi-agent-starter`)

> **Your agents can think. The gap is the wiring** — roles, least-privilege tool bindings, 3-tier memory separation, deterministic handoffs, and the guardrails that stop a crew from wandering.

This repository contains the free open-source starter templates extracted from a live 13-agent production OpenClaw fleet (`rigel-1`, running `<$0.80/day` across OpenRouter + Google Vertex Flash/Argon models).

---

## Included Free Starter Files (`examples/`)
- **[`examples/01-role-map-starter.md`](examples/01-role-map-starter.md):** The 3-seat starter crew map (`Coordinator`, `Builder`, `Verifier`), hard *Never Touches* boundaries, and the 3 role anti-patterns to ban immediately.
- **[`examples/04-handoff-contract.md`](examples/04-handoff-contract.md):** The File-Pointer Brief Rule (`>15` lines go to disk), the 4-Field Handoff Card, and the mandatory **3-Bucket Truth Footer** (`Verified` / `Carried Notes` / `Stated Unverified`).
- **[`examples/06-failure-modes.md`](examples/06-failure-modes.md):** The 5 ways multi-agent setups actually rot in production — and the exact one-line fix for each.

---

## Quick Preview: The 5 Ways Multi-Agent Setups Rot

| # | Failure Mode | Symptom in Logs / Transcripts | Root Cause | Exact Fix Line |
|---|---|---|---|---|
| **1** | **Silent Stale Session Pins** | Nightly cron or wake fails with `404 This model was not found` weeks after `openclaw.json` migration | Per-session SQLite state or a cron job's `payload.model` still holds a retired model ID | Audit all sessions via `session_status` (`model: default`) and inspect `openclaw cron get <id>` for stale `payload.model` overrides. |
| **2** | **Deferred-Tool Discovery Loops** | Worker burns 5–7 calls on `tool_search` / `tool_describe` and times out before writing its file | Enabling `tool_search`/`tool_describe` on a non-`exec` agent flips it into Deferred Schema Mode | Keep `tool_search` and `tool_describe` in `tools.deny` on non-`exec` crew agents so `tools.allow` schemas project directly as 1-call tools. |
| **3** | **Compound Scope Inflation** | Stage 1's *'one of the most common'* becomes Stage 2's *'#1 blocker'* and Stage 4's overstated revenue table | Downstream stages trust upstream prose summaries instead of checking raw evidence files and re-deriving math | Require the Verifier seat to audit Stage 1 quotes against `00-live-search-raw.json` and recompute every financial row from per-unit formulas. |
| **4** | **Single-Provider `429` Cascade** | Resident agent aborts after 9 retries (`RESOURCE_EXHAUSTED` or `120s` idle timeout) | Strict session `/model` override bypasses `model.fallbacks`, or all fallbacks sit on the same provider | Set the target model as `model.primary` in `openclaw.json` with a cross-provider fallback chain and clear the session override (`model: default`). |
| **5** | **Hub-and-Spoke Bottleneck** | Orchestrator turn hits 2-minute timeout waiting on 4 sequential stages in a single cell | Orchestrator relays massive inline prompts and runs slow CLI subprocesses inside a 10s guest budget | Use File-Pointer Briefs, run independent stages in parallel via `Promise.all`, and enforce `<=2` tool calls per stage. |

---

## Want the Full 14-File Production Loadout & Pro Fleet Kit?

The complete **OpenClaw Multi-Agent Loadout & Guardrail Pack (`v1.0.0`)** includes:
- **Starter Rung (`9` files):** Adds `00-README-start-here.md` (20-minute quickstart), `02-tool-bindings.md` (full least-privilege `tools.allow`/`tools.deny` matrix + Code Mode vs. Standard Tool Mode config JSON), `03-memory-scaffold.md` (3-tier memory architecture + `160k` context ceiling guard), and `05-guardrail-checklist.md` (10-point pre-flight check).
- **Pro Fleet Kit (`14` files):** Adds `07-fleet-blueprint.md` (Resident vs. On-Demand pod swimlanes for Trend-to-Income, Media Production, and Engineering), `08-gate-wiring.md` (4-gate Shift-Left verification wiring), `09-escalation-routing.md` (One-Hotline rule + quiet-hours routing diagram), `10-hardening-pass.md` (20-point fleet hardening scorecard), and `11-rollout-sheet.md` (one-page go-live & instant rollback runbook).

---

## Author & License
- **Published by:** **[Phyrex](https://phyrex.net/)** *(Software & Systems Development, Implementation, and Automation)*
- **License:** Free starter files in this repository are MIT-licensed (`LICENSE`). Independent operator template pack for OpenClaw; not affiliated with or endorsed by the OpenClaw Foundation.
