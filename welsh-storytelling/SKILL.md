---
name: welsh-storytelling
description: "Apply Michael Welsh's storytelling frameworks from The Backstory on Storytelling whenever creating slides, decks, presentations, pitches, talks, briefings, or board materials. Use this skill when the user asks Claude to build a presentation, PowerPoint, .pptx, slide deck, or pitch — even casually phrased like 'put together some slides' or 'make me a quick deck.' Also use when the user explicitly references Welsh's frameworks: '5 Slide Rule,' 'Designing for Diamonds,' 'Arcs of Uncertainty,' 'Repetition with Variation,' '3 is more than magic,' or 'curveball questions.' This skill produces TWO outputs every time: the slide deck AND a companion Story Guide for delivery coaching. Do NOT use this skill for non-presentation writing tasks (regular reports, emails, documents) unless they will be delivered as a talk."
---

# Welsh Storytelling Skill

Apply Michael Welsh's storytelling frameworks from *The Backstory on Storytelling* whenever building presentations. Every deck request produces **two** deliverables: the slide deck AND a companion Story Guide for delivery coaching.

## When to use this skill

Trigger on any of these signals:

- User asks to create slides, a deck, a presentation, a pitch, a talk, a briefing, board materials, or a "quick PPT"
- User asks for help preparing to deliver a presentation
- User explicitly references Welsh frameworks: "5 Slide Rule," "Designing for Diamonds," "Arcs of Uncertainty," "Repetition with Variation," "3 is more than magic," "curveball questions"
- User uploads an existing deck and asks for it to be improved, restructured, or re-storyboarded

Do NOT trigger for plain documents, emails, or reports unless they are scripts for a talk.

## The non-negotiable two-output pattern

Every deck request produces:

1. **A `.pptx` slide deck** — built on Welsh's structural frameworks (5 Slide Rule, Setup→What→How→Why→Magic Wand arc, Rule of 3, Diamonds). Every slide carries speaker notes containing the BME of that slide.
2. **A `.docx` Story Guide** — a companion document for the presenter. Nine sections covering Core Message, Diamond, Repetition with Variation library, Arc Map with timing, Curveball Question prep, "I Don't Know" list, verbatim Opening/Closing lines, Delivery Notes, and the Cut List.

Both files are produced and shared with the user via `present_files` at the end of every run. Never produce just the deck. Never produce just the guide.

## Skill stacking — auto-detect the brand context

This skill provides the storytelling structure. It does NOT know how to render slides or documents. It must stack with format and brand skills.

**For WWT presentations (default for World Wide Technology context):**
- Stack with `wwt-presentation` skill at `/mnt/skills/organization/wwt-presentation/SKILL.md` — provides python-pptx slide builders, brand colors, layouts, asset paths
- Stack with `wwt-brand` skill at `/mnt/skills/organization/wwt-brand/SKILL.md` — provides tone-of-voice, color tokens, typography rules

**For non-WWT or generic decks:**
- Stack with the public `pptx` skill at `/mnt/skills/public/pptx/SKILL.md`
- Stack with the public `docx` skill at `/mnt/skills/public/docx/SKILL.md`

Read the relevant skill files BEFORE writing any code. The brand/format skills tell you HOW to render. This skill tells you WHAT to put on each slide and WHY.

## Execution flow

Follow these steps in order. Do not skip the interrogation step.

### Step 1: Read the framework reference

Read `references/frameworks.md` first. The frameworks are interconnected — the arc choice affects which slide patterns apply, which affects which Diamond facets get surfaced.

### Step 2: Interrogate the user (one focused round)

Ask the questions in `templates/interrogation.md` using the `ask_user_input_v0` tool where possible. If the user already provided enough context in the request, skip questions you already have answers to and STATE your assumptions explicitly.

The questions cover: audience, **voice (register)**, time slot, desired outcome, topic and key facts, and arc preference. See `templates/interrogation.md` for the full intake script.

**Voice inference is preferred over asking.** Most of the time you can infer voice from audience + topic and just state it ("Reading this as a technical architecture review, so I'd plan to use the Technical voice — sound right?"). Only ask the voice question outright when the inference is genuinely ambiguous. See the inference table in `references/voice.md`.

If the user uploaded an existing deck, ALSO ask: "Should I rework the whole deck or just the front-of-deck business framing?" Most existing decks have technical appendix material that's fine — the pain is usually in the opening.

### Step 3: Choose the arc, draft the outline

Read `references/slide_patterns.md` AND `references/voice.md`. Then build a slide-by-slide outline applying:
- The 5 Slide Rule as a ceiling (push back if user wants more)
- Rule of 3 on every content slide
- The chosen narrative arc as the spine
- **The chosen voice as the register** — substitute headlines, What-slide sentences, and Magic Wand patterns from `voice.md` based on the selected voice
- Linkage between consecutive slides — each slide must explicitly set up the next

