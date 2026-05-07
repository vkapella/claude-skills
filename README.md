# claude-skills

Personal skills repository for Anthropic Claude. Each top-level folder is one skill — a self-contained set of instructions, references, templates, and example code that Claude reads to handle a category of task.

## Structure

```
claude-skills/
├── README.md                    # this file
├── CHANGELOG.md                 # repo-level changes (skills added/removed/renamed)
├── .gitignore
└── welsh-storytelling/          # one folder per skill
    ├── SKILL.md                 # entry point — frontmatter + instructions
    ├── INSTALL.md               # how to install this skill into a Claude environment
    ├── CHANGELOG.md             # per-skill changes
    ├── references/              # files Claude reads on demand for context
    ├── templates/               # reusable scaffolds (intake scripts, doc templates)
    ├── examples/                # working code samples Claude can crib from
    └── tests/                   # sample prompts + expected behavior for regression checks
```

## Skills in this repo

| Skill | Purpose |
|---|---|
| `welsh-storytelling` | Apply Michael Welsh's storytelling frameworks when building presentations. Produces a `.pptx` deck and a companion `.docx` Story Guide every time. Voice-aware (Boardroom, Operator, Technical, Reflective registers). |

## Conventions

**One skill per folder.** Skills can reference each other by absolute path (e.g. `/mnt/skills/user/welsh-storytelling/`), so keeping them as siblings in one repo makes cross-references easier to maintain.

**Edit here, sync to deployment.** This repo is the source of truth. The deployed skill location (e.g. `/mnt/skills/user/...` in Claude environments) is read-only at runtime. Workflow: edit locally → commit → push → sync to the deployment target.

**Tag releases when a skill is in a good state.** `git tag welsh-v1.2 && git push --tags`. Tags become named rollback points beyond just "the previous commit."

**Per-skill CHANGELOG.md.** A skill's behavior can shift dramatically from a six-word edit to its description (it changes when the skill triggers). One line per change describing the *behavioral* delta is more valuable than the diff.

**Sample outputs as test fixtures.** Each skill's `tests/` folder holds prompts + redacted expected outputs. After a change, re-run the prompts and eyeball-diff against the saved outputs. This is the closest thing to a unit test prompt-shaped code can have.

## Installing a skill into Claude

Each skill has its own `INSTALL.md` with specific instructions. The general pattern is to copy the skill folder into your Claude skills directory (commonly `/mnt/skills/user/<skill-name>/`) or upload it through the skills UI.

## Contributing changes

1. Make changes on a branch.
2. Update the per-skill `CHANGELOG.md` with a one-line behavioral note.
3. If the change could affect output character (tone, structure, length, triggers), add or update a fixture in the skill's `tests/` folder.
4. Open a PR. Squash on merge.
5. Tag a release if the change is significant.
