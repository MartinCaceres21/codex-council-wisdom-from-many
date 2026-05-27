# Codex Council Release Checklist

Use this checklist before publishing or sharing updates to other Codex users.

## Skill Contract

- `SKILL.md` still describes an engineering-focused decision council.
- The output contract still includes:
  - `Situation`
  - `Council Summary`
  - `Director's Ruling`
  - `Confidence`
  - `What Would Change This Decision`
  - `Recommended Next Step`
- The Director still produces one ruling rather than multiple equal options.
- The skill still defaults to English-only output.

## Package Shape

- The repo root still contains `SKILL.md`.
- `agents/openai.yaml` still matches the skill positioning and default prompt.
- The install guidance in `README.md` still matches the actual repo layout.

## Examples

- `EXAMPLES.md` still reflects the current output contract.
- The examples still focus on development, testing, release, or architecture decisions.
- At least one example covers a clarifying-question case.
- At least one example covers a conditional ruling under uncertainty.

## Validation

- Run:

```text
python C:\Users\martin.caceres\.codex\skills\.system\skill-creator\scripts\quick_validate.py <repo-root>
```

- Review the README top section and confirm the differentiation is still obvious to a first-time visitor.