Show the outline to the user as a numbered list and get a yes before generating the .pptx. This saves a regeneration cycle if the structure is wrong.

### Step 4: Generate the deck

Read the relevant brand/format skill (wwt-presentation OR public pptx). Build the deck per its conventions. For each slide:
- Apply Welsh's slide pattern (Setup, What, How, Why, Magic Wand)
- **Apply the voice register from `voice.md`** to all visible text — headlines, body copy, closing lines
- Keep visible content to Rule of 3
- Add speaker notes with the BME of THIS slide and what the presenter should say
- Add Repetition with Variation hints in the speaker notes (3 ways to land the slide's point)

Save the .pptx to `/home/claude/output/` first; copy to `/mnt/user-data/outputs/` only when complete.

### Step 5: Generate the Story Guide

Read `references/delivery.md` and `templates/story_guide_template.md`. Build the .docx with all nine sections. The Story Guide is NOT a summary of the deck — it's the delivery script and coaching layer the audience never sees.

The Story Guide should also be voice-consistent. The verbatim Opening and Closing lines, Repetition with Variation library, and Delivery Notes all reflect the chosen voice. A Reflective deck does not get a Boardroom Story Guide.

Use python-docx directly (not the docx skill's docx-js path) because the Story Guide needs custom callout boxes, colored cells, and tight typography control. See `examples/build_story_guide_example.py` for a working pattern.

### Step 6: Present both files and offer one diagnostic

Use `present_files` to share both the .pptx and the .docx. Then end with ONE diagnostic question:

> "Want me to stress-test this with three more curveballs a [audience] might throw?"

Don't list the contents of the deck back at the user. They can see the file. End the turn.

## What this skill enforces

### Always
- Two files per request (.pptx + .docx)
- Speaker notes on every slide
- Rule of 3 on every content slide
- A real Setup before any What — never start the deck with the proposal
- A voice selected (or inferred and stated) before generating headlines
- A Magic Wand at the end — but the *form* of the Magic Wand depends on voice (see below)

### Never
- 50-slide decks. If asked, push back, propose 5-7 with the rest as backup.
- Bullet-soup slides where the bullets ARE the message. Bullets are the storyboard; speaker notes are the script.
- Generic "agenda," "objectives," "thank you," or "Q&A" filler slides.
- Quoting more than 15 words from any source if research was used. Paraphrase Welsh's frameworks; don't reproduce them.

### Conditional rules (depend on voice)

The "End with wanting — never close with a thud" rule is **conditional on voice**:

- **Boardroom / Operator / Technical voices:** Magic Wand ends with a concrete ask, dates, or a decision point. Don't close with "either option works."
- **Reflective voice:** Magic Wand ends with direction, commitments to learn, or calibrated uncertainty. Forcing a decision-ask onto a post-mortem produces the flamboyant, oversold feel. Ending with "here's what we don't yet know, and here's how we'll find out" is the *correct* close.

When in doubt, the closing line should match the voice — not override it.

## Pushback patterns

When the user requests something that violates the principles, push back conversationally:

- **"Make me a 30-slide deck"** → "30 slides for what time slot? Welsh's rule is 47 minutes of material max for an hour meeting. I'd propose 7 core slides plus an appendix — happy to put more in backup if you want detail on demand."
- **"Just put bullet points on each slide"** → "I can do that, but bullet-only slides put the burden on the audience to read while you talk. Welsh's pattern is: slides as storyboard, speaker notes as script. Want me to do it that way?"
- **"Add an agenda slide"** → "I'd skip it. The Setup slide does that work without the meta-slide. If you want a roadmap, I can add it to the speaker notes for slide 1 instead."
- **"Make it punchier"** on a Reflective deck → "I can — but punchier in a post-mortem usually reads as oversold. Want me to swap to Boardroom voice across the whole deck, or just tighten the close?"

## Reference files

- `references/frameworks.md` — All Welsh frameworks in detail. Read first.
- `references/voice.md` — The four voices (Boardroom, Operator, Technical, Reflective) with headline patterns, Magic Wand patterns, and inference rules. Read alongside slide_patterns.md.
- `references/delivery.md` — Story Guide content: RWV, Curveballs, Poise/Presence, "I Don't Know."
- `references/slide_patterns.md` — Concrete slide patterns by role (Setup, What, How, Why, Magic Wand). Defaults to Boardroom voice; substitute from voice.md based on selection.
- `templates/story_guide_template.md` — The 9-section Story Guide skeleton.
- `templates/interrogation.md` — The intake script with `ask_user_input_v0` payloads, including voice inference.
- `examples/build_story_guide_example.py` — Working python-docx code for the Story Guide (used in the BNY demo).
