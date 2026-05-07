# Changelog — welsh-storytelling

Behavioral changes to this skill. Each entry describes what *Claude does differently* as a result of the change, not just what files moved.

## [1.1.0] — 2026-05-07

### Added
- **Voice register selection.** Four voices: Boardroom (exec-to-exec, decision-forcing), Operator (peer-to-peer, plainspoken), Technical (engineer-to-engineer, evidence-first), Reflective (honest leadership, comfortable with uncertainty). Selected via the interrogation step or inferred from audience + topic.
- New file: `references/voice.md` — full pattern library per voice (headlines, What-slide sentences, Magic Wand patterns, when-to-use, what-to-avoid).
- Voice inference table in `templates/interrogation.md` — Claude states the inferred voice in plain language ("Reading this as Technical voice — sound right?") rather than asking outright when the inference is clear.

### Changed
- The "End with wanting — never close with a thud" rule is now **conditional on voice**. In Reflective voice, ending with calibrated uncertainty is the *correct* close; forcing a Magic Wand decision-ask onto a post-mortem is the failure mode this voice exists to prevent.
- `SKILL.md` execution flow Step 3 and Step 4 now require reading `voice.md` alongside `slide_patterns.md`, and explicitly substituting headlines/closes per the selected voice.
- `templates/interrogation.md` adds Q2 (voice) between the existing Q1 (audience) and Q2 (time slot); other questions renumbered Q3-Q6.

### Behavioral effect on output
- Decks for SRE rollouts, internal team briefings, and architecture reviews no longer default to flamboyant three-beat closes ("Sign this week. Ship by July. Save twenty million by year-end.").
- Post-mortems and year-end reviews now end with direction and learning commitments rather than forced investment-asks.
- Boardroom decks (the prior default for everything) are unchanged when audience and topic match.

## [1.0.0] — initial version

- Welsh's structural frameworks, 5-Beat arc, Rule of 3, Diamonds, BMEs.
- Two-output pattern: `.pptx` deck + `.docx` Story Guide.
- Skill stacks with `wwt-presentation` / `wwt-brand` for WWT context, public `pptx` / `docx` skills otherwise.
