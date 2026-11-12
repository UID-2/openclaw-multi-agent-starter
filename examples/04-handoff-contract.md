# 04 — Handoff Contract & The 3-Bucket Truth Footer

## 1. File-Pointer Brief Rule (>15 Lines Go to Disk)
Never paste a 100-line specification into an inter-session sessions_send message. Write the specification once to briefs/YYYY-MM-DD-<slug>.md, then send a <10-line handoff message pointing the receiving agent to the exact brief path and expected output file path.

## 2. Standard 4-Field Handoff Card
Every inter-agent handoff message uses four fields:
1. **Objective & Stage:** One sentence naming the stage and target artifact path (crew/<run>/02-spec.md).
2. **Upstream Input:** Exact file path(s) to read (crew/<run>/01-research.md).
3. **Mechanical Acceptance Bar:** Concrete invariants the output must satisfy (0 placeholder tokens, exact section count, ffprobe duration, or unit-economics fee formula).
4. **Turn Budget:** Follow bounded-step rule (<=2 tool calls): 1. Read input. 2. Write output + reply with 1-line receipt.

## 3. Mandatory 3-Bucket Truth Footer (Every Receipt & QA Verdict)
Every stage artifact and QA receipt must close with these three explicit buckets so assumptions never masquerade as verified facts:
- **Verified (with proof on disk):** Exact file paths, byte counts, SHA256 hashes, HTTP status codes, or verbatim source quotes inspected in this pass.
- **Carried Notes (S2/S3 non-blocking):** Known caveats or upstream claims carried forward without independent re-derivation (non-blocking for dry-run, blocking for live publish).
- **Stated Unverified:** Anything out of scope, behind an unconfigured API key, or requiring live market/buyer testing. (An empty Unverified bucket must be earned, never assumed.)
