# Tests — welsh-storytelling

Sample prompts and expected behaviors for regression-checking this skill. There's no test runner — this is eyeball-diff territory. The point is that after changing the skill, you can rerun a small fixed set of prompts and see whether the *character* of the output drifted.

## How to use

1. Pick a prompt from `prompts/`.
2. Start a fresh Claude conversation with this skill installed.
3. Paste the prompt. Let Claude run through the full flow (interrogation, outline confirmation, deck + Story Guide).
4. Compare against the corresponding `expected_behavior.md` file. You're checking *qualitative* properties — voice, structure, slide count, whether forbidden patterns appear.
5. If the behavior diverged in a way you didn't intend, that's a regression. If it diverged in a way you *did* intend (because of a recent change), update the expected_behavior.md file and commit it as part of the same change.

## Test cases

| Prompt | What it exercises | Expected voice |
|---|---|---|
| `prompts/01_cfo_siem_pitch.txt` | Boardroom inference from "CFO" + "recommending" | Boardroom |
| `prompts/02_sre_rollout.txt` | Operator inference from "SRE team" + "rollout" | Operator |
| `prompts/03_year_end_review.txt` | Reflective inference from "year-end review" + "what didn't" | Reflective |
| `prompts/04_architecture_review.txt` | Technical inference from "architecture review" | Technical |
| `prompts/05_ambiguous.txt` | Should ask the voice question outright | (asked, not inferred) |

## What "passing" looks like

A fixture passes when, in a fresh conversation:

- The interrogation step **states the inferred voice** (or asks for it, in the ambiguous case).
- Headlines, the What-slide sentence, and the Magic Wand close all match the patterns in `references/voice.md` for that voice.
- The forbidden patterns for that voice (listed in `voice.md` "Avoid in this voice") do not appear.
- The deck and Story Guide are both produced.
- Slide count is within the bound for the time slot.

## What "failing" looks like

- The deck defaults to Boardroom voice for an obvious Operator or Reflective prompt.
- A post-mortem closes with "Sign this week" energy.
- Voice is silently chosen without being stated.
- Only one of the two files is produced.
