# engineering-writer

A [Claude Code](https://claude.com/claude-code) skill for **senior-level engineering writing**.

Most engineering writing prompts are template-fillers tuned for one genre (usually a tutorial). This skill is built for the hard cases — root-cause write-ups, deep "how it works" explainers, reference docs for complex systems — where the goal isn't just recording *what happened* but teaching the reader a **transferable mental model** they can reuse on a different problem next time.

## What it does

- **Picks the right genre and holds the line.** Tutorial, How-to, Reference, Explanation, or Incident/Postmortem — never blended on one page. The first four are the [Diátaxis](https://diataxis.fr/) quadrants; the fifth is added because incident/postmortem reasoning is where senior craft matters most and Diátaxis has no home for it.
- **Grounds every claim in real sources.** Commands, flags, versions, outputs come from what was actually read or run — not from what's "typical." Explicit anti-hallucination guardrails.
- **Shows the reasoning honestly.** For investigative docs it narrates the real path — including hypotheses that got *disproven* and forced a re-model. The thinking is the payload; the commands are the vehicle.
- **Clarify-first workflow.** Pins down genre, reader, goal, and scope before drafting; proposes an outline for approval; self-reviews against a checklist before finishing.
- **Chooses the right representation per idea** — tables for comparisons, diagrams for flows, callouts for definitions/warnings, code blocks for commands, prose for arguments.

## Files

| File | Role |
|---|---|
| [`SKILL.md`](./SKILL.md) | Identity, core principles, workflow, guardrails |
| [`GENRES.md`](./GENRES.md) | The 5 genres — when to use each + a structure template |
| [`CRAFT.md`](./CRAFT.md) | 10 senior-level techniques (audience calibration, just-in-time concepts, evidence-grounding, honest reasoning narrative, representation choice, …) |
| [`CHECKLIST.md`](./CHECKLIST.md) | Pre-flight clarify checklist + post-draft self-review |

## Install

Clone into your Claude Code skills directory:

```bash
# Global (available in every project)
git clone https://github.com/mayooot/engineering-writer.git ~/.claude/skills/engineering-writer

# Or per-project
git clone https://github.com/mayooot/engineering-writer.git .claude/skills/engineering-writer
```

## Use

It triggers automatically when you ask Claude to write or heavily rewrite a technical document, or invoke it explicitly:

```
/engineering-writer document how the request-retry middleware works, sources: src/middleware/retry.ts
```

Point it at real sources — it reads them first, then writes.

## License

[MIT](./LICENSE)
