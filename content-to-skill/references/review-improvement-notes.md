# Review Improvement Notes

This reference captures reusable ideas for improving `content-to-skill` itself and for reviewing generated skills.

## External Design Ideas To Reuse

- **Progressive disclosure**: keep the always-loaded skill body small; move detailed examples, source maps, and checklists into references loaded only when needed.
- **Routing-first metadata**: treat `name` and `description` as the trigger contract. The description should name source types, user intents, generated artifacts, and important boundaries.
- **Small specialized capabilities**: prefer one focused skill per recurring capability instead of broad catch-all skills.
- **Executable workflows**: skills should tell the agent what to do in order, not merely explain a topic.
- **Examples as tests**: include representative prompts and expected response shape when they help validate trigger precision or output stability.
- **Guardrails and provenance**: mark source uncertainty, avoid long copied passages, and keep source-to-rule mapping in references.

## Review Questions

Use these questions when auditing this skill or a generated skill:

1. Would the skill trigger from a natural user request without naming the skill?
2. Is the description too broad, causing unrelated tasks to match?
3. Does `SKILL.md` define a repeatable workflow and output shape?
4. Are long source details, examples, and mappings outside `SKILL.md`?
5. Can a future maintainer add a new source, example, or checklist without rewriting the main workflow?
6. Is there a simple validation prompt for testing the generated skill?

## Improvement Backlog

- Add a generator script only if this skill starts producing many repetitive file skeletons.
- Add domain-specific reference variants only when multiple source types require different extraction logic.
- Keep this skill language-neutral unless a repository standard requires Chinese or English output.

## Sources Consulted

- OpenAI Academy Skills: https://openai.com/academy/skills/
- OpenAI prompt engineering guide: https://platform.openai.com/docs/guides/prompt-engineering
- Anthropic Claude Skills overview: https://docs.anthropic.com/en/docs/claude-code/skills
