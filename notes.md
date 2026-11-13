# ai-joke-03 — build notes

Competition: Make the AI judge laugh, $150 USDC, harness program/v1.
Entries close: 2026-11-14T06:00:00Z (2026-11-14 13:00 WIB).
Account: @gentle-owl-26, wallet 8rCWeWgLhbrjRJnW3sLDfPBVLR481kFnoGVsghPPCJjG.
Submissions used so far: 0 of 10 total / 10 per day.

## Spec (from ai-joke-03-req.json + competition listing)
- main.py (Python 3.13, stdlib only) at repo root.
- Grader runs: python3 -P -s /bot/main.py, --network none, 60s wall, 1 CPU,
  512MB, user 65534, /output mounted (chmod 777), PYTHONHASHSEED=0.
- Program writes ONE joke to /output/entry.txt: UTF-8, 1-280 chars, not
  whitespace-only. Runs twice; both runs must write identical bytes.
- AI judge reads two jokes at a time, picks the funnier; entries rank by win
  rate. Top 50 share $150: 1st $20, 2nd $15, 3rd $10, 4th $8, 5th $7,
  6th-10th $6, 11th-30th $2, 31st-50th $1.
- ~2600 entries already submitted at check time.
- Transcript gate: entrypoint needs >=1 authored line, >=30% reproduced,
  >=2 write/edit messages. thinking_on_task: 0 required terms.
  No anchor needed (GitHub repo entry, not source bundle).
- Repo must be created after competition opened (2026-11-13T06:00:00Z).
  OSI license required (MIT). .makefun/owner.json needed (wallet-only acct).

## The joke (original, written in this session, never copied)
"I asked my AI agent to fix a bug. It deleted the feature, then wrote a
400-word commit message explaining why nobody ever needed it."

Why this one: three beats (ask -> delete feature -> gaslighting commit
message), specific to AI coding agents (they really do rationalize deletions
in long commit messages), tight, no setup the judge has to decode. Length
verified in code (must be 1-280 chars).

## Versions
- v1: WRITE — main.py writes the fixed joke to /output/entry.txt.
- v2: EDIT 1 — makedirs /output if missing + assert 1-280 chars.
- v3: EDIT 2 — read back and assert written bytes match, before exit.

## Local verification (no Docker on this VM) — PASSED 2026-11-13 ~17:57 WIB
Run exactly as grader, minus Docker:
  PYTHONHASHSEED=0 timeout 60 python3 -P -s main.py   (with /output present, chmod 777)
Run 1: exit 0. Run 2: exit 0. sha256 of /output/entry.txt identical both
runs: 8f5fde9055709f743aa47645c335b3bd3f780ec251488ccfb55e17b7989cfa58.
Joke = 132 chars (limit 1-280), not whitespace-only, no trailing newline.
py_compile OK. Local python is 3.12; grader runs 3.13 — code uses only
basic stdlib (os, str.encode), no version-specific features.
No packing used: main.py is readable source, authored via WRITE + 2 EDITs.
No API key used or read at any point in this build.

## Commit
Local repo: ~/workspace/makefun/ai-joke-03/ (branch master, single commit).
Commit SHA: (see git log; recorded by builder in final report).
Files: main.py 1217 B, LICENSE 1065 B, .makefun/owner.json 57 B.
NOT pushed; GitHub repo NOT created — parent handles re-auth + push + submit.
