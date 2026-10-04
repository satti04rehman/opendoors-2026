# LESSONS — Open Doors 2026 application

> Evidence-based, reviewable. A single failure is not a rule — accumulate, then let
> future Masters weigh it. Last updated: 2026-09-28

---

## 1. Re-downloading a completed file truncated it

**What happened:** `curl -sL -o file.pdf <url>` returned nothing visible and the shell
tool killed the command at its 120s timeout — but the download had actually **finished
and written a 913,408-byte file**. I read the empty output as failure, re-ran the
download with `--max-time 20`, and **overwrote the good file with a truncated
113KB one.**

**Root cause:** treating a *tool-level* timeout as a *transfer* failure. The two are
different events.

**Rule now:** after any interrupted download, **inspect the artefact on disk first**
(`stat -c%s`, header bytes, `%%EOF` marker) before re-running. Never blindly re-run a
download that may already have succeeded.

**Also learned:** a PDF is only valid if it ends with `%%EOF` in the last few KB *and*
has a trailer/`startxref`. `file` reporting "PDF document" is **not** sufficient — a
truncated file also reports as a valid PDF. `pdftotext` (poppler) is available on this
machine and is a better check than `file`.

**Open item:** `od.globaluni.ru` served inconsistent sizes across attempts
(913,408 / 866,865 bytes) and never produced a complete file via CLI. The Stage 2 demo
PDF must be downloaded in a browser. Recorded in `team-context.md` §4.

---

## 2. A home-directory `team-context.md` belonged to a completely different project

**What happened:** `~/team-context.md` exists and the natural reflex was to append the
scholarship work there. Reading it first showed it documents **Sony Xperia PUBG display
tuning** across seven phases. Completely unrelated.

**Rule now:** `AGENTS.md` §4 warns about this and the warning is real. **Always read a
discovered `team-context.md` before writing to it.** Verify it describes the current
task. A state file found in an ancestor directory is a common trap when several
projects run in parallel from one home directory.

**Consequence:** scholarship state went to its own `~/opendoors-2026/team-context.md`
with a pointer in `memory/projects.md`. The PUBG file was not touched.

---

## 3. A weak CGPA is a ceiling, not a starting point — do the arithmetic

**What happened:** Abdul's 2.7/4.0 looked like a soft disadvantage worth "compensating
for" in a letter. The arithmetic said otherwise: with ~38 of ~44 courses complete,
`(38 × 2.7 + 8 × 4.0) ÷ 46 = 2.93`. **3.0 is mathematically unreachable**, which
permanently closed MBZUAI, KAUST, Türkiye and Korea before any application effort.

**Rule now:** when a hard numeric gate blocks a route, **compute whether it is
reachable** before advising "improve your grades and re-apply." If it is not reachable,
say so immediately and redirect effort to routes with no published floor. Effort spent
chasing an impossible threshold is the expensive mistake.

**Companion lesson:** at the same time, do *not* over-generalise. Open Doors publishes
**no CGPA floor at all** — so the same 2.7 was an asset there. Gates are
scheme-specific and must be checked per scheme, never assumed globally.

---

## 4. Separate what a *test* gates from what a *portfolio* gates

**What happened:** the instinct was to treat the HAT aptitude test as the main hurdle.
It is not — the HAT is largely independent of undergraduate grades, sits in two
separate routes, and can be re-sat. It is the only genuinely *controllable* lever in
the whole application.

**Rule now:** when a candidate has a fixed weakness (transcript, age, nationality) and
one adjustable input (test score, portfolio evidence, deadline), **rank by
controllability**, not by prominence. The unfixable thing sets the boundaries; the
fixable thing is where effort pays.

---

## 5. Check the real platform for what a competition actually scores

**What happened:** the obvious source — the competition's own official demo paper —
existed and had been assumed unavailable. The published **assessment criteria for the
advanced tasks** turned out to be a usable rubric for calibrating depth of answer.

**Rule now:** before building a preparation plan, spend one search on the *primary
document* the organiser publishes for candidates. Aggregators confidently carry numbers
("90 tasks in 60 minutes") that trace to nothing official — one such figure turned out
to be `NOT VERIFIED` and was struck from the plan rather than repeated.
