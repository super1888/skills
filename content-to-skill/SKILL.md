---
name: content-to-skill
description: Use when the user provides technical blogs, articles, documentation links, pasted long-form content, tutorials, design notes, implementation guides, or source materials and asks to generate, distill, create, update, or refine a Codex Skill from them; produces a complete usable skill with precise trigger metadata, concise SKILL.md workflow, references-based source traceability, fixed output structure, and quality checks.
---

# Content to Skill

Use this skill to convert user-provided technical articles, blogs, documents, links, tutorials, or pasted source content into a complete, directly usable Codex Skill. The goal is not summarization: distill the source into triggerable agent capability with stable workflow, traceable references, and low context cost.

## Core Workflow

1. Intake sources: identify all links, pasted text, files, article titles, authors, dates, and user constraints.
2. Triage source sufficiency: decide whether to browse, read local files, proceed from pasted content, or ask for missing material.
3. Extract the technical core: find the source problem, design logic, architecture ideas, execution method, constraints, risks, and reusable decision rules.
4. Define skill positioning: name, trigger scope, target tasks, non-goals, and expected user intent.
5. Split content by disclosure level: keep `SKILL.md` concise; move source trace, long notes, examples, mappings, and checklists into `references/`.
6. Generate a complete skill folder with `SKILL.md`, optional `agents/openai.yaml`, and relevant `references/*.md` files.
7. Validate against trigger precision, stable output format, source traceability, context efficiency, maintainability, and direct usability.

## Required Generated Skill Modules

Every generated skill must include these modules in `SKILL.md`:

- **Skill Positioning**: applicable scenarios, core purpose, task scope, and non-goals.
- **Underlying Thinking**: distilled design logic, architectural ideas, problem-solving principles, and source-derived heuristics.
- **Practical Method**: executable steps, operation points, conventions, and implementation rules.
- **Trigger Conditions**: automatic matching signals, task features, domain keywords, and exclusion signals.
- **Output Format**: fixed structured template the skill should produce when used.
- **Reference Index**: links to `references/` files containing source traceability and expanded knowledge.

## Source Handling Rules

- Preserve the original technical kernel, not the original wording.
- Attribute source ideas in `references/source-map.md` with link/title and concise paraphrased notes.
- Do not paste large copyrighted passages from articles or blogs; summarize and transform instead.
- If a URL is provided and browsing is available, open the source before distillation; if not available, ask for pasted content.
- If sources conflict, document the conflict and choose the rule that best fits the target skill scope.
- If the input lacks enough substance to build a usable skill, ask for missing source content, target audience, or intended task examples.

## Source Triage Rules

- **Proceed** when the source contains a clear task, method, constraints, and examples or enough implementation detail.
- **Browse or read** when the user provides links, local files, or named documents that are not already in context.
- **Ask first** when the source is only a title, vague topic, marketing summary, or missing the target skill audience.
- **Flag uncertainty** when the source is opinion-heavy, outdated, vendor-specific, or conflicts with current project conventions.
- **Record provenance** for every source-derived rule that materially shapes the generated skill.

## Reference Files To Create

Create only the reference files that the generated skill actually needs:

- `references/source-map.md`: original links, titles, key ideas, design rationale, and source-to-skill mapping.
- `references/extraction-notes.md`: deeper technical decomposition, architecture notes, edge cases, and trade-offs.
- `references/workflow-checklist.md`: operational checklist, examples, validation rules, or reusable templates.
- `references/examples.md`: representative prompts and expected output shape when examples materially improve reuse.

Read this skill's `references/generated-skill-template.md` when the user asks for a full generated skill or when output consistency matters.
Read this skill's `references/extraction-framework.md` when the source is long, dense, or mixes concepts with implementation details.
Read this skill's `references/source-map-template.md` when creating source traceability files for generated skills.
Read this skill's `references/review-improvement-notes.md` when reviewing or improving this skill's design approach.
Read this skill's `references/quality-checklist.md` before final delivery.

## Generated Skill Structure

```text
skill-name/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── source-map.md
    ├── extraction-notes.md
    └── workflow-checklist.md
```

## `SKILL.md` Quality Rules

- Keep the body compact and procedural; avoid raw article dumps.
- Make `description` broad enough to auto-trigger but specific enough to avoid unrelated tasks; include source types, user intents, output artifacts, and exclusion signals when needed.
- Write `description` as the main routing contract, not as a marketing summary.
- Use stable section names from Required Generated Skill Modules.
- Prefer imperative workflow steps and checklists over explanatory essays.
- Include exact guidance for when to read each reference file.
- State red flags and exclusion cases when misuse is likely.
- Include 1-3 realistic trigger examples in `references/examples.md` when auto-trigger precision is hard to judge.

## Generated Skill Design Rules

- Keep one skill focused on one reusable capability; split broad topics into separate skills or reference variants.
- Convert examples into reusable patterns, but keep representative prompts in references when they teach correct use.
- Add guardrails for unsafe, stale, or ambiguous source material.
- Include a minimal validation prompt so the user can test whether the skill triggers and outputs the expected structure.
- Prefer stable names and file paths so future updates can add references without renaming the skill.

## Fixed Delivery Format

When generating a skill, respond with:

- **Skill Summary**: name, purpose, trigger scope, and generated files.
- **Source Distillation**: core ideas extracted from the source and how they map to the skill.
- **Files Created Or Updated**: paths and one-line role for each file.
- **Quality Check**: trigger precision, output stability, reference traceability, context efficiency, maintainability.
- **Next Steps**: installation, testing prompt, or missing source questions if generation is blocked.

## Quality Gate

Before finalizing, verify:

- Trigger precision: related user tasks can match without manually naming the skill.
- Output stability: the skill defines a repeatable output template.
- Source traceability: source-derived knowledge is discoverable in `references/`.
- Context efficiency: `SKILL.md` contains core logic only.
- Maintainability: new cases can be added to references without changing the main workflow.
- Practicality: the generated skill can be copied into a skills directory and used immediately.
- Testability: the final answer includes one realistic prompt for manually testing the generated skill.
- Safety: copyrighted text is paraphrased, source uncertainty is marked, and source-specific limitations are documented.
