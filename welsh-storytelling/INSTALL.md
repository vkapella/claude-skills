# Installing and Publishing the welsh-storytelling skill

This guide covers four scenarios — pick the one that matches what you want to do.

| Scenario | Use this section |
|---|---|
| Try the skill in a chat right now (one-time) | **Section 1** |
| Use the skill across all your chats | **Section 2** |
| Share with your team | **Section 3** |
| Publish broadly (Anthropic skills marketplace, GitHub) | **Section 4** |

---

## What's in this folder

```
welsh-storytelling/
├── SKILL.md                              ← entry point, read first
├── INSTALL.md                            ← this file
├── CHANGELOG.md                          ← behavioral changes per version
├── references/
│   ├── frameworks.md                     ← all Welsh frameworks
│   ├── voice.md                          ← the four voice registers (v1.1+)
│   ├── delivery.md                       ← Story Guide content rules
│   └── slide_patterns.md                 ← slide patterns by role
├── templates/
│   ├── interrogation.md                  ← intake script with voice inference
│   └── story_guide_template.md           ← Story Guide skeleton
├── examples/
│   ├── build_deck_example.py             ← working deck builder (BNY, Boardroom voice)
│   └── build_story_guide_example.py      ← working Story Guide builder (BNY, Boardroom voice)
└── tests/                                ← prompt fixtures and expected behaviors
    ├── README.md                         ← how to run regression checks
    ├── prompts/                          ← 5 test prompts (one per voice + ambiguous)
    └── expected_behavior/                ← what each prompt should produce
```

The skill is self-contained. It depends on `python-pptx` and `python-docx` (both standard) and stacks with whatever brand/format skill is available in your environment (`wwt-presentation`, public `pptx`, public `docx`).

---

## Section 1: Try it in a chat right now (one-time)

The fastest path. No installation. Works in any Claude.ai conversation.

1. Zip this folder: `welsh-storytelling.zip`
2. Start a new Claude conversation
3. Upload the zip
4. Tell Claude: *"This is a skill. Unzip it and use it for this conversation. Now build me a deck on [your topic]."*

Claude will read the SKILL.md, follow the framework references, and produce both files. The skill is active only for that conversation.

Good for: testing, demos, trying out frameworks before committing.

---

## Section 2: Use it across all your chats (per-user)

If you have a Claude Pro, Team, or Enterprise account, you can upload the skill once and have it available everywhere.

### Option A: Through the Claude.ai UI (recommended for most people)

1. Go to **claude.ai** → click your profile → **Settings** → **Capabilities** → **Skills**
2. Click **Upload skill**
3. Drag in the `welsh-storytelling` folder (or zip it first if the UI requires)
4. Confirm — the skill now appears in your skills list

The next time you ask Claude to build a deck or pitch, the skill triggers automatically based on its description. No need to mention it by name.

> **Note:** The exact location of the Skills upload UI may have moved since this guide was written. If you don't see it in Settings → Capabilities, search the Claude help docs for "upload skill" or check **Settings → Features**. I'd verify the current path with a quick search before walking your team through it.

### Option B: As an Anthropic API user

If you're calling the Claude API directly with the `agent_skills` capability, mount the skill folder as part of your skills directory and reference it in the API call. See Anthropic's API documentation for the current `skills` parameter shape.

---

## Section 3: Share with your team

Three ways, in increasing levels of formality:

### Quick share (just hand them the folder)

1. Zip the `welsh-storytelling` folder
2. Drop it in shared storage (SharePoint, Google Drive, Slack)
3. Each teammate uploads it via the path in Section 2

This works fine for a small team. Downside: when you update the skill, everyone has to re-upload.

### Team workspace (Claude for Work / Enterprise)

If your organization has a Claude Team or Enterprise plan, an admin can install the skill at the workspace level so everyone gets it automatically.

1. The workspace owner goes to **Workspace settings** → **Skills**
2. Uploads the skill folder
3. The skill becomes available to every member of the workspace

When you update the skill, the owner re-uploads once and everyone sees the new version.

### Internal Git repo

For teams comfortable with version control, the cleanest approach:

1. Create an internal Git repo: `your-org/claude-skills/welsh-storytelling/`
2. Commit the folder there with a CHANGELOG.md tracking versions
3. Document the install steps in your team's onboarding
4. Use Git tags for releases (`welsh-v1.0`, `welsh-v1.1`)

This is what I'd recommend for WWT specifically — alongside any other internal skills (wwt-brand, wwt-presentation, etc.). Treat the skill as code. See the repo-root `AGENTS.md` for the recommended GitHub workflow.

---

## Section 4: Publish broadly

If you want to share this beyond your team — public GitHub, the Anthropic skills marketplace, or a vendor's distribution channel — there are a few extra steps.

### Step 1: Decide on licensing

The skill incorporates frameworks from Michael Welsh's *The Backstory on Storytelling*. A few considerations:

- **Welsh's frameworks are concepts.** Concepts can be applied and taught. The names ("5 Slide Rule," "Designing for Diamonds," "Arcs of Uncertainty") are likely his trademarks or distinctive coinages.
- **The skill teaches Claude to APPLY the frameworks.** It does not reproduce the book. The reference files paraphrase the frameworks rather than quote them.
- **For broad publication, get permission.** Reach out to Michael Welsh or his publisher before publishing publicly. A license to apply the named frameworks in software is a different right from quoting the book.
- **Attribute clearly.** Every output of the skill (every Story Guide footer) credits Welsh and the book.

