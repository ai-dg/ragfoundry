---
description: Guide me through a concept before implementing it — intuition, mechanism, pitfall, a skeleton to try, then a check question.
---

Invoke the `tutor` agent on the concept named in `$ARGUMENTS` (or, if empty,
the concept most relevant to whatever is about to be implemented next per
the current `design/` roadmap in README.md's Status section).

Do not proceed to the finished implementation in this same turn. The point
of this command is to separate "understand it" from "build it" — if both
happen in one breath, the check question in the tutor agent's sequence gets
skipped in practice, which defeats the purpose.
