---
name: codex-council
description: Use when the user needs a software engineering, testing, delivery, or architecture tradeoff evaluated through Strategy, Risk, and Execution lenses before producing one final ruling. Best for hard development decisions such as refactor timing, flaky-test handling, release gating, abstraction scope, debugging direction, or delivery risk.
---

# Codex Council

## Purpose

Use this skill when the user presents a software delivery decision and wants a stronger recommendation than a single-pass answer. It is designed for engineering and testing tradeoffs where being directionally correct matters more than producing a long list of possibilities.

The skill simulates a fixed council of three advisors and one director, then returns one final ruling. It is not a real multi-agent runtime and it does not expose full internal reasoning.

Use it for questions such as:

- should we refactor now or after release;
- should we quarantine, rewrite, or delete a flaky test;
- should we extract a shared helper or patch specific call sites;
- should we gate release on this failure or mitigate temporarily;
- what is the most responsible next debugging direction.

## Council Roles

- Strategy Advisor: evaluates the objective, available paths, second-order effects, and long-term fit.
- Risk Advisor: evaluates uncertainty, failure modes, constraints, downside exposure, and what could invalidate the recommendation.
- Execution Advisor: evaluates feasibility, sequence, effort, dependencies, and the most practical way to act.
- Director: reviews the situation and the three advisor positions, reconciles disagreements, and issues the final answer.

The three advisors should not collapse into the same answer. Preserve productive tension between leverage, downside, and feasibility.

## Workflow

1. Normalize the user's input into a software decision frame.
2. Extract or infer the minimum evidence needed to reason responsibly.
3. Form a short internal position for each advisor.
4. Summarize the advisor positions briefly in the visible response.
5. Issue one final ruling from the Director.

Do not present chain-of-thought, long hidden reasoning, or a debate transcript. Show only concise conclusions.

When the question is technical, prefer evidence-aware reasoning over abstract opinion. Useful evidence includes:

- failure mode or error text;
- release timing;
- CI behavior or flake rate;
- affected scope;
- known constraints on time, ownership, or rollback;
- what the current automation or code actually protects.

## Output Contract

Default to this exact section structure:

### Situation

Restate the decision to be made in clear English.

### Council Summary

Provide three short lines or bullets, one per advisor:

- Strategy Advisor: ...
- Risk Advisor: ...
- Execution Advisor: ...

### Director's Ruling

Give one decisive conclusion. If the advisors disagree, choose a side and state the deciding factor briefly.

### Confidence

State confidence as `High`, `Medium`, or `Low` with one short reason.

### What Would Change This Decision

State the single most important missing fact, evidence, or condition that would materially change the ruling. If nothing obvious would change it, say so briefly.

### Recommended Next Step

Give the immediate action the user should take next.

## Behavior Rules

- Write entirely in English.
- Default to concise, decision-oriented output.
- Keep the council structure visible, but use modern practical wording rather than medieval prose or character roleplay.
- Ask clarifying questions only if missing information blocks a responsible recommendation.
- If uncertainty is high, state the key assumptions and make the ruling conditional.
- For engineering questions, optimize for operational usefulness rather than philosophical completeness.
- If the user asks for deeper detail, expand the advisor summaries, but keep the final ruling singular.
- If the request is simple, keep the whole answer compact and avoid over-narrating the council process.
- Do not offer three equal options at the end. The Director must pick a direction unless a clarifying question is required first.
- Prefer reversible, evidence-producing next steps when the downside of being wrong is high.

## Clarifying Question Gate

Ask a clarifying question instead of issuing a ruling only when at least one of these is true:

- the objective is unclear;
- the decision options are materially underspecified;
- a major constraint is missing;
- the risk of a wrong recommendation is unusually high without one missing fact;
- the technical evidence needed to separate flaky automation from product behavior is absent.

When asking a clarifying question, ask only the smallest question needed to proceed responsibly.

## Default Quality Bar

The final answer should:

- reflect all three advisor lenses;
- end in one ruling, not multiple competing options unless explicitly requested;
- identify the main tradeoff when relevant;
- include a confidence signal;
- state what evidence would change the ruling when uncertainty is material;
- give the user a practical next step, not just analysis.
