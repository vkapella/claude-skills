# Expected behavior — 05 Ambiguous

## Voice
- **Should be ASKED, not inferred.**
- "Mixed audience" + a topic ("data platform") that doesn't strongly signal any of the four voices = genuine ambiguity. This is the case where the inference shortcut should NOT fire.
- Claude should present the voice question via `ask_user_input_v0` with all four options visible.

## Failure modes to watch for
- Silently defaulting to Boardroom = fail (this is the prior behavior the patch was designed to fix).
- Claiming an inference confidently when the prompt genuinely doesn't support one = fail.
- Asking the voice question on prompts where the inference IS clear (the other four fixtures) = also fail — that's over-asking.

## Other interrogation behavior
- Should still ask the prose questions (outcome, must-include facts).
- Should still ask the time slot if not specified — wait, time slot IS specified ("30 minutes"), so don't re-ask.
- Audience IS specified ("Mixed"), so don't re-ask audience either.
- The interrogation should feel minimal — only ask what's truly missing.

## Both files produced (eventually, after the user answers)
- Same two-output rule applies once the user picks a voice.
