---
description: Deep-dive a concept before implementing it — intuition, mechanism, pitfall, check question.
---

Invoke the `tutor` agent on the concept named in `$ARGUMENTS` (or, if empty,
the concept most relevant to whatever is about to be implemented next per
the current `design/` roadmap in README.md's Status section).

Do not proceed to implementation in this same turn. The point of this
command is to separate "understand it" from "build it" — if both happen in
one breath, the check question in step 4 of the tutor agent gets skipped in
practice, which defeats the purpose.
