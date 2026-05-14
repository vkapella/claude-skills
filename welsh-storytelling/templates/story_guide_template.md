# Story Guide Template

The skeleton for the .docx Story Guide companion document. Use this as the structural reference when generating the file. The visual rendering details and python-docx code patterns are in `examples/build_story_guide_example.py`.

> **Voice consistency.** The Story Guide must be in the same voice register as the deck. The visual identity (colors, fonts, layout) is voice-agnostic — only the *content* shifts. The sections most affected by voice are: the Core Message wording, the Diamond's facet content, the RWV library angles, the verbatim Opening/Closing lines, and how prominently the "I Don't Know" list features. See `references/voice.md` for the per-voice patterns and `references/delivery.md` for section-by-section voice notes.

---

## Document structure

```
COVER
├── Eyebrow: "STORY GUIDE  ·  COMPANION TO THE SLIDE DECK"
├── Title: [The core message restated as a memorable phrase — voice-matched]
├── Horizontal rule
├── Italic subtitle: "Delivery coaching for the [topic] presentation. Built on Michael Welsh's storytelling frameworks from The Backstory on Storytelling."
└── Footer line: "[Brand]  ·  Prepared for [audience]  ·  [Month YYYY]"

1. THE CORE MESSAGE
├── Body lead-in: "If [audience] leaves the room remembering one sentence, this is the sentence:"
├── Callout box (light blue tint, left accent border):
│   ├── Eyebrow: "CORE MESSAGE"
│   └── Italic body: [The one sentence — voice-matched]
└── Body close: "Everything else in the deck is in service of this one sentence. When in doubt during Q&A, return to this."

2. THE DIAMOND
├── Italic subtitle: "Welsh's framework: every core message is a diamond with five facets..."
└── 5-row table (label column tinted blue, content column white):
    ├── The Point        | [headline restated — voice-matched]
    ├── The Context      | [the setup, the why now]
    ├── The Evidence     | [the proof, the data]
    ├── The Application  | [what it means for the audience]
    └── The Call to Action | [what you need from them — or commitments to learn in Reflective voice]

3. REPETITION WITH VARIATION LIBRARY
├── Italic subtitle: "Welsh's principle: tell the same truth three different ways..."
├── Sub-section: "Three ways to land [primary message]"
│   ├── Labeled para: [Angle 1 per voice] — "[variation]"
│   ├── Labeled para: [Angle 2 per voice] — "[variation]"
│   └── Labeled para: [Angle 3 per voice] — "[variation]"
├── Sub-section: "Three ways to land [secondary message]"
│   └── (3 variations with different angles)
└── Sub-section: "Three ways to close"
    └── (3 closing line options — voice-matched cadence)

Voice-matched angle defaults (see delivery.md):
- Boardroom: Technical / Financial / Strategic
- Operator: Day-1 reality / Honest / Forward-looking
- Technical: Tradeoff-framed / Constraint-framed / Comparison-framed
- Reflective: Honest / Operational / Future-facing

4. ARC MAP — HOW TIME GETS SPENT
├── Italic subtitle: "Welsh's math: 60-minute meeting = ~47 minutes of material maximum..."
├── 4-column table (NAVY header):
│   └── # | Beat | What happens | Time
│   └── (one row per slide)
└── Italic close: "Total slide time: ~X minutes. Leaves ~Y minutes for Q&A inside a Z-minute slot..."

5. CURVEBALL QUESTION PREP
├── Italic subtitle: "Welsh's six techniques for handling hard questions..."
└── For each of 5-8 questions:
    ├── Bold dark blue: "Q.  [question text]"
    ├── Italic orange: "Technique:  [Welsh technique name]"
    └── Indented body in quotes: "[drafted answer]"

Voice note: Technical voice favors Complete Disassembly and Disambiguate-and-Redirect. Reflective voice favors honest "I Don't Know" more than the other voices.

6. TOPICS WHERE "I DON'T KNOW" IS THE RIGHT ANSWER
├── Italic subtitle: "Welsh's power move: admitting uncertainty turns vendors into partners..."
└── Bulleted list:
    └── ·  [Bold navy topic]  [italic gray reason]

Voice note: In Reflective voice, consider promoting 1-2 of these onto a deck slide (the Emergent Understanding slide if Arc of Uncertainty was the chosen arc).

7. OPENING AND CLOSING LINES — MEMORIZE THESE VERBATIM
├── Eyebrow: "FIRST 30 SECONDS"
├── Callout box (light blue tint):
│   ├── Eyebrow: "OPENING (VERBATIM)"
│   └── Italic body: "[scripted opening line — voice-matched]"
├── Eyebrow: "LAST 30 SECONDS"
└── Callout box (orange tint):
    ├── Eyebrow: "CLOSING (VERBATIM)"
    └── Italic body: "[scripted closing line — voice-matched]  Then SHUT UP. Three-second rule."

8. DELIVERY NOTES — POISE, PRESENCE, POSTURE
├── Sub-heading: "Before you walk in"
│   └── Bullets: box breathing, read the room, bookmark appendix
├── Sub-heading: "During delivery"
│   └── Bullets: Three-Second Rule, eye contact, movement, recovery from stumbles
└── Sub-heading: "Where to slow down"
    └── Bullets: specific slides where extra time matters (voice-dependent — see delivery.md)

9. THE CUT LIST — WHAT'S IN THE APPENDIX AND WHY IT'S NOT IN THE FRONT
├── Italic subtitle: "Welsh: 'Make people pitch why their content deserves inclusion.'..."
└── 2-column table (NAVY header):
    └── Content | Why it's not in the front
    └── (5-8 rows of cut/appendix content with one-line reasons)

FOOTER
├── Horizontal rule
└── Italic gray attribution: "This Story Guide applies frameworks from The Backstory on Storytelling by Michael Welsh: the 5 Slide Rule, the Setup-What-How-Why-Magic Wand arc, Designing for Diamonds, Repetition with Variation, and the Curveball Question techniques. The deck is the storyboard. This guide is the script."
```

