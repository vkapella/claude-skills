# Changelog — welsh-storytelling

Behavioral changes to this skill. Each entry describes what *Claude does differently* as a result of the change, not just what files moved.

## [1.1.0] — 2026-05-14

### Added
- **Voice register selection.** Four voices: Boardroom (exec-to-exec, decision-forcing), Operator (peer-to-peer, plainspoken), Technical (engineer-to-engineer, evidence-first), Reflective (honest leadership, comfortable with uncertainty). Selected via the interrogation step or inferred from audience + topic.
- New file: `references/voice.md` — full pattern library per voice (headlines, What-slide sentences, Magic Wand patterns, when-to-use, what-to-avoid, inference table, slide-role-by-voice matrix).
- Voice inference table in `templates/interrogation.md` — Claude states the inferred voice in plain language ("Reading this as Technical voice — sound right?") rather than asking outright when the inference is clear.
- `tests/` folder with five prompt fixtures and matching expected_behavior files, one per voice plus an ambiguous case.

### Changed
- The "End with wanting — never close with a thud" rule is now **conditional on voice**. In Reflective voice, ending with calibrated uncertainty is the *correct* close; forcing a Magic Wand decision-ask onto a post-mortem is the failure mode this voice exists to prevent.
- `SKILL.md` execution flow Step 3 and Step 4 now require reading `voice.md` alongside `slide_patterns.md`, and explicitly substituting headlines/closes per the selected voice.
- `templates/interrogation.md` adds Q2 (voice) between the existing Q1 (audience) and Q2 (time slot); other questions renumbered Q3-Q6.
- `references/frameworks.md` — added a voice cross-reference at the top, voice notes on the Magic Wand row, the Rule of 3, the Diamond, and Arcs of Uncertainty. Extended the "When to use which arc" table with a typical-voice column.
- `references/slide_patterns.md` — added a v1.1 header noting that the example headlines and closing lines default to Boardroom voice and should be substituted from voice.md based on the selected register. Added per-voice example variants to Title, What, Why, and Magic Wand slide roles. Added Pattern D for the Setup slide (Reflective-only "what we believed at the start") and Pattern D for the How slide (Technical-only denser layout).
- `references/delivery.md` — added voice-consistency note at the top, plus voice variation notes on the Core Message, RWV library angles, Curveball technique mix, "I Don't Know" prominence, and verbatim Opening/Closing lines. Clarified that Story Guide *visual* identity is voice-agnostic; only content shifts.
- `templates/story_guide_template.md` — added voice notes throughout the section skeleton. Listed voice-matched angle defaults for the RWV library section.
- `INSTALL.md` — folder tree now includes `voice.md`, the `CHANGELOG.md`, and the `tests/` directory. Testing section updated to point at the fixture suite rather than generic prompts. Added a "deck defaults to Boardroom for non-exec prompts" troubleshooting entry. Bumped SKILL.md frontmatter version example to 1.1.0.

### Unchanged (intentionally)
- `examples/build_deck_example.py` and `examples/build_story_guide_example.py` — these are a working BNY demo that happens to be in Boardroom voice. Kept as-is to serve as a concrete Boardroom reference. A second example in a different voice may be added in a future release.

### Behavioral effect on output
- Decks for SRE rollouts, internal team briefings, and architecture reviews no longer default to flamboyant three-beat closes ("Sign this week. Ship by July. Save twenty million by year-end.").
- Post-mortems and year-end reviews now end with direction and learning commitments rather than forced investment-asks.
- Story Guides reflect the deck's voice in verbatim Opening/Closing lines, RWV library angles, and Diamond facet content.
- Boardroom decks (the prior default for everything) are unchanged when audience and topic match.

## [1.0.0] — initial version

- Welsh's structural frameworks, 5-Beat arc, Rule of 3, Diamonds, BMEs.
- Two-output pattern: `.pptx` deck + `.docx` Story Guide.
- Skill stacks with `wwt-presentation` / `wwt-brand` for WWT context, public `pptx` / `docx` skills otherwise.
