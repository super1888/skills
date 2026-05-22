# Generated Skill Template

Use this template when creating a complete skill from source materials.

## `SKILL.md`

```markdown
---
name: skill-name
description: Use when ...; covers ...; produces ...
---

# Skill Display Name

Use this skill to ...

## Skill Positioning

- Applicable scenarios:
- Core purpose:
- Task scope:
- Target users:
- Non-goals:

## Underlying Thinking

- Source-derived design logic:
- Architecture or workflow principles:
- Decision heuristics:
- Trade-offs:

## Practical Method

1. ...
2. ...
3. ...

## Trigger Conditions

- Use when:
- Strong trigger phrases:
- Domain keywords:
- Do not use when:
- Ambiguity handling:

## Output Format

When using this skill, respond with:

- **Context**: assumptions, inputs, and scope.
- **Core Analysis**: source-specific reasoning or design decomposition.
- **Action Plan**: ordered implementation or execution steps.
- **Artifacts**: files, schemas, APIs, templates, diagrams, or checklists as applicable.
- **Validation**: tests, review checks, risk controls, or acceptance criteria.
- **Next Steps**: follow-up actions or missing inputs.

## Reference Index

- Read `references/source-map.md` for source traceability and source-to-skill mapping.
- Read `references/extraction-notes.md` for deeper design rationale, trade-offs, and edge cases.
- Read `references/workflow-checklist.md` for operational steps and validation checks.

## Validation Prompt

Test this skill with: "..."
```

## `agents/openai.yaml`

```yaml
display_name: Skill Display Name
short_description: One sentence describing the reusable capability.
default_prompt: Use the skill-name skill to ...
```

## `references/source-map.md`

```markdown
# Source Map

## Sources

| ID | Title | URL/File | Author/Org | Date | Notes |
| --- | --- | --- | --- | --- | --- |

## Source To Skill Mapping

| Source ID | Key Idea | Distilled Rule | Skill Location |
| --- | --- | --- | --- |

## Ambiguities Or Conflicts

- 

## Copyright And Quotation Notes

- Source content is paraphrased unless short quotation is necessary.
- Long examples are transformed into reusable patterns.
```
