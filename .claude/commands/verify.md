---
description: Turn a claim about this codebase's behavior into a runnable check and report the actual result.
---

Take the claim in `$ARGUMENTS` (e.g. "the guardrail rejects off-topic
questions", "the index no longer duplicates on restart", "tests pass
without a .env file") and:

1. State the exact command or script that would prove or disprove it.
2. Run it.
3. Report the actual output, not a paraphrase — paste the real numbers,
   the real test result, the real log line.
4. State plainly whether the claim held, and if not, what it revealed.

If running the check requires something costly (a live LLM call, spending
money, a slow rebuild), say so and propose the cheapest check that still
proves the claim, before running anything.

This command exists because "should work" and "this fixes it" are the two
phrases most responsible for shipping wrong code in this project's history —
see `.claude/rules/verification.md`.
