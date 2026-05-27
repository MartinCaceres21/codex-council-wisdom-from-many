# Codex Council Examples

These examples show the expected visible behavior of the `codex-council` skill in v1. They are intentionally concise and use the stable engineering-focused output contract.

## Example 1: Clear Development Decision

### User Prompt

`Use codex-council to evaluate whether I should refactor this Playwright helper now or postpone it until after next week's release. The helper is messy, but the tests are currently stable in CI and the release branch is already in QA.`

### Expected Response Shape

## Situation

You need to decide whether to refactor a messy but currently stable Playwright helper before a release branch that is already in QA.

## Council Summary

- Strategy Advisor: Preserve release focus unless the refactor is required to unblock a near-term delivery goal.
- Risk Advisor: Refactoring now creates avoidable test regression risk late in the release cycle with little recovery time.
- Execution Advisor: Postpone the refactor, document the cleanup scope, and schedule it immediately after release.

## Director's Ruling

Postpone the refactor until after the release. The deciding factor is timing: the helper is currently stable in CI, while the branch is already in QA and late structural changes add more delivery risk than immediate value.

## Confidence

High. The release timing and current CI stability make the downside of refactoring now clear.

## What Would Change This Decision

Evidence that the helper is actively blocking release work or causing current production-risk defects.

## Recommended Next Step

Create a post-release refactor task with scope, owner, and test acceptance criteria before this release ships.

## Example 2: Ambiguous Testing Case That Requires Clarification

### User Prompt

`Use codex-council to tell me whether I should keep this failing test or delete it.`

### Expected Response Shape

What is the test supposed to protect, and why is it failing: product drift, flaky automation, outdated assertions, or a real regression?

## Example 3: Tradeoff Case With Advisor Disagreement

### User Prompt

`Use codex-council to analyze whether our team should build a shared Playwright service for this workflow or keep patching individual specs. We have repeated locator bugs across four specs, one engineer available part-time for six weeks, and a release in progress.`

### Expected Response Shape

## Situation

You need to decide whether to invest limited engineering time in a shared Playwright service or continue patching repeated issues directly in individual specs during an active release cycle.

## Council Summary

- Strategy Advisor: A shared service could reduce duplication and stabilize the workflow across multiple specs.
- Risk Advisor: A broad abstraction introduced during release work may spread instability if the service contract is still unclear.
- Execution Advisor: Do not attempt a large refactor now; isolate the repeated interaction behind the narrowest shared helper that solves today's recurring failures.

## Director's Ruling

Do not build a broad shared service right now. The deciding factor is execution capacity during release work: the better path is to extract only the repeated unstable interaction into a narrow helper, prove it across the affected specs, and expand later if the pattern holds.

## Confidence

Medium. The direction is sound, but the right abstraction boundary still depends on how similar the four failing interactions actually are.

## What Would Change This Decision

Evidence that the four specs already share a stable interaction contract with the same failure mode and selectors.

## Recommended Next Step

Identify the single repeated interaction causing most failures and extract that slice into one shared helper, then validate it against the affected specs before widening the abstraction.

## Example 4: High-Risk Conditional Recommendation

### User Prompt

`Use codex-council to decide whether we should disable a flaky end-to-end test before release. It fails about 8 percent of the time in CI, covers a payment flow, and we do not yet know whether the failures are environmental or product defects.`

### Expected Response Shape

## Situation

You need to decide whether to disable a flaky end-to-end test before release even though it covers a payment flow and the source of failure is still unclear.

## Council Summary

- Strategy Advisor: Keep coverage on critical payment behavior if possible, because removing it reduces confidence in a high-impact workflow.
- Risk Advisor: Leaving a flaky critical test enabled can mask true signal and disrupt release decisions, but disabling it blindly may remove the only automated guardrail on payments.
- Execution Advisor: Do not make a permanent keep-or-delete decision until you classify the failures and define a temporary mitigation path.

## Director's Ruling

Conditionally disable the test only if you add a temporary replacement control and open an immediate investigation. The deciding factor is operational clarity: an 8 percent flaky failure rate is too noisy for release gating, but removing payment coverage without compensating controls is too risky.

## Confidence

Medium. The flake rate justifies action, but confidence is limited because the current failures have not yet been classified as environmental or product-related.

## What Would Change This Decision

Proof that the failures are genuine product regressions rather than automation or environment noise.

## Recommended Next Step

Quarantine the test from release gating, add a targeted payment smoke check or manual verification step, and assign an owner to classify the flake before the next release checkpoint.
