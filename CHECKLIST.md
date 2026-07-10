# CHECKLIST

## Pre-flight — before writing a word

Do not draft until you can answer these. Ask the user (in one batch) for anything missing.

- [ ] **Genre chosen** and it's a *single* genre (Tutorial / How-to / Reference / Explanation / Incident-Postmortem). See `GENRES.md`.
- [ ] **Reader named**, with an explicit statement of what they already know.
- [ ] **Goal stated** — what the reader can do or understand afterward.
- [ ] **Scope bounded** — what's in and what's explicitly out.
- [ ] **Sources of truth identified** — the repos/files/docs/command-outputs that ground the claims. If documenting a system, you've *read it*, not recalled it.
- [ ] **Outline proposed** and (for non-trivial docs) approved.

## Post-draft — self-review before declaring done

Read your own draft against this. Fix what fails; report honestly what you couldn't verify.

### Truth
- [ ] Every command, flag, path, version, field, and output is grounded in something you actually read or ran — none invented or assumed-typical.
- [ ] Inferences are marked as inferences ("likely…", "this suggests…"), not stated as fact.
- [ ] No external sources used beyond what the user provided/authorized.
- [ ] Causal claims are real causation, not correlation; the tempting wrong story is named and dismissed where relevant.

### Genre discipline
- [ ] The document stays in one genre — no theory dumped into a tutorial, no story told in a reference.
- [ ] Structure matches the genre template in `GENRES.md`.
- [ ] Cross-links point to other docs for content that belongs in a different genre.

### Reader fit
- [ ] Nothing is explained that this audience already knows; nothing load-bearing is left unexplained.
- [ ] Every new term is defined just-in-time, the first time it matters.
- [ ] Jargon-heavy output (errors, logs, specs) is followed by a plain-language translation.

### Craft
- [ ] For investigative docs: the reasoning path is shown, **including at least one disproven hypothesis and the re-model** (if the real investigation had one).
- [ ] Each idea uses the right representation (table / diagram / callout / code / prose) — comparisons aren't buried in prose; arguments aren't shredded into bullets.
- [ ] Sections are ordered by progressive disclosure — no fact is needed before it's given.
- [ ] Investigative/explanatory docs end with **transferable principles**, not just "we fixed it."
- [ ] Terminology is consistent — one name per concept throughout.

### Finish
- [ ] There's a short summary/TL;DR up top for anything longer than a screen.
- [ ] References/links to primary sources are included.
- [ ] Formatting, tone, and language match the surrounding docs and the request's language.
- [ ] You've stated to the user what, if anything, you could not verify.
