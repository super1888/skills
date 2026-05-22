# Extraction Framework

Use this reference when a source is long, dense, or mixes tutorial, opinion, and implementation detail.

## Extraction Passes

1. **Intent Pass**: identify what task the future skill should help with.
2. **Concept Pass**: list domain terms, components, actors, inputs, outputs, and invariants.
3. **Logic Pass**: extract design rationale, sequencing, architecture, constraints, and decision rules.
4. **Operation Pass**: convert tutorial steps into executable agent workflow.
5. **Risk Pass**: capture edge cases, anti-patterns, validation methods, and failure recovery.
6. **Trigger Pass**: identify natural user phrases, domain keywords, false positives, and exclusion cases.
7. **Disclosure Pass**: decide what belongs in `SKILL.md` versus `references/`.
8. **Validation Pass**: create one realistic prompt to test trigger and output stability.

## Distillation Heuristics

- Convert repeated advice into rules.
- Convert narrative examples into checklists.
- Convert implementation details into conditions and steps.
- Convert caveats into red flags and validation gates.
- Convert diagrams or architecture descriptions into text-based component relationships.
- Convert source-specific warnings into guardrails and refusal-or-ask-first rules.
- Convert representative examples into validation prompts when they help test the skill.

## Keep In `SKILL.md`

- Trigger description
- Core workflow
- Required output shape
- Critical constraints
- Reference loading guidance

## Move To `references/`

- Source summaries and mappings
- Long examples
- Variant-specific details
- Deep architecture notes
- Extended checklists
- Prompt/output samples
