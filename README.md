# Codex Council

Three advisors. One ruling. Built for engineering decisions.

Codex Council is a prompt-only Codex skill for software engineering decision support. It takes a freeform development, testing, release, or architecture situation, analyzes it through three fixed advisor roles, and returns one final ruling from a director.

Positioning: this is not a generic advice council. It is a disciplined decision engine for software delivery tradeoffs.

## What This Repository Contains

- `SKILL.md`: the installable Codex skill
- `agents/openai.yaml`: display metadata and default prompt
- `EXAMPLES.md`: sample prompts and expected outputs
- `RELEASE_CHECKLIST.md`: a small quality gate for future updates

## Best For

- release-time refactor decisions
- flaky test keep, quarantine, rewrite, or delete calls
- shared abstraction versus local patch tradeoffs
- release-gating and mitigation decisions
- debugging direction when the failure signal is noisy or incomplete

## Quick Pitch

Most council-style skills stop at "here are several viewpoints." Codex Council is designed to finish the job:

- it is opinionated toward software delivery and test automation decisions
- it forces Strategy, Risk, and Execution to pull in meaningfully different directions
- it produces one ruling, a confidence signal, and the key fact that would change the verdict
- it prefers evidence-aware next steps over generic brainstorming

## How It Differs From Generic Council Skills

- It is optimized for engineering and test-delivery tradeoffs rather than broad life or business advice.
- It treats evidence as a first-class input for technical decisions.
- It requires the Director to choose a direction instead of ending with several equivalent options.
- It highlights confidence and the single fact that would change the ruling, which makes the output more actionable.
- It stays concise and operational instead of turning the council metaphor into roleplay.

## What It Does

- Accepts a natural-language situation with no required template
- Focuses on engineering and test decisions rather than generic life or business advice
- Applies three fixed lenses:
  - Strategy Advisor
  - Risk Advisor
  - Execution Advisor
- Produces one final decision from the Director
- Adds a confidence signal and the key fact that would change the decision
- Keeps responses concise and entirely in English

## Recommended Use Cases

- `Should we refactor now or after release?`
- `Should this flaky test stay in release gating?`
- `Should we extract a shared helper or keep fixing call sites locally?`
- `What is the most responsible next debugging step with the current evidence?`
- `Should we mitigate temporarily or block the release?`

## Install

This repository is itself the skill directory. The installable path is the repo root because it contains `SKILL.md`.

### Manual Install

Copy this repository into your Codex skills directory as:

```text
~/.codex/skills/codex-council
```

Then restart Codex so it reloads installed skills.

### Install From GitHub

If you use Codex's GitHub skill installer, point it at the repository root path:

```text
--path .
```

The selected directory only needs to contain `SKILL.md`, which this repo already does.

## Suggested Repository Description

If you want a short GitHub repo description, use:

`A Codex skill for software engineering tradeoffs that weighs Strategy, Risk, and Execution before issuing one final ruling.`

## How To Invoke It

Ask Codex to use the `codex-council` skill when you want a situation evaluated from multiple fixed perspectives before getting one final recommendation.

Example prompts:

- `Use codex-council to decide whether we should quarantine this flaky payment E2E test before release.`
- `Use codex-council to evaluate whether I should refactor this Playwright helper now or postpone it until after release.`
- `Use codex-council to analyze whether we should extract a shared service or keep patching individual specs.`
- `Use codex-council to recommend the next debugging direction for this recurring CI failure.`

## Council Roles

- Strategy Advisor: evaluates goals, options, and longer-term implications
- Risk Advisor: evaluates uncertainty, constraints, and downside risk
- Execution Advisor: evaluates feasibility, effort, and sequencing
- Director: reconciles the three views and issues the final ruling

## Output Shape

The default response format is:

1. `Situation`
2. `Council Summary`
3. `Director's Ruling`
4. `Confidence`
5. `What Would Change This Decision`
6. `Recommended Next Step`

The council summary is intentionally brief. The skill does not expose a full internal debate transcript. The goal is an actionable engineering ruling, not a theatrical deliberation.

## Why It Differs

- Built for software delivery tradeoffs, not general-purpose advice
- Forces productive disagreement across Strategy, Risk, and Execution rather than three similar opinions
- Uses evidence-aware reasoning for technical questions
- Produces a ruling, a confidence level, and the key fact that would change the verdict
- Stays concise and operational instead of roleplaying a theatrical debate

## v1 Boundaries

- Prompt-only skill, not a real multi-agent runtime
- Fixed advisor roster
- Freeform input
- No configuration layer or external orchestration API

## Examples

See [EXAMPLES.md](C:/Users/martin.caceres/codexcouncil/codex-council-wisdom-from-many/EXAMPLES.md) for sample prompts and expected responses covering:

- a clear decision case
- an ambiguous case that triggers a clarifying question
- a tradeoff case with advisor disagreement resolved by the Director
- a high-risk case with an assumption-sensitive ruling

## Maintenance

Use [RELEASE_CHECKLIST.md](C:/Users/martin.caceres/codexcouncil/codex-council-wisdom-from-many/RELEASE_CHECKLIST.md) before publishing changes for other Codex users.
