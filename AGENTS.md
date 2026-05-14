# AGENTS.md

Conventions for any agent (human or AI) making changes to skills in this repo. This file is read first by Claude when working on this repo and is the source of truth for "how do we change things here."

## What this repo contains

A collection of Claude skills, one per top-level folder. Each skill is a self-contained set of markdown references, templates, example code, and tests that Claude reads at runtime to handle a category of task.

## Core principles

1. **Skills are code.** They live in git. They get versioned, branched, reviewed, tagged, and rolled back like any other source code.
2. **Behavioral changes are the unit of work.** A diff that doesn't change Claude's behavior probably doesn't belong in CHANGELOG. A behavior change that has no diff is impossible.
3. **Tests live next to the skill.** Each skill has a `tests/` folder with prompt fixtures and expected behaviors. After every change, the matching fixtures get re-run.
4. **GitHub is the source of truth.** The deployed copy (Claude skills UI, mounted path, etc.) is a *sync target*, not the source. The push doesn't update Claude — a separate sync step does.

## Standard workflow for a skill change

This is the workflow to follow whenever you're modifying an existing skill in this repo. Each step is intentionally explicit because skill behavior is hard to verify automatically, so the discipline matters.

### Step 1 — Open a GitHub issue

Every change starts with an issue. Title format: `[<skill-name>] <one-line behavioral change>`.

Issue body should answer:
- **What behavior changes?** Describe Claude's output before vs. after.
- **Why?** What problem is this solving, or what new capability is being added?
- **Which files do you expect to touch?** Doesn't have to be exhaustive — directional is fine.
- **Test impact:** Will existing test fixtures still pass? Need new ones?

Label the issue with the affected skill name (e.g. `skill:welsh-storytelling`).

### Step 2 — Create a branch

Branch naming: `<skill-name>/<short-slug>` — e.g. `welsh-storytelling/voice-registers`, `wwt-presentation/dark-mode-layout`.

```bash
git checkout main
git pull
git checkout -b <skill-name>/<slug>
```

Branch from `main`, never from another feature branch.

### Step 3 — Make the changes

Edit the relevant files. Common patterns:

- **A new behavior requires a new reference file.** Add to `references/`, then update SKILL.md execution flow to read it, then update CHANGELOG.
- **A change to existing behavior usually touches SKILL.md and one or more references.** Cross-reference files that mention the changed behavior get updated even if their "core" content is unchanged — stale cross-references rot fast.
- **A new question in the interrogation flow.** Update `templates/interrogation.md` AND SKILL.md Step 2 AND the sample interrogation flow at the bottom of interrogation.md.
- **A new test case.** Add the prompt to `tests/prompts/` and the matching expectation to `tests/expected_behavior/`. Update `tests/README.md` if the table of test cases changes.

For each file you touch, ask: *does this file mention the thing I'm changing somewhere else?* If yes, update that too. Stale cross-references in markdown skill files are silent failures.

### Step 4 — Update the per-skill CHANGELOG

Open `<skill>/CHANGELOG.md`. Add an entry at the top under "[Unreleased]" (or create that section if missing).

Required sections:
- **### Added** — new files, new behaviors
- **### Changed** — modifications to existing files/behaviors
- **### Behavioral effect on output** — what Claude does differently after this change

Don't describe the diff. Describe what Claude *does differently* now. If you can't articulate a behavioral effect, you may not actually be making a meaningful change.

### Step 5 — Run the test fixtures

