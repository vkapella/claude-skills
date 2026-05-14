# Delivery Reference

This file defines the content and approach for the Story Guide companion document. The Story Guide is delivery coaching — it contains everything the presenter needs but the audience never sees.

Read this file when generating the .docx Story Guide.

> **Voice consistency.** The Story Guide must speak in the same voice register as the deck. A Reflective deck does NOT get a Boardroom Story Guide. The sections most affected by voice are the Diamond's facet content, the Repetition with Variation library angles, the verbatim Opening and Closing lines, and the "I Don't Know" list (which is more prominent in Reflective voice). See `voice.md` for the per-voice patterns.

---

## The 9 Story Guide sections

Every Story Guide has these nine sections in this order. Don't reorder. Don't skip.

### 1. The Core Message

**One paragraph. One sentence ideally. The thing the audience must remember if they remember nothing else.**

Format: A callout box with ORANGE eyebrow label "CORE MESSAGE" and the message in italic body text inside a tinted box with a left accent border.

The core message is NOT the topic. It's the conclusion. It's what you want the audience to think when they walk out.

**Voice variation:**
- **Boardroom:** "Our Q3 roadmap closes the three control gaps that triggered the audit findings — and does it before the November re-audit."
- **Operator:** "Moving to Opsgenie changes three things about your on-call rotation — and one of those is rough for the first two weeks."
- **Technical:** "Sharded Postgres meets 4× write throughput at the cost of global consistency — the right tradeoff for our load profile, the wrong one for a globally distributed analytical workload."
- **Reflective:** "Three of four workloads landed clean. The fourth taught us what our migration model didn't account for — and that's the gap we're investing in next year."

**Bad core message (any voice):** "An update on the Q3 cybersecurity roadmap." (topic, not conclusion)

### 2. The Diamond

**A 5-row table mapping the core message across all five Diamond facets.**

| Row | Label | What goes here |
|---|---|---|
| 1 | The Point | The headline. The core message restated as one sentence. |
| 2 | The Context | The setup. Why this conversation is happening now. |
| 3 | The Evidence | The data, the proof, the technical case. |
| 4 | The Application | What it means for the audience specifically. |
| 5 | The Call to Action | What you need from them. Concrete and time-bound. |

The Diamond is a Q&A pivot tool. When asked about cost, the presenter surfaces the Application facet. When asked about technical risk, Evidence. When asked about timing, Call to Action.

**Voice note:** In **Reflective voice**, the Call to Action row may legitimately read "Commitments to learn and report back quarterly" rather than a discrete decision-ask. Do not force a fake decision into this row if the room isn't there for one.

### 3. Repetition with Variation Library

**3 sub-sections, each with 3 variations of a key message.**

Each sub-section is for a different angle. **The angles should match the voice:**

- **Boardroom:** Technical / Financial / Strategic
- **Operator:** Day-1 reality / Honest / Forward-looking
- **Technical:** Tradeoff-framed / Constraint-framed / Comparison-framed
- **Reflective:** Honest / Operational / Future-facing

Format each variation as a `labeled_para` with a colored label tag and the variation in quotes.

The presenter doesn't memorize all nine. They pick 2-3 based on which angle the room responds to.

**Example structure (Boardroom):**

> Three ways to land "why we should buy X"
> - **Technical:** "X is the only option that fits the architecture."
> - **Financial:** "X costs more now but saves twice as much over three years."
> - **Strategic:** "X is the platform decision, not the procurement decision."

**Example structure (Reflective):**

> Three ways to land "what we got wrong on the migration"
> - **Honest:** "We underestimated how much the legacy data model would push back."
> - **Operational:** "The on-call team felt it first — and they were right that we weren't ready."
> - **Future-facing:** "It's the lesson we're carrying into the FY27 plan, not a wound to dress."

### 4. Arc Map — How time gets spent

**A table with 4 columns: #, Beat, What happens, Time.**

One row per slide. The Time column shows minutes:seconds.

Below the table, a one-line summary: "Total slide time: ~X minutes. Leaves ~Y minutes for Q&A inside a Z-minute slot."

This forces honest time math. Most presenters over-prepare. The Arc Map shows them where they have slack and where they're tight.

### 5. Curveball Question Prep

**5-8 anticipated hostile or trap questions, each with three components:**

1. The question itself, formatted as `Q.  [question text]` in BOLD.
2. The technique tagged in italic ORANGE: `Technique:  [Welsh technique name]`.
3. A drafted answer in body text, indented, in quotes.

Welsh's six techniques to draw from:
- **Don't react immediately** (the Three-Second Rule)
- **Acknowledge** (brief, not sycophantic)
- **Intentional silence**
- **Characterize and Categorize** ("So if I'm hearing you correctly...")
- **Disambiguate and Redirect** ("Help me understand the concern — is it X or Y?")
- **Complete Disassembly** (take apart the assumptions in the question)
- **Honest "I Don't Know"** (when uncertainty is real)

Mix techniques across the questions. Don't use Characterize and Categorize for every question. Real Q&A demands variety.

**Voice note:** Technical voice curveballs lean heavily on Complete Disassembly and Disambiguate-and-Redirect — the audience expects rigorous engagement with the question's premises. Reflective voice leans on Honest "I Don't Know" more than the other voices.

