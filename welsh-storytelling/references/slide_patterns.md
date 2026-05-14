# Slide Patterns Reference

Concrete patterns for each slide role in Welsh's 5-Beat arc. Read this when generating the .pptx so each slide has the right structure for its role.

These patterns are framework-level. Specific rendering (colors, fonts, layouts) comes from the stacked brand/format skill (wwt-presentation, public pptx, etc.).

> **Voice note (v1.1).** The example headlines, What-slide sentences, and Magic Wand closes in this file default to **Boardroom voice** — punchy, three-beat, decision-forcing. The *structural* patterns (how many cards, what eyebrows, where the accent rule goes) apply to all voices. The *word choice* in the examples should be substituted from `voice.md` based on the selected voice register. For example, an Operator-voice Magic Wand keeps the three-card Rule of 3 layout, but the closing line cadence and word choice come from voice.md, not from the Boardroom examples below.

---

## Slide role 1: Title

**Purpose:** Make a promise the deck will keep.

**Pattern:**
- Eyebrow label (small, colored): the audience and program/topic
- Headline (huge): a sentence or fragment that tells the audience what the deck is FOR
- Accent rule (small colored bar)
- Subtitle (medium): one line elaborating the promise
- Footer (tiny): presenter, audience, date

**Good titles by voice (same structure, different cadence):**
- **Boardroom:** "11 sites. 6 months. One decision."
- **Operator:** "What's changing in your on-call rotation next month"
- **Technical:** "Sharded Postgres over Spanner — the tradeoffs that decided it"
- **Reflective:** "We held the line. Here's what almost broke us."

**Bad titles (any voice):**
- "Q3 Cybersecurity Roadmap" (topic, not promise)
- "Welcome to Our Presentation" (zero information)
- "Innovating for Tomorrow" (jargon, no promise)

**Speaker notes for the title slide:**
The verbatim opening line (30 seconds). The presenter memorizes this. Include the Three-Second Rule reminder before clicking past. The opening line cadence varies by voice — see voice.md.

---

## Slide role 2: Setup

**Purpose:** Establish the situation, the constraint, the problem. The BME of why this conversation exists.