In a fresh Claude conversation (NOT the one you're using for development):

1. Install the updated skill locally (sync your branch to wherever you load skills from).
2. For each prompt in `<skill>/tests/prompts/`, paste it in and let Claude run the full flow.
3. Compare against the matching `<skill>/tests/expected_behavior/*.md`.

A fixture **passes** when the qualitative properties in the expected_behavior file are met. These are eyeball checks, not automated assertions — there's no CI runner. The discipline is in actually running them.

If a fixture fails:
- If the failure is unintended → that's a regression. Fix the change before merging.
- If the failure is the intended new behavior → update the expected_behavior file in the same commit. The fixture file is part of the change.

If you've added a new test fixture, also run the existing four to make sure you didn't regress them.

### Step 6 — Run the negative tests

A few prompts that should NOT trigger the skill:

- "Write me an email to the team about Friday's offsite."
- "Summarize this PDF."
- "Help me debug this Python error."

If any of these now trigger the skill, the SKILL.md `description:` field is too broad. Tighten it before merging.

### Step 7 — Commit

```bash
git add <skill>/
git commit -m "<skill-name>: <one-line behavioral change>

<a few sentences explaining what changed and why>

Refs #<issue-number>"
```

Commit messages should reference the issue. Use the `Refs #N` line in the trailer.

### Step 8 — Push and open a PR

```bash
git push -u origin <skill-name>/<slug>
```

Open a PR against `main` on GitHub. Use this template:

```
Closes #<issue-number>

## What changed
<paste the CHANGELOG entry>

## Files touched
<bullet list of changed files with one line each on what changed>

## Test results
- 01_<fixture>: PASS / FAIL (link to expected_behavior if updated)
- 02_<fixture>: PASS / FAIL
- ...
- Negative tests: PASS / FAIL

## Anything reviewers should look at specifically
<callouts>
```

### Step 9 — Review and merge

For solo work: self-review the PR diff in the GitHub web UI. Reading the diff in a different surface than where you wrote it catches mistakes. Then squash-merge to main.

For team work: at least one reviewer who didn't write the change. The reviewer's job is to verify (a) the CHANGELOG entry accurately describes the behavioral change, (b) test fixtures actually got re-run, and (c) no stale cross-references were left in the skill files.

```bash
# After merge
git checkout main
git pull
git branch -d <skill-name>/<slug>
```

### Step 10 — Tag the release (when warranted)

Not every change gets a tag. Tags mark *named rollback points* — moments you'd want to be able to return to. Rules of thumb for when to tag:

- A new minor version of a skill (`<skill>-v1.1`, `<skill>-v1.2`) → tag it.
- A change that significantly affects what Claude outputs → tag it even if you'd call it a patch.
- A pure cross-reference cleanup → don't bother tagging.

```bash
git tag -a <skill>-v<version> -m "<skill>: <one-line summary>"
git push --tags
```

Tags are named per-skill (`welsh-v1.1`) rather than globally so that one skill's release doesn't imply anything about another's state.

### Step 11 — Close the issue

The PR-issue link from Step 8 closes the issue automatically on merge if you used `Closes #N`. Verify the issue actually closed; sometimes the auto-close misses.

### Step 12 — Sync to the Claude deployment

**This is the step that actually changes Claude's behavior in production.** GitHub doesn't talk to Claude. The merge to main doesn't update the skill Claude reads at runtime.

Sync target depends on the deployment:
- **Skills UI upload:** open the relevant skill in Claude's settings, replace the changed files, save. New chats will see the updated skill.
- **Mounted path:** copy the updated folder into the deployment path. New chats will see the updated skill on next read.

Don't skip this step. A change merged to main and not synced is a change that doesn't exist for users.

### Step 13 — Smoke-test in production

After syncing, run *one* of the test fixtures in a real Claude conversation as a smoke test. This catches issues where the sync didn't take effect or the deployment environment differs from what you tested against locally.

---

## Versioning

Per-skill semantic versioning:
- **MAJOR** (`v2.0`) — Breaking change to a skill's interface or default behavior such that an existing deployment would produce noticeably different outputs without any user-side change. Rare.
- **MINOR** (`v1.1`) — New capability added that doesn't break existing usage. The voice register patch was the canonical example.
- **PATCH** (`v1.1.1`) — Bug fix, cross-reference cleanup, typo. Rarely tagged.

The repo as a whole does NOT have a single version. Each skill versions independently.

---

## File layout conventions

```
<skill-name>/
├── SKILL.md              # frontmatter + entry point + execution flow
├── INSTALL.md            # how to install this skill into Claude
├── CHANGELOG.md          # per-skill behavioral changelog
├── references/           # files Claude reads on demand
├── templates/            # reusable scaffolds (intake scripts, doc templates)
├── examples/             # working code samples (optional but useful)
└── tests/
    ├── README.md         # how to run the regression checks
    ├── prompts/          # one .txt per test case
    └── expected_behavior/ # one .md per prompt, named identically
```

Don't add other top-level folders inside a skill without updating this section of AGENTS.md.

---

## Working with Claude as the agent

When Claude is making changes to this repo (via a connector, in an interactive session, or otherwise), Claude should:

1. **Read AGENTS.md first** — this file.
2. **Read the affected skill's SKILL.md, CHANGELOG.md, and INSTALL.md** before proposing changes — to understand the current state and conventions.
3. **Propose the change as a list of file edits before writing them.** Make the human approve the plan before executing it. Skills are subtle; an unreviewed plan is more dangerous than an unreviewed line of code.
4. **Update CHANGELOG and cross-references** in the same change. Don't leave them for later.
5. **Articulate the behavioral effect** in the proposal. "I'll update voice.md to add Vendor voice" is not enough; "Adding a fifth Vendor voice that defaults for sales-to-customer pitches; SKILL.md inference table will gain a row; expected effect is that decks for prospect meetings will substitute pricing-forward Magic Wand patterns" is the kind of articulation that lets a human evaluate the proposal.
6. **Run the test fixtures mentally before merging.** For each existing fixture, predict whether the change would alter the expected behavior. Flag any that need updating.

When in doubt, Claude should ask the human rather than guess at convention.

---

## What this repo intentionally does NOT have

- **A CI pipeline.** Skill behavior can't be automatically asserted — fixtures are eyeball-diff territory. CI here would be theater.
- **A single version number for the whole repo.** Skills evolve independently. The repo-level CHANGELOG only tracks structural changes (skills added/removed/renamed).
- **A formal contribution process for external contributors.** This is currently a personal/small-team repo. If that changes, replace this paragraph.

---

## Quick reference

| I want to... | Read | Then do |
|---|---|---|
| Change a skill's behavior | This file, then `<skill>/SKILL.md` | Steps 1-13 above |
| Add a new skill | This file, then an existing skill as a template | Issue → branch → folder → tests → PR → tag |
| Roll back a skill | `git tag --list` to find the version | `git checkout <tag> -- <skill>/` then commit + sync |
| Test a skill change locally | `<skill>/tests/README.md` | Run fixtures in a fresh Claude conversation |
| Sync a merged change to Claude | The deployment-specific instructions in `<skill>/INSTALL.md` | Skills UI re-upload or path copy |
