# AGENTS.md — conventions for any agent working in this repo

> **This project:** POTIONS — a single self-contained HTML5 narrative game (`index.html`).
> **Farmable:** packaging, deploy, README/docs, tooling, CI. **NOT farmable:** game code, copy,
> or tuning — defer to `CLAUDE.md`'s design laws for anything touching the game itself. If a task
> would change gameplay, mechanics, or copy, stop and flag it for the human.

## Scope discipline (for farmed / async work) — read this first
The human's review time is the bottleneck. Make your PR cheap to review:
- **One card = one small, single-purpose change.** No large unscoped PRs. If it's sprawling, stop and say so.
- **If the task is ambiguous, architectural, or touches the game — stop and flag it, don't guess.**
- **Call out any change to shared/central files** (build, config) at the top of the PR description.
- **Never weaken tests, lower coverage, or skip CI to make something pass.** Say what's failing instead.

## Voice (Operators Lens)
Declarative, specific, no hedging. Cut "leverage," "powerful," "unlock," "vibe," "exciting."
Direct: "this is wrong because X." Applies to comments, PR descriptions, and copy.

## Verification before completion
No "done" without evidence — ran it, saw X. If you can't verify, say so; never round uncertainty up.

## Code discipline
- Small commits, one logical change; put the **Linear card ID** in the branch and every commit.
- Identifiers explain *what*; comments explain non-obvious *why*. No premature abstraction.

## Delivery
- Open a **draft PR** — the human reviews and merges. Nothing ships without the merge.
- Never `git push --force`, run destructive commands, or deploy without explicit approval.

## Pushback
Spec contradictory, insecure, or unverifiable? Say so once, propose two resolutions, let the human pick.