**Pattern A: The Three Failures (when there's a clear past problem)**
- Title that names the problem honestly: "The last build broke. Here's how." (Boardroom) or "Three things we got wrong last cycle." (Reflective)
- Three card layout (Rule of 3) with: number, short heading, body description
- Italic takeaway line below the cards that becomes a callback later in the deck

**Pattern B: The Changed World (when the situation shifted)**
- Title that names what changed: "Three things the auditors now expect that they didn't last year"
- Three columns or rows, each describing one shift
- The shift in plain language, not jargon

**Pattern C: The Stakes (when the audience needs to feel the cost of inaction)**
- Title that names the stake: "What we're losing every quarter we don't decide"
- Three numbers or three concrete costs
- Visual contrast (red/orange) to signal urgency
- **Voice note:** This pattern is strongest in Boardroom voice. In Operator voice, replace "stakes of inaction" with "what's actually breaking for your team this week."

**Pattern D: What we believed at the start (Reflective only)**
- Title acknowledges the prior position: "What we believed when we started this migration"
- Three points capturing the original confident assumptions
- Italic line: "Two of these turned out to be right. One didn't."
- Sets up the Trough of Despair slide if Arc of Uncertainty is the chosen arc.

**What NOT to make:**
- An "Agenda" slide
- An "Objectives" slide
- A timeline of how the project came to be
- A list of stakeholders

The Setup is about the AUDIENCE'S situation, not the project's history.

---

## Slide role 3: What — The Core Message

**Purpose:** Land the proposal in ONE sentence. The Diamond's top facet.

**Pattern:**
- Eyebrow label: "WHAT · THE CORE MESSAGE" or similar
- A large dark colored box (navy, dark blue) covering the upper-middle of the slide
- ONE sentence inside the box, large type, white text. This is the recommendation.
- Below the box: 3 supporting facets (Rule of 3) — each a short heading + 1-2 sentence elaboration
- Each facet gets a small left accent border in brand color

**The sentence inside the box must:**
- Be readable in under 5 seconds
- Contain the actual recommendation, not a description of the proposal
- Use plain language. No acronyms in the headline (acronyms can appear in supporting facets)

**Voice variation of the box sentence — see voice.md for the full pattern library:**
- **Boardroom (default in this file):** "Deploy 11 microbranches on Cisco SD-WAN over 6 months — the only option that fixes all three documented failures."
- **Operator:** "We're moving the on-call rotation to Opsgenie next month. Here's what changes for you, what stays the same, and what we're still figuring out."
- **Technical:** "Sharded Postgres over a single Spanner instance — we trade global consistency for 4× write throughput and a known operational model."
- **Reflective:** "Three of four workloads landed clean. Here's what the fourth taught us about our migration model."

**Speaker notes for the What slide:**
Read the box aloud. Don't paraphrase. Let it sit. THEN move to the supporting facets.

---

## Slide role 4: How — The Proof

**Purpose:** Prove the proposal. Apply Rule of 3 ruthlessly to whatever evidence is available.

**Pattern A: The 3-Row Comparison (when comparing options)**
- Title that names the comparison: "Why X, not Y"
- Subtitle italic: a fair acknowledgment ("Both options work. Three things separate them.")
- A 3-row table with: Requirement / Option A / Option B
- Use ✓ and ✕ marks in green/red for clarity
- Bottom italic line: where the full data lives ("Full 12-row table in appendix")

**Pattern B: The 3-Step Process (when explaining how)**
- Title that names the mechanism: "How we get to live in 6 months"
- Three boxes left-to-right, with arrows or visual flow between them
- Each step has: a number, a heading, 2-3 lines of body
- Bottom italic line: a key risk or dependency

**Pattern C: The 3 Pillars (when describing capabilities)**
- Title that names the offering: "What you get with [solution]"
- Three columns, each with an icon, a heading, and 2-3 supporting points
- Bottom italic line: the integration point — what makes the three add up to more than their parts

**Pattern D: The Denser Technical Pattern (Technical voice only)**
- Allows a 5-row comparison, a layered diagram, or an assumption table
- Rule of 3 still applies to the *speaker's emphasis* (they speak to 3 of the 5 rows) even if the slide shows more
- The Technical voice audience can read and process density that would overwhelm an exec audience

**What NOT to make (in non-Technical voices):**
- A 12-row conformance table on a single slide (use Pattern A and put the rest in the appendix)
- A wall of bullets with no structure
- A diagram so complex it requires the speaker to walk through 8 boxes

---

## Slide role 5: Why — What it means for the audience

**Purpose:** Translate the proposal into the audience's language. Frame the cost honestly. The Diamond's Application facet.

**Pattern A: The Honest Cost Comparison (Boardroom — when there's a price gap)**
- Title that frames the trade: "The cost of being right vs. being cheap"
- Two large blocks side-by-side: the cheaper option on the left (gray), the recommended option on the right (navy)
- Each block has: option name, big price, one-line summary, then "What you give up" / "What you get" with 3 bullets
- Bottom centered italic line: the bottom line in 1-2 sentences

**Pattern B: The Strategic Frame (Boardroom — when there's no obvious cost gap)**
- Title that names the strategic implication: "Why this is the platform decision, not the procurement decision"
- A central headline statement
- 2-3 supporting paragraphs in plain language, with key phrases highlighted
- A visual that anchors the strategic claim (a graph, a quadrant, a map)

**Pattern C: The Operational Reality (Operator — when the audience cares about ongoing impact)**
- Title that names the ongoing change: "What changes for your operations team on day 1"
- A before/after table or two-column comparison
- Concrete examples, not abstractions ("Tickets per week drop from ~40 to ~12" not "improved operational efficiency")

**Pattern D: Why this design (Technical)**
- Title names the design choice: "Why sharded Postgres, not Spanner"
- Tradeoffs named explicitly in a 3-row table or list
- Bottom line: which tradeoff is the one that decided it, and why it matches *this* workload

**Pattern E: What this means we should do differently (Reflective)**
- Title acknowledges the learning: "What this changes about our migration approach"
- 3 specific changes to the operating model
- Italic line: "These are the changes we're committing to. Two more are still in discussion."

**The Why slide is where most decks fail.** Don't repeat the What. Don't dump features. Translate.

---

## Slide role 6: Magic Wand — End with wanting

**Purpose:** Paint the picture of success. State the ask. End the room wanting the next step.

**Pattern:**
- Title that names the ask plainly: "What we need from you today" (Boardroom/Operator/Technical) or "Where we're heading from here" (Reflective)
- Eyebrow above the picture-of-success line: "BY [DATE] — IF WE DECIDE THIS WEEK" (Boardroom) or "BY [DATE], HERE'S WHERE WE INTEND TO BE" (Reflective)
- The picture in one line, large type
- Below: 3 commitments (Rule of 3) in a 3-column layout
- Each commitment has: a colored bar with the timing label, the WHAT in bold, the WHY in italic
- Bottom centered line: the closing rhythm phrase, BOLD, in brand color

**The closing line is the second piece of verbatim memorization** (the first being the opening). It should:
- Match the deck's voice register (see voice.md)
- Be rhythmic — three beats, not four (Boardroom/Operator/Technical) or two-part with acknowledgment (Reflective)
- Echo the title slide's promise

**Good closing lines by voice:**
- **Boardroom:** "One decision today. Eleven sites by September. The pattern for everything that follows."
- **Operator:** "Pilot starts Monday. Office hours every Thursday. If something feels weird, you ping me."
- **Technical:** "RFC open through Friday. Prototype in two weeks. Decision at the next architecture sync."
- **Reflective:** "Here's where we are. Here's where we're heading. Questions are how we get sharper from here."

**Bad closing lines (any voice):**
- "Thank you for your time and attention." (says nothing)
- "We hope you'll consider our proposal." (begs)
- "In conclusion, the benefits outweigh the costs." (sleep)
- "Either option works." (Boardroom-thud — but acceptable phrasing in Reflective voice if framed as "and that's by design")

**Speaker notes for the Magic Wand slide:**
After delivering the closing line, SHUT UP. Three-second rule. Make them speak first. The silence is the close, not the words.

---

## Slides that should NOT exist

These are deckware. They feel safe but waste the audience's attention.

| Don't make | What to do instead |
|---|---|
| Agenda / objectives slide | Cover it in the Setup slide's speaker notes — the presenter says it once |
| "Thank you" closing slide | The Magic Wand IS the closing |
| "Q&A" slide | Just stop talking after the Magic Wand line |
| "About us" slide | If credibility matters, weave it into the How slide |
| Stakeholder/team list | If it matters, mention names in speaker notes |
| Multi-bullet "executive summary" | The What slide does this |
| "Next steps" wrap-up | The Magic Wand slide IS the next steps |

---

## Appendix patterns

The appendix is where ruthlessness is rewarded. Move there:

- The full data tables (the 12-row conformance, the 30-row pricing, the full RACI)
- Detailed timelines and Gantt charts
- Technical architecture diagrams
- Vendor capability slides
- Case studies and references
- Methodology/approach diagrams

Each appendix slide should have a clear title and be self-contained — the presenter may jump to it cold during Q&A.

---

## Speaker notes pattern (every slide gets these)

For every slide, write speaker notes that contain:

1. **Slide role:** "SETUP" or "WHAT" or "HOW" etc.
2. **BME of this slide:** Beginning, Middle, End in one sentence.
3. **What to say:** A specific verbal pattern or example, with timing if relevant ("90 seconds"). Match the voice register.
4. **Repetition with Variation:** 2-3 alternative ways to land the slide's point, using the voice's preferred angles (see delivery.md).
5. **Curveball prep:** If a likely question lands here, the technique and a starter answer.
6. **Linkage out:** "This leads us to..." — the bridge sentence to the next slide.

Speaker notes are the script. Slides are the storyboard. The audience sees the storyboard. The presenter reads the script.
