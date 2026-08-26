# Verification discipline

> Loaded whenever a claim is made about behavior, a bug fix, a library
> default, or a measurement.

## The rule

A claim about what code *does* is only as good as the command that proves
it. Before stating one:

1. **Locate the exact mechanism** — the line, the default, the config value —
   not an approximate memory of it.
2. **Run something** that would fail if the claim were wrong. A test, a
   REPL check, a log inspection, a decomposed calculation.
3. **Show the actual output**, not a paraphrase of expected output.

## Patterns from this project's own history

- *"Chroma returns a similarity score"* — wrong, and stated three times
  before it was checked. The fix wasn't reading the docs harder, it was
  running `scripts/inspect_metric.py` against the live collection and
  looking at the numbers.
- *"The tests pass"* said without running them, once, led to shipping a
  guardrail that silently accepted everything — `if not best_results == 0`
  is always `True` in Python; nobody caught it by reading it twice, one
  `pytest` run caught it instantly.
- *"This should fix the duplication bug"* — the fix needed a `before`/`after`
  vector count to be a fix at all, not just a plausible-looking diff.

## What "expensive to verify" doesn't excuse

If verification needs a live LLM call, real API spend, or a slow build:
say so, propose the cheapest check that still proves the claim, and ask
before running it. It does not excuse skipping verification, only
negotiates its form.

## The tell that verification was skipped

Language like "should work," "this fixes it," "normally this returns X" —
all three are a claim dressed as a fact. Replace with the actual command
and its actual output, or explicitly say "unverified, here's why."