I'd recommend not publishing this publicly without contacting Welsh. For internal/team use this is moot — internal application of published frameworks is normal practice.

### Step 2: Add the publication metadata

Before publishing, add to the SKILL.md frontmatter:

```yaml
---
name: welsh-storytelling
version: 1.1.0
author: [Your Name]
license: [your license — MIT, Apache 2.0, proprietary, etc.]
attribution: "Frameworks from 'The Backstory on Storytelling' by Michael Welsh, applied with permission."
description: "..."
---
```

### Step 3: Pick a distribution channel

- **Anthropic Skills Marketplace** (if/when available) — check `docs.claude.com` for current submission process. Last I knew, Anthropic was curating an official skills directory but the public submission flow was evolving. Verify the current state before submitting.
- **Public GitHub repo** — `github.com/yourname/welsh-storytelling-skill` with a clear README, the LICENSE file, and example outputs.
- **Vendor distribution** — if WWT wants to distribute this to clients as part of a service offering, that's a business conversation, not a publication step.

### Step 4: Versioning discipline

If you publish, expect feedback. Plan for it:

- Maintain a `CHANGELOG.md` documenting changes
- Use semantic versioning (1.0.0 → 1.1.0 for additions, 2.0.0 for breaking changes)
- Tag releases in Git so users can pin to a version

---

## Updating the skill after install

When you change the skill files:

- **Per-user install (Section 2):** delete the old version in your skills list, upload the new folder.
- **Workspace install (Section 3):** workspace owner re-uploads.
- **Git-based install:** users `git pull` the latest.

The skill description (the `description:` field in SKILL.md frontmatter) is what determines when Claude triggers the skill. If you change behavior significantly, update the description to match — otherwise the skill may trigger in wrong contexts or fail to trigger when you'd want.

---

## Testing the skill before broad release

A small fixture suite lives in `tests/`. Use it before every release.

The five prompts in `tests/prompts/` each exercise one voice register plus one ambiguous case:

1. `01_cfo_siem_pitch.txt` — should trigger and infer **Boardroom**
2. `02_sre_rollout.txt` — should trigger and infer **Operator**
3. `03_year_end_review.txt` — should trigger and infer **Reflective**
4. `04_architecture_review.txt` — should trigger and infer **Technical**
5. `05_ambiguous.txt` — should trigger and **ask** the voice question (not infer)

For each, compare the run against the matching `tests/expected_behavior/*.md` file. Pass criteria:

- The interrogation step **states the inferred voice** (or asks, for the ambiguous case)
- Headlines, What-slide sentence, and Magic Wand close match the patterns in `references/voice.md` for that voice
- The "Avoid in this voice" patterns do NOT appear
- Both `.pptx` and `.docx` are produced
- Slide count is within the time-slot bound

Also run a small negative set — prompts that should NOT trigger the skill at all:

- "Write me an email to the team about Friday's offsite."
- "Summarize this PDF."
- "Help me debug this Python error."

If trigger accuracy is off, refine the `description:` field — that's the lever that controls when Claude reaches for the skill.

---

## Troubleshooting

**The skill doesn't trigger when I ask for a deck.**
The description may not match the user's phrasing. Look at the actual phrases used in your test prompts and make sure the description includes those words.

**The skill triggers but only produces the deck, no Story Guide.**
The "two-output pattern" instruction in SKILL.md may be getting deprioritized. Reinforce it — make the section header more visible, repeat the rule once more in the execution flow.

**The deck defaults to Boardroom voice for an obvious Operator or Reflective prompt.**
The voice inference table in `templates/interrogation.md` may not be reaching Claude in Step 2. Verify SKILL.md Step 2 explicitly says to read `references/voice.md`. Run the matching test fixture in `tests/prompts/` to confirm.

**The Story Guide formatting looks wrong.**
The python-docx code in `examples/build_story_guide_example.py` is the working reference. If a Story Guide comes out misformatted, compare against that example and identify what's different.

**The skill works but the slides don't follow WWT brand.**
The skill stacks with `wwt-presentation` — make sure that skill is also installed in the same workspace. Without it, the skill falls back to generic styling.

---

## Recommended next steps for WWT specifically

Given the WWT context, here's the path I'd take:

1. **Internal Git repo:** put `welsh-storytelling` alongside `wwt-presentation` and `wwt-brand` in a shared internal skills repo
2. **Workspace install:** the WWT Claude workspace admin uploads it once for everyone
3. **Onboarding:** add a one-liner to the team Confluence/Notion: *"For client deck builds, just ask Claude to build the deck — the Welsh storytelling skill will trigger automatically and produce both the deck and a Story Guide."*
4. **Feedback loop:** after the first 5-10 real client uses, gather what worked and what didn't. The Curveball Prep section especially benefits from real-world examples.
5. **Permission conversation:** if WWT wants to use this in client-facing work, brief Welsh or his publisher. Most thought leaders welcome their frameworks being applied — but it's a courtesy worth extending.
