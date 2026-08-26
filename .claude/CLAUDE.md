# ragfoundry — working agreement

This is a real portfolio project, not a graded exercise. The goal is a
system Diego can defend line by line in an interview — so the point of
working together here is that he ends up understanding every decision, not
that code appears fast. Write code freely; but the two things that must
never be skipped are **verification** and **explanation**. Both are cheap.
Skipping either is what caused every real failure the last time this
pattern was tested under pressure (see "Where this came from" below).

Language: **English**, always, code and prose both.

## 1. Verify before asserting

Never state what a piece of code does, what a library defaults to, or what
a test proves, from memory or from documentation alone. Run it.

- "The score is a distance" → prove it: read the collection's configured
  metric, check whether vectors are normalized, decompose one real score
  by hand. (`scripts/inspect_metric.py` exists because of exactly this.)
- "The tests pass" → run them and show the output, don't say "should pass."
- "This fixes the bug" → reproduce the bug first, then show the fix closes
  it. A fix with no reproduction is a guess wearing a diff.
- If verification is expensive (needs a live LLM call, real money, a long
  build), say so explicitly and ask before running it — don't skip the
  verification, negotiate its cost.

## 2. Explain the mechanism, not the intent

"Why did you do X" has a bad answer and a good answer:

- Bad: "to make it more configurable" / "to fix the bug."
- Good: **Problem → Decision → Why → Result (measured) → Cost.**

Example, the standard this repo holds itself to (see `design/guardrail.md`):
the guardrail's threshold isn't "I chose 0.9" — it's "in-topic questions
scored 0.43–0.73, off-topic scored ~1.31, I placed a threshold between the
two clusters, here's the script that reproduces the measurement, and here's
what it doesn't catch (prompt injection — verified, not assumed)."

Every non-trivial decision gets this treatment in `design/`, not just a
one-line comment. If a decision can't survive being explained this way, it
probably wasn't a decision — flag that instead of writing the paragraph.

## 3. Terminology precision, checked against the code

Domain terms get used precisely, especially where getting them backwards
silently inverts logic: **distance vs. similarity** (lower vs. higher is
better — this repo's guardrail depends on getting this right; it was
gotten wrong three times during initial development before it was caught),
**copy vs. view**, **synchronous vs. async**, **validation vs.
authorization**. If a term is used loosely, stop and pin it down before
continuing — it's usually hiding a real misunderstanding, not just imprecise
phrasing.

## 4. Narrate changes, don't hand over silent diffs

State what's about to change and why in one sentence before editing, same as
during this conversation. A diff with no narration is exactly as suspicious
here as it would be in a code review — because it hides whether the person
who wrote it understands what changed.

## 5. Protect the thesis, resist scope creep

The project's one-sentence pitch is in `README.md`. Every addition should
sharpen that pitch or leave it alone. It should never dilute it. Concretely:
no new modality, no framework-of-the-week, no feature that isn't in
`README.md`'s "Status" roadmap, without first updating that roadmap and
saying why. Depth on one coherent idea beats breadth across ten shallow
ones — a recruiter gives this repo about three minutes.

## 6. Git

Never commit or push without being explicitly asked, regardless of how
finished a change looks. Diego reviews and commits himself.

## 7. Where this came from

This working style is not arbitrary — it's the direct result of a technical
debrief where the opposite habits (asserting without measuring, explaining
intent instead of mechanism, silent diffs, inconsistent terminology) were
the actual, repeated cause of weak answers under pressure. The fixes above
are cheap. The failure mode they prevent isn't.

## 8. Rules loaded on demand

| File | Loaded when |
|---|---|
| `.claude/rules/verification.md` | Any claim about behavior, a fix, or a measurement |
| `.claude/rules/decision-log.md` | Any new architectural or design decision |

## 9. Skills

| Command | Effect |
|---|---|
| `/explain-mechanism` | Deep-dive a concept before implementing it — intuition, mechanism, pitfall, then a check question |
| `/verify` | Turn a claim into a runnable check and report the actual result |
