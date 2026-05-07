# Voice Reference

Welsh's structural frameworks are universal. The **register** the deck speaks in is not. The same arc, the same Rule of 3, and the same Diamond can land as confident exec pitch, plainspoken ops briefing, rigorous architecture review, or measured leadership reflection — depending on which voice the deck adopts.

Read this file alongside `slide_patterns.md` whenever generating a deck. The patterns in `slide_patterns.md` default to **Boardroom** voice (punchy three-beat closes, decision-forcing headlines). Substitute the relevant voice patterns from this file based on the user's selection in the interrogation step.

If voice was not explicitly chosen, infer it from the audience answer using the mapping at the bottom of this file, and **state the inferred voice in your response** so the user can correct it.

---

## Voice 1: Boardroom (exec-to-exec)

**When to use:** C-suite, board, steering committee, sales pitch with a buying decision attached, any room where the goal is a yes/no on a specific ask.

**Posture:** Confident. Decision-forcing. Comfortable with brevity. Treats the audience's time as the scarcest resource. Cost framing is explicit and quantified.

**Headline rhythm:** Punchy. Three beats. Numbers in the headline.

**Hedging:** Minimal. State the recommendation. Caveats live in the appendix.

**What-slide sentence patterns:**
- "Deploy 11 microbranches on Cisco SD-WAN over 6 months — the only option that fixes all three failures."
- "Replace the legacy CRM with Salesforce by Q2 — saves $2.4M over five years."
- "Three options. One we recommend."

**Magic Wand patterns:**
- "One decision today. Eleven sites by September. The pattern for everything that follows."
- "Sign this week. Ship by July. Save twenty million by year-end."

**Avoid in this voice:** "It depends." Long acknowledgments of complexity. Closing with anything other than the ask.

---

## Voice 2: Operator (operator-to-operator)

**When to use:** Internal team rollouts, ops reviews, peer-to-peer briefings, runbook walkthroughs, change-management sessions for the people doing the work.

**Posture:** Plainspoken. Slightly understated. Comfortable with caveats and rough edges. Leads with what changes Monday morning, not with strategic framing. Respects the audience's craft.

**Headline rhythm:** Direct, declarative, conversational. Avoids rhetorical flourish.

**Hedging:** Honest. "This part is still rough" is a feature, not a bug.

**What-slide sentence patterns:**
- "We're moving the on-call rotation to PagerDuty next month. Here's what changes for you."
- "The new deploy pipeline is faster, but it'll feel different the first week."
- "Three things you'll do differently. Two stay the same. One we're still figuring out."

**Magic Wand patterns:**
- "Pilot team starts Monday. Full rollout in six weeks. Office hours every Thursday until it's boring."
- "If something breaks, you ping me. If something feels weird, you ping me. We'll iterate."

**Avoid in this voice:** Boardroom three-beat closes — they sound like marketing in a peer room. Strategic-sounding phrases ("paradigm shift," "force multiplier"). Pretending the rollout is smoother than it is.

---

## Voice 3: Technical (engineer-to-engineer)

**When to use:** Architecture reviews, design reviews, technical deep-dives, engineering all-hands, any room where the audience can read a diagram and a table and resents oversimplification.

**Posture:** Precise. Evidence-first. Names tradeoffs explicitly. Comfortable with density on the How slide. Treats the audience as peers who can handle nuance.

**Headline rhythm:** Architectural claim or constraint statement. Often names the tradeoff in the headline itself.

**Hedging:** Calibrated. Distinguishes "we measured this" from "we believe this" from "we're guessing." Assumptions are explicit.

**What-slide sentence patterns:**
- "Sharded Postgres over a single Spanner instance — we trade global consistency for 4× write throughput and a known operational model."
- "Three constraints shaped this design. We relaxed the third."
- "We chose option B. Option A is better in two of three dimensions; the third is the one that matters for our load profile."

**How-slide latitude:** This voice is allowed denser How slides — a 5-row comparison, a layered diagram, an explicit assumption table. Rule of 3 still governs the *speaker's emphasis*, even if the slide shows more.

**Magic Wand patterns:**
- "RFC open for review through Friday. Prototype in two weeks. Decision point at the next architecture sync."
- "Three open questions. One blocker. We need a call on the blocker today."

**Avoid in this voice:** Glossing over tradeoffs. Hand-wavy "best-of-breed" or "scalable" without numbers. Boardroom dollar-savings closes — the audience cares about the design, not the spreadsheet.