### 6. Topics Where "I Don't Know" Is the Right Answer

**A bulleted list of 3-6 topics where the presenter is pre-authorized to admit uncertainty.**

Format: Each item has a bold NAVY topic label and a gray italic note explaining why it's an "I don't know" topic.

This list is the presenter's permission slip. It eliminates the panic-fabrication that happens when an executive asks something the presenter genuinely doesn't know.

**Voice note:** In **Reflective voice**, consider whether one or two of these "I Don't Know" items belong in the deck itself (as a dedicated slide or as part of the Emergent Understanding slide). Reflective decks earn credibility by *showing* calibrated uncertainty on the slides, not just preparing for it backstage.

### 7. Opening and Closing Lines (Verbatim)

**Two callout boxes — one for the opening 30 seconds, one for the closing 30 seconds.**

These are scripted word-for-word. The presenter memorizes them. They are the only verbatim parts of the talk.

Why memorize? Because:
- The opening has to be confident from second one. Improvising the opener loses the room.
- The closing is what the audience walks out remembering. It can't be left to chance.

**Format:**
- Opening box: LIGHT BLUE TINT background, "OPENING (VERBATIM)" eyebrow, the script in italic.
- Closing box: ORANGE TINT background, "CLOSING (VERBATIM)" eyebrow, the script in italic, ending with "Then SHUT UP. Three-second rule. Make them speak first."

**Voice variation (the closing line):**
- **Boardroom:** "One decision today. Eleven sites by September. The pattern for everything that follows. — What questions do you have?"
- **Operator:** "Pilot starts Monday. Office hours every Thursday. If something feels weird, you ping me. — What's on your mind?"
- **Technical:** "RFC open through Friday. Prototype in two weeks. Decision at the next architecture sync. — Where should we push harder on this?"
- **Reflective:** "Here's where we are. Here's where we're heading. Questions are how we get sharper from here. — What are you seeing that I'm not?"

The "SHUT UP, three-second rule" instruction applies across all voices — the silence after the closing line is the close, not the words.

### 8. Delivery Notes — Poise, Presence, Posture

**Three sub-sections of bulleted advice: Before you walk in / During delivery / Where to slow down.**

Sub-section: **Before you walk in**
- Box breathing: 4-4-4-4 for one minute
- Read the room before starting (cues to look for)
- Have specific appendix slides bookmarked

Sub-section: **During delivery**
- Three-Second Rule between slides
- Eye contact discipline (one thought per person)
- Movement (don't hide behind the laptop)
- If you stumble: pause, breathe, restart the sentence — don't apologize

Sub-section: **Where to slow down**
- Slide-by-slide notes on which moments need extra time
- Specifically the moments where the message lands

**Voice note:** Delivery Notes content is mostly voice-agnostic — the physical layer is the same regardless of register. The exception is *where to slow down*. In Reflective voice, slow down on the Trough of Despair slide and the "what we don't yet know" moments. In Boardroom voice, slow down on the cost slide and the Magic Wand close.

### 9. The Cut List

**A 2-column table: Content / Why it's not in the front.**

5-8 rows of content that was considered for the front of the deck and moved to the appendix or cut. Each row gives a one-line reason.

This makes the curation visible. It also gives the presenter answers if someone says "I'm surprised you didn't include X" — there's a documented reason.

---

## Story Guide visual identity

The Story Guide should feel like a coaching document, not a slide handout.

- **Cover:** Eyebrow label, large title (the core message restated), horizontal rule, italic gray subtitle, small footer with prep date.
- **Section headings:** WWT Dark Blue, 18pt bold for level 1; NAVY 14pt bold for level 2.
- **Body text:** Calibri 11pt, BODY color (#262626).
- **Eyebrows:** ORANGE, 9pt, ALL CAPS, bold.
- **Callouts:** Tinted background (light blue tint or orange tint) with a 3pt left border in the accent color.
- **Tables:** Header row in NAVY background with white bold text. Body rows alternate or stay clean.

Visual identity is voice-agnostic. A Reflective Story Guide looks the same as a Boardroom Story Guide — only the words inside change.

---

## Tone of voice for the Story Guide

The Story Guide talks TO the presenter, not ABOUT the audience. Write in second person:

- "Pause here." — not "The presenter should pause."
- "If they push on cost, use option 2." — not "When the audience pushes back on cost, the presenter should consider..."

Be direct. Be specific. The Story Guide is read in the car ride to the meeting, possibly in a stressful state. It needs to be scannable and actionable.

**Note on internal voice vs. delivery voice:** This "talk to the presenter" tone is *Claude's* voice inside the Story Guide — coaching, second-person, direct. It's separate from the *delivery voice* (Boardroom/Operator/Technical/Reflective) which governs what the presenter says to their audience. Keep them distinct: the Story Guide coaches in a direct second-person tone regardless of which delivery voice the presenter is using.

---

## What the Story Guide does NOT contain

- A summary of the slide deck contents (the deck speaks for itself)
- Generic public speaking advice ("smile, make eye contact")
- Disclaimers or caveats ("this is just a suggestion")
- Marketing language ("leverage these powerful insights")
- Anything the presenter already knows

If a section feels like filler, cut it.
