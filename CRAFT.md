# CRAFT — the senior-level techniques

Genre (`GENRES.md`) decides the *shape* of the document. Craft decides whether it's *good*. These are the section- and sentence-level techniques that separate a senior write-up from a competent one. Apply the ones that fit the genre.

## 1. Calibrate to a declared audience

State who the document is for, near the top, and write to exactly that person.

> Written for: engineers comfortable *using* Kubernetes who have never touched the container-runtime layer. Low-level concepts are explained the first time they appear.

Then hold that line. Don't explain what a Pod is to this reader (they know), but *do* explain what a Linux namespace is (they don't). Every explanation you include or omit should be justified by that one sentence. Guessing the audience wrong is the most common reason a doc feels either patronizing or impenetrable.

## 2. Just-in-time concepts, not a glossary dump

Explain a term **the first time it becomes load-bearing**, inline, right where the reader needs it — not in a glossary they'll never scroll to, and not preemptively three sections early. A short callout works well:

> **What `StartError` means:** the Pod was scheduled and the image is ready, but the runtime failed to *create* the container. So the problem is on the node's runtime — not scheduling, image, or network.

Introduce exactly enough to keep moving. Depth goes in a linked Explanation.

## 3. Ground every claim in evidence

A claim without evidence is an opinion. Show the command and the *real* output, then interpret it:

````
```bash
runc --version
# runc version 1.0.0-rc3
```
containerd 1.7 expects runc 1.1.x — pairing it with a 2017 rc3 preview is a severe mismatch.
````

Interpretation without evidence is hand-waving; evidence without interpretation is a data dump. Always pair them. If you didn't run it or read it, don't claim it.

## 4. Translate jargon into plain language

After any dense error, log line, or spec, add a "in plain terms" translation. The raw text proves it; the translation makes it *land*.

> `lstat /proc/1289930/ns/ipc: no such file or directory`
>
> In plain terms: the container tried to join another process's IPC namespace, but that process was already gone. The sandbox died before the workload could attach to it.

## 5. Honest reasoning narrative (the core senior move)

For anything investigative, **the reasoning path is the product.** Narrate it the way it really unfolded:

1. **Symptom** — the exact observed state, verbatim.
2. **Why you looked where you looked** — "the first rule is always read the events and the container state message."
3. **What you found, and what it ruled in or out** — narrow the space deliberately.
4. **The dead end.** State a hypothesis, show the evidence that **disproved** it, and re-model out loud:

   > I assumed the difference was `RuntimeClass`. But the running Pods had *identical* config and worked — that falsified it. Stop and rebuild the model instead of forcing the conclusion.

5. **The turning point** — the observation that reframed everything ("the same error hit unrelated Pods, and the dead PID kept changing → this isn't one Pod's problem, it's the node's runtime").
6. **The fingerprint** — the single decisive piece of evidence that nails the cause.

Showing the wrong turns is not a confession of incompetence — it's the most valuable thing in the document, because it teaches the reader how to *think*, not just what the answer was.

## 6. Separate correlation from causation

Name the tempting-but-wrong causal story explicitly and dismantle it. Readers arrive with the same wrong intuition; addressing it head-on is worth a dedicated line or callout.

> ⚠️ "Resource recovered → the old Evicted pods got cleaned up → a new one started" is the wrong causal chain. Resource recovery and garbage-collection of old records are two independent things.

## 7. Choose the representation that fits the idea

| The idea is… | Use… |
|---|---|
| A comparison across 2+ options on shared dimensions | a **table** |
| A flow, pipeline, state machine, or decision path | a **diagram** (ASCII is fine and diffs well) |
| A definition, warning, or key takeaway | a **callout** (`>` blockquote / admonition) |
| A command and its result | a **code block** with real output |
| A sequence of actions to perform in order | a **numbered list** |
| An argument, rationale, or narrative | **prose** — don't fragment it into bullets |

Two anti-patterns: forcing a comparison into prose (the reader can't scan it), and shredding an argument into a bullet list (the logical connective tissue is lost). Bullets are for genuinely parallel items, not for thoughts that depend on each other.

## 8. Progressive disclosure

Order sections so each one earns the next. Define and *characterize* the problem before diving into internals (is it a scheduling / image / runtime problem?), then narrow. The reader should never need a fact you haven't given them yet. A document that front-loads implementation detail before establishing why it matters loses the reader in the first screen.

## 9. Distill transferable principles at the end

Close investigative and explanatory docs with the reusable heuristics — the part the reader carries to a *different* problem next month.

> Two rules of thumb from this one:
> 1. One error hitting multiple unrelated objects → stop debugging the instance, start debugging the node/service.
> 2. `runc` is only invoked at container *creation*. "Already running" and "starting now" are two different worlds — a broken runtime hits only the second.

Without this section you've written a report. With it, you've written something that makes the reader better.

## 10. Precision in language

- Prefer the specific noun to the vague pronoun. "The kubelet's local admission rejects it" beats "it gets rejected."
- Active voice, present tense for how things work; past tense for what happened in an incident.
- One idea per sentence for load-bearing technical claims. Save the long sentences for connective narration.
- Define acronyms on first use. Be ruthlessly consistent with terminology — pick one name per concept and never drift.