---

## Brand color tokens (defaults)

If stacking with `wwt-brand`, use the WWT palette. Otherwise:

| Token | Hex | Usage |
|---|---|---|
| Primary dark | `#1C0087` | Section headings, table cells |
| Primary light | `#0086EA` | Eyebrows in main color, callout accents |
| Accent | `#EE282A` | Hard-stop emphasis (rare) |
| Highlight orange | `#FB550E` | Eyebrows on Story Guide, technique labels |
| Navy deep | `#1D1E48` | Sub-headings, table header backgrounds |
| Body | `#262626` | Body text |
| Gray | `#6B7280` | Italic notes, footer text |
| Light blue tint bg | `#E6F3FD` | Callout box backgrounds |
| Light gray bg | `#F5F7FA` | Quiet card backgrounds |
| Orange tint bg | `#FFF4E6` | Closing callout box background |

Visual tokens are voice-agnostic. A Reflective Story Guide uses the same palette as a Boardroom Story Guide.

---

## Page layout

- 8.5" × 11" (Letter) portrait
- Margins: 2cm all sides
- Body font: Calibri 11pt
- Headings: Calibri (H1: 18pt bold, H2: 14pt bold, H3: 12pt bold)
- Eyebrows: Calibri 9pt bold ALL CAPS
- Line spacing: tight (default with small space-after)

---

## Length targets

- Total document: 4-6 pages
- Cover: 1/3 page
- Sections 1-3 (Core, Diamond, RWV): ~1 page combined
- Section 4 (Arc Map): 1/2 page
- Section 5 (Curveballs): 1.5-2 pages (this is the meatiest section)
- Sections 6-7 (I Don't Know, Opening/Closing): 1 page combined
- Sections 8-9 (Delivery, Cut List): 1 page combined

If the Story Guide is creeping past 6 pages, cut. The presenter won't read it.
