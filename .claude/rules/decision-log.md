# Decision log

> Loaded whenever a new architectural or design decision is made — a new
> component, a changed default, a chosen algorithm, a rejected alternative.

## Where decisions live

`design/<topic>.md`. One file per coherent area (guardrail, retrieval,
evaluation, observability...), not one giant log. Each file is written so
that reading it out loud in an interview takes 60–90 seconds per decision.

## The format, every time

**Problem** — what was actually broken or missing, stated concretely enough
that someone could reproduce it. Not "needed better X" — what specifically
went wrong, for whom, under what condition.

**Decision** — the one-sentence choice. No hedging.

**Why** — the mechanism that justifies it, not the intent. "Because it's
simpler" is an intent. "Because a single per-chunk threshold can't
distinguish wrong-domain from adversarial phrasing, and this does" is a
mechanism.

**Result (measured)** — a number, a log line, a test, a script output. If
there's no measurement, that's worth stating honestly rather than skipping:
"not yet measured — here's how I would."

**Cost** — what this doesn't solve, what it's calibrated for and stops
working outside of, what a reviewer should push back on. A decision
without a stated cost reads as either dishonest or unexamined.

## Example that meets the bar

See `design/guardrail.md` — the threshold section is the reference example:
concrete problem, one decision, the mechanism (squared L2 vs. cosine,
verified in code), measured clusters (0.43–0.73 vs. ~1.31), and an explicit
list of three things it doesn't catch, one of them verified by running
actual injection attempts against it.

## What doesn't belong in the log

Anything reversible and cheap to redo doesn't need this treatment — a
variable rename, a formatting choice. This is for decisions someone would
reasonably ask "why?" about in a technical interview.
