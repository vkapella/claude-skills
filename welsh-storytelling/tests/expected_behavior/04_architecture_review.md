# Expected behavior — 04 Architecture review

## Voice
- **Inferred (not asked):** Technical.
- The interrogation message should state the inference: "Reading this as Technical voice — evidence-first, names tradeoffs explicitly, How slide allowed to be denser."
- Signals: "architecture review," "staff and principal engineers," "tradeoffs not necessarily a final yes."

## Structure
- 7-10 slides + appendix (60-min slot).
- 5-Beat arc; the Why slide should be "why this design over the alternative," not "why this saves money."

## Headline character
- Headlines name tradeoffs, not promises. E.g. "Sharded Postgres over Spanner — we trade global consistency for 4× write throughput and a known operational model."
- "Three constraints shaped this design. We relaxed the third." is the kind of structural claim this voice produces.
- The How slide is allowed to carry an assumption table or layered diagram — denser than the default Boardroom How slide.

## Magic Wand character
- Ends with RFC dates, prototype timeline, and a defined decision point — NOT a dollar-savings close.
- Example: "RFC open through Friday. Prototype in two weeks. Decision at the next architecture sync."

## Failure modes to watch for
- Hand-wavy language ("scalable," "best-of-breed") without numbers = fail.
- Boardroom three-beat dollar close = fail — wrong room.
- Glossing over the tradeoff in the headline (saying "Postgres is the right choice" without naming what's given up) = fail.

## Both files produced
- `.pptx` with denser-than-usual How slide acceptable. `.docx` Story Guide with curveball prep weighted toward technical objections (consistency model, operational complexity, migration path).
