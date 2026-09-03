---
name: refine
description: Turn a loose, high-stakes question into a hard-coded prompt that has to show its sources and dates, score its own confidence, say "Data Not Found" instead of guessing, and push back when the question itself is wrong. Use when the user runs /refine, hands over a rough question and asks for a better prompt, or says the AI's answer sounded confident but they cannot tell what to trust.
---

# Refine a prompt before you ask it

`/refine <question>`

The failure this exists for: an AI answers a factual question quickly and confidently, the answer
carries no source and no date, and you act on it. This skill rewrites the question into a prompt
that makes the answer checkable.

The rules are in `instruction.md`, in this repo, and that file is the source of truth. Read it
before you write anything.

## How to run it

**Step 1 — audit the gaps first. Do not write a prompt yet.**

Read the user's question against the nine guardrails in `instruction.md` and find what is
missing. If you cannot satisfy a guardrail because the user has not told you something, ask.
Concrete example: a question about opening a bank account cannot be hard-coded without residency
status and ID type, so those are questions, not assumptions.

Ask the questions as a short list and stop. Never fill a gap by guessing.

If the question genuinely has no gaps, say so in one line and go straight to step 2.

**Step 2 — write the refined prompt.**

Apply the nine guardrails from `instruction.md` to the user's now-complete question. Output the
prompt as one block the user can copy in a single action. It is a prompt, not a report: no
commentary inside the block.

**Step 3 — say where it goes.**

Tell the user to paste it into a **new chat**, not the one they are in. The refining conversation
is full of the reasoning that produced the prompt, and that context is exactly what the prompt is
supposed to exclude.

## Output shape

```
Missing info
  1. ...
  2. ...

(after the user answers)

The refined prompt
  <one copyable block>

Why these guardrails
  <two or three lines: which rules this question needed and what each one stops>
```

## What this does not claim

It does not stop the model being wrong. It makes the answer show its sources and dates, mark what
it is unsure of, and say when it does not know, so you can see which lines to check before you
act on them. Say it that way to the user; do not call the result bulletproof.
