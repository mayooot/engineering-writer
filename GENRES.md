# GENRES — pick one, hold the line

The most common failure in technical writing is mixing genres on one page. Each genre serves a different reader in a different mindset. Decide which one you're writing, and cross-link to the others rather than blending.

The first four are the [Diátaxis](https://diataxis.fr/) quadrants. The fifth (Incident/Postmortem) is added because it's a distinct, high-value genre that Diátaxis folds awkwardly into "explanation" — and it's where senior reasoning-craft matters most.

## Quick selector

| Reader is… | …and wants to… | Genre |
|---|---|---|
| A newcomer | learn by doing, guided to a first success | **Tutorial** |
| A competent user | accomplish a specific task they already understand | **How-to** |
| Anyone mid-task | look up an exact fact (flag, field, signature) | **Reference** |
| A curious reader | understand *why* something is the way it is | **Explanation** |
| An engineer after an incident | understand what broke, why, and how to reason about it next time | **Incident / Postmortem** |

Two axes help you choose: **practical (doing) vs. theoretical (knowing)**, and **serving study vs. serving work**. Tutorial = doing + study. How-to = doing + work. Reference = knowing + work. Explanation = knowing + study.

---

## Tutorial — *learning-oriented*

A lesson. Takes a beginner by the hand to a concrete, guaranteed success. The reader is learning the *skill*, not solving *their* problem yet.

- **Promise a specific outcome up front** and deliver exactly it. No detours.
- **Every step must work.** A tutorial that breaks halfway destroys trust. Test the path.
- **Minimize explanation.** The reader is learning by doing; deep theory belongs in an Explanation you link to. A one-line "we do this because…" is fine; a three-paragraph digression is not.
- **No choices.** Don't offer "you could also…". One golden path.
- **Concrete over abstract.** Real values, real output the reader can compare against.

**Structure:** What you'll build/learn → prerequisites → numbered steps (each: action → what you should see) → "what you accomplished" → where to go next.

---

## How-to guide — *task-oriented*

A recipe. The reader has a specific goal and enough context to follow along. Serves work, not study.

- **Title is the task**, phrased as the reader's goal: "How to rotate the signing key," "Configure TLS for the ingress."
- **Assume competence.** Skip the teaching; get to the steps.
- **Address the real-world messiness** the golden-path tutorial ignored: variations, "if you're on X do this instead," what to do when it fails.
- **Focus on the sequence of actions**, not on explaining the machinery (link to Reference/Explanation for that).

**Structure:** Goal (one line) → prerequisites/assumptions → ordered steps → verification → common variations & failure modes.

---

## Reference — *information-oriented*

A dictionary. The reader knows what they're looking for and wants it fast and exact. Serves work.

- **Describe, don't instruct or explain.** State what the thing *is* — parameters, return values, fields, flags, error codes, defaults.
- **Accuracy and completeness are everything.** A wrong default or missing flag makes the whole page untrustworthy.
- **Mirror the structure of the code/API.** Consistent, predictable, scannable. Same layout for every entry.
- **Be austere.** No narrative, no opinions, no "you might want to…". Examples are allowed but minimal.

**Structure:** Consistent entries — name, signature/syntax, description, parameters (name · type · default · meaning), returns, errors, minimal example. Alphabetical or grouped-by-module, whichever the reader will scan.

---

## Explanation — *understanding-oriented*

A discussion. The reader wants to understand *why* — the concepts, the design rationale, the trade-offs, how the pieces fit. Serves study, read away from the keyboard.

- **Answer "why," not "how."** Why is it built this way? What alternatives were rejected and why? What are the trade-offs?
- **Make connections.** Relate this topic to others; give the reader a map, not a pin.
- **It's okay to have a point of view** — "this design favors throughput over latency because…". Reference can't; Explanation can.
- **Bound the topic.** An explanation sprawls if you let it. State what it covers and what it doesn't.
- **Don't turn it into instructions.** No steps to follow. If you're telling the reader what to *do*, it's a how-to.

**Structure:** The question/topic → the mental model (often a diagram) → how the parts relate → the key trade-offs and design decisions → boundaries and links to related concepts.

---

## Incident / Postmortem — *reasoning-oriented*

A case study that teaches a **transferable investigation method**. The reader wants to (a) understand what actually happened, and (b) learn how to think when they hit a *different* instance of the same class of problem. This is where senior writing earns its title — see `CRAFT.md` §"Honest reasoning narrative."

- **Lead with a one-paragraph summary** (TL;DR / a "one sentence" callout): symptom, root cause, fix. Busy readers get the whole story in 5 seconds; the rest is the *why*.
- **Narrate the investigation in the order it actually happened** — symptom → what you checked and why → what you found → what that ruled in/out → next move. The *sequence of reasoning* is the lesson.
- **Show the dead ends.** A hypothesis you formed, the evidence that **disproved** it, and how you re-modeled. Hiding this makes the reasoning look like magic and teaches nothing.
- **Ground every step in real evidence** — the actual command, the actual output, the actual log line. Then translate it into plain language ("what this error is really saying is…").
- **Distinguish correlation from causation explicitly.** Call out the tempting-but-wrong causal chain and why it's wrong.
- **End with transferable principles** — the reusable heuristics ("if the same error hits multiple unrelated objects, escalate from 'this instance' to 'this node/service'"). This is the part the reader will carry to the next incident.

**Structure:** Summary callout → symptom (with the exact status/error) → getting the real error → ruling out the obvious → the turning-point observation → capturing the "fingerprint" (the decisive evidence) → the counter-intuitive check (why some things still worked) → root cause → fix (and why it's safe) → optional deep-dive → **retro & transferable heuristics** → references.
