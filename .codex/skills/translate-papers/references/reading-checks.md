# Academic Reading Checks

Use this checklist when translating dense academic passages or when the user is worried about meaning drift.

## Preserve Claim Strength

- "may", "might", "can": possible, not guaranteed.
- "we observe", "we find": empirical observation, not universal proof.
- "suggests", "indicates": evidence toward a claim, not definitive causality.
- "up to": best observed case, not average.
- "on average": aggregate result; do not imply every case.

## Preserve Scope

Track conditions introduced by:

- under / when / if / given / assuming
- in our setup / in our experiments / in this workload
- for short prompts / long outputs / high load / memory-bound cases

Do not remove these conditions in Chinese translation.

## Preserve Comparison Targets

For every "better", "faster", "lower", "higher", or "more efficient", identify:

- what is being compared
- under what metric
- in which environment
- whether the result is average, tail, peak, or case-specific

## Technical Term Policy

Keep the English term when the Chinese translation is not standard or may hide the concept. Recommended pattern:

`continuous batching（连续批处理）`

After first definition, use the term consistently.

## Project-Implication Discipline

Separate paper facts from project inference:

- Paper fact: "The authors report..."
- Inference: "For your project, this suggests..."

Never imply the authors evaluated the user's project unless the paper explicitly did so.
