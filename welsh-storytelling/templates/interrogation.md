# Interrogation Template

The intake script Claude uses before generating any deck. Use the `ask_user_input_v0` tool to present these as tappable options where it makes sense.

If the user already answered some of these in their original request, SKIP those questions and STATE your assumptions in your response. Don't ask what you already know.

---

## When to use ask_user_input_v0 vs. just asking

**Use ask_user_input_v0** when the answers are short and selectable (audience type, time slot, voice, arc preference). The buttons are easier on mobile.

**Just ask in prose** when the answer needs explanation (the topic, the key facts, the desired outcome). These need typing.

A good interrogation pattern is ONE `ask_user_input_v0` call with the multiple-choice questions, plus a follow-up sentence asking for the prose answers.

---

## The questions

### Q1. Audience

Question text: "Who are you presenting to?"

Options:
- "Executive (C-suite, board, COO)"
- "Peer (colleagues, internal team)"
- "Client (external customer)"
- "Mixed (some senior, some operator)"

**How this affects the deck:**
- Executive → emphasize Why and Magic Wand. Keep How brief. Strong cost framing.
- Peer → expand How. Less ceremony in Setup.
- Client → emphasize Setup (their problem, in their language). Magic Wand is more about partnership than commitment.
- Mixed → default 5-Beat. Keep technical depth in appendix, surface on demand.

### Q2. Voice (register)

Question text: "What register fits this room?"

Options:
- "Boardroom — confident, decision-forcing, three-beat closes"
- "Operator — plainspoken, concrete, what-changes-Monday"
- "Technical — precise, evidence-first, names tradeoffs"
- "Reflective — measured, comfortable with uncertainty"

**How this affects the deck:** This shapes word choice and rhythm — not structure. See `references/voice.md` for the full pattern library per voice. Headlines, What-slide sentences, and Magic Wand closes all swap based on voice. The skill's general "end with wanting" rule is **conditional on voice** — in Reflective voice, ending with calibrated uncertainty is correct.

**Inference shortcut — usually skip the question.** Before asking, infer the voice from Q1 and the topic, and **state the inference**. Only present this question if the inference is genuinely ambiguous. Mapping:

| Audience | Default voice | Override |
|---|---|---|
| Executive | Boardroom | Post-mortem topic → Reflective |
| Peer | Operator | Architecture topic → Technical |
| Client | Boardroom | Mature partnership + learning topic → Reflective |
| Mixed | Reflective | Decision-ask present → Boardroom; architecture room → Technical |

Topic signals that override the audience default:
- "post-mortem," "incident," "what we learned," "year in review" → **Reflective**
- "architecture," "design review," "RFC," "tradeoffs" → **Technical**
- "rollout," "runbook," "team enablement," "ops handoff" → **Operator**
- "recommendation," "proposal," "investment ask" → **Boardroom**

When inferring, phrase it like this in your response: *"Reading this as a technical architecture review, so I'd plan to use the Technical voice — punchy three-beat closes off, evidence-first headlines on. Sound right, or want a different register?"*

### Q3. Time slot

Question text: "How long is the meeting?"

Options:
- "15 minutes or less"
- "30 minutes"
- "60 minutes"
- "More than 60 minutes"

**How this affects the deck:**
- ≤15 min → 3-5 slides + appendix
- 30 min → 5-7 slides + appendix (target ~16 min of slides, 14 min Q&A)
- 60 min → 7-10 slides + appendix (target ~30 min of slides, 30 min Q&A)
- 60+ min → use Section Break slides; max 12 content slides per section

### Q4. Desired outcome

Question text (prose, not multiple choice): "What's the outcome you want from this meeting? In one sentence — a decision, alignment, buy-in, action, insight?"

This becomes the Magic Wand slide's content. It also shapes the closing line. **Note:** for Reflective voice, the "outcome" may legitimately be alignment-on-direction or shared understanding rather than a discrete decision — don't push the user to invent a decision-ask if the room doesn't call for one.

### Q5. Topic and key facts

Question text (prose): "Walk me through the topic and the must-include facts — numbers, dates, names, vendors, anything specific that has to appear."

If the user has uploaded an existing deck or document, this is "what should I keep from your existing materials, and what's new context I should layer in?"

### Q6. Arc preference

Question text: "Which narrative arc fits this talk?"

Options:
- "Default — Setup → What → How → Why → Magic Wand (best for proposals, recommendations, pitches)"
- "Familiar → Foreign → Transformation → Return (best for innovation, change, transformation)"
- "Arc of Uncertainty (best for honest leadership talks, post-mortems, learning)"
- "Not sure — pick for me"

**How this affects the deck:**
- 5-Beat → use the patterns in slide_patterns.md as written
- Familiar→Foreign → adapt the Setup as "the world we know," the What as "what's changing," the How as "the bridge," the Why+Magic Wand as "the new normal"
- Arc of Uncertainty → REQUIRES the Trough of Despair slide; do not omit it. Strongly correlates with Reflective voice.
- "Not sure" → default to 5-Beat unless the topic clearly signals one of the others

---

## Bonus question for existing-deck reworks

If the user uploaded an existing presentation, ask ONE additional question:

Question text: "Should I rework the whole deck, just the front-of-deck business framing, or just produce the Story Guide for the existing deck as-is?"

Options:
- "Rework the whole deck"
- "Just the front-of-deck business framing — keep the technical/appendix slides"
- "Just the Story Guide — leave my deck alone"

**Most existing decks have solid technical content but weak business framing.** The "front-of-deck only" option is usually the highest-ROI choice. Make this clear when offering it.

---

## What to do with the answers

After the user responds:

1. **Confirm the inputs in plain language, including voice.** ("So — 30-minute slot with the COO, recommending Cisco SD-WAN over Meraki, decision needed by Friday, default 5-beat arc, **Boardroom voice**. Ready to outline?")
2. **Show the slide outline as a numbered list** before generating the .pptx. This catches structure errors before they become rendering errors.
3. **Wait for the user's "yes"** on the outline. THEN generate the .pptx and .docx in sequence.

Do not generate the files in the same response as the interrogation. Two-step is faster than wrong-and-redo.

---

## Sample interrogation flow (with voice inference)

User: "Build me a board deck on our security posture for next Tuesday."

Claude (interrogation):
> Before I draft this, a few quick questions. I'm reading this as a board audience with an honest year-in-review feel, so I'd plan to use **Reflective voice** — measured, comfortable acknowledging what almost went wrong, no forced decision-ask at the close. Say so if you'd rather it be Boardroom (decision-forcing) instead.

[ask_user_input_v0 with audience, time slot, arc preference]

> Plus two open-text:
> - **Outcome:** What do you want the board to do or decide as a result of this talk?
> - **Must-includes:** What specific facts, numbers, incidents, or names have to appear?

User answers.

Claude (confirmation + outline):
> Got it — board audience, 45-minute slot (I'll target 7 slides + appendix), Arc of Uncertainty, Reflective voice. Outcome is alignment on next year's investment ask.
>
> Here's the proposed outline:
> 1. Title — "We held the line. Here's what almost broke us."
> 2. Setup — Three near-misses from the past 12 months
> 3. Confidence we had — what we believed at the start of the year
> 4. Trough of Despair — the moment we realized the gaps
> 5. Quiet Progress — the corrections we made
> 6. Emergent Understanding — what we now know
> 7. Magic Wand — the FY26 investment ask, framed as a commitment to keep learning publicly
>
> Look right? Say yes and I'll build the deck and Story Guide.

User: "Yes."

Claude generates .pptx, then .docx, then presents both files.
