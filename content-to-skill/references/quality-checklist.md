# Generated Skill Quality Checklist

Use this checklist before delivering any generated skill.

## Trigger Precision

- `description` names the source domain and user task types.
- It includes likely natural-language trigger phrases.
- It excludes unrelated or overly broad tasks.
- It describes generated artifacts, not just the source topic.

## Output Stability

- `SKILL.md` defines a fixed response structure.
- The workflow order is explicit and repeatable.
- Required sections are named consistently.

## Source Traceability

- `references/source-map.md` records source links or files.
- Source ideas are paraphrased and mapped to skill rules.
- Ambiguities and conflicts are documented.
- Copyright-sensitive passages are summarized instead of copied.

## Context Efficiency

- `SKILL.md` avoids long quotes and raw article content.
- Detailed examples live in references.
- Reference loading instructions are conditional.

## Maintainability

- New cases can be added as new reference files.
- The main workflow does not need changes for every new example.
- File names are stable and descriptive.

## Direct Usability

- The skill folder has a valid `SKILL.md` frontmatter block.
- Optional `agents/openai.yaml` matches the skill purpose.
- The final answer lists created files and a testing prompt.

## Validation Prompt

- A realistic user prompt is included for manual trigger testing.
- The expected output structure is clear enough to compare by inspection.