---

## Voice 4: Reflective (overview / honest-leader)

**When to use:** Post-mortems, year-end reviews, transformation talks, "where we are and what we don't yet know" sessions, customer-trust briefings after an incident, any talk built on the **Arc of Uncertainty**.

**Posture:** Measured. Grounded. Comfortable with the trough. Doesn't oversell the recovery. Ends with a direction or a commitment to learn, not a demand.

**Headline rhythm:** Reflective, sometimes two-part. Often acknowledges the difficulty before stating the position.

**Hedging:** Welcomed. "We don't yet know" is a strength here, not a weakness. The "I Don't Know" list from the Story Guide is a first-class citizen of the deck itself.

**What-slide sentence patterns:**
- "We held the line. Here's what almost broke us."
- "Three things we got right. Two we got wrong. One we're still arguing about."
- "The strategy mostly worked. The places it didn't are where we're investing next."

**Magic Wand patterns:**
- "We're not asking for a decision today. We're asking you to walk out knowing what we know — and what we don't."
- "Three commitments for next year. One we'll measure publicly. Two we'll report on quarterly."
- "Here's where we are. Here's where we're heading. Questions are how we get sharper from here."

**Avoid in this voice:** Boardroom closes — they ring false in a reflective room. Pretending uncertainty is resolved when it isn't. Heroic narratives ("how we saved the day"). Forcing a Magic Wand ask onto a learning talk.

**Important rule override:** The skill's general "Never close with a thud — end with wanting" rule is **conditional on voice**. In Reflective voice, ending with appropriate uncertainty *is* the right close. Forcing a decision-ask onto a post-mortem is exactly the failure mode that produces the flamboyant, oversold feel this voice is designed to prevent.

---

## Voice inference defaults

If the user did not explicitly select a voice, infer it from the audience answer (Q1) and the topic, and **state the inference in plain language** before generating the outline:

| Audience (Q1) | Default voice | Override signals to watch for |
|---|---|---|
| Executive | Boardroom | If the topic is a post-mortem or honest review → switch to Reflective |
| Peer | Operator | If the topic is architectural or design-review → switch to Technical |
| Client | Boardroom | If the relationship is mature and the topic is partnership/learning → Reflective |
| Mixed | Reflective unless context says otherwise | If a clear decision-ask exists → Boardroom; if it's an architecture room → Technical |

Topic signals that override audience defaults:
- "Post-mortem," "incident review," "year in review," "what we learned" → **Reflective**
- "Architecture," "design review," "RFC," "system design," "tradeoffs" → **Technical**
- "Rollout," "runbook," "team enablement," "ops handoff" → **Operator**
- "Recommendation," "proposal," "investment ask," "buying decision" → **Boardroom**

---

## How voice affects each slide role

A quick reference for how the same slide role expresses differently across voices:

| Slide role | Boardroom | Operator | Technical | Reflective |
|---|---|---|---|---|
| **Title** | Promise + decision rhythm | Plain "what this is about" | Constraint or claim | Two-part: acknowledgment + position |
| **Setup** | Stakes / cost of inaction | What's changing for the team | Problem statement + constraints | What we believed at the start |
| **What** | One-sentence recommendation | One-sentence change | Architectural claim w/ tradeoff | "Here's what we now believe" |
| **How** | 3-row comparison, decision-forcing | 3 concrete process changes | Denser is OK — assumption table, layered diagram | The journey: what we tried, what worked, what didn't |
| **Why** | Cost/benefit, dollar-framed | Day-1 operational reality | Why this design over alternatives | What this means we should do differently |
| **Magic Wand** | The ask + three-beat close | Pilot dates + office hours | RFC dates, prototype, decision point | Direction + commitments to learn |

---

## Mixing voices

Most decks are single-voice. A few legitimate cases mix:

- **Boardroom front + Technical appendix.** The exec deck closes Boardroom; the appendix slides for Q&A are Technical. Use this when the audience is mixed-seniority and questions will go deep.
- **Reflective Setup + Boardroom close.** A talk that opens by acknowledging difficulty ("here's what we got wrong last year") and closes with a confident ask for the new investment. Powerful but easy to botch — the pivot has to be earned, not just declared.

Avoid mixing more than two voices in one deck. The audience will feel the shift and lose trust.
