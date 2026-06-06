# Fidelity Checklist for Chinese PDF Explanation

Use this checklist before finalizing translation or evaluation.

## Metadata

- Confirm title from the paper itself, arXiv page, DOI page, or publisher page.
- Confirm venue separately from arXiv. arXiv alone is a preprint source, not necessarily the formal publication venue.
- If publication status is unclear, say `arXiv preprint` or `Unknown formal venue`.

## Translation Fidelity

- Preserve conditions: under, when, if, assuming, in our setup, in this workload.
- Preserve uncertainty: may, might, can, could, suggests, indicates, likely.
- Preserve measurement type: average, median, P50, P95, P99, peak, worst case.
- Preserve comparison target: faster than what, lower than what, compared under which setup.
- Preserve scope: dataset, model size, hardware, benchmark, workload, and experiment configuration.

## Summary Discipline

- Summaries may simplify wording but must not broaden claims.
- Separate method claims from experiment results.
- Separate paper facts from project implications.
- Mark project implications as inference unless the paper directly studies the user's project.

## Evaluation

Consider:

- Is the problem important?
- Is the method clearly specified?
- Are baselines appropriate?
- Are metrics appropriate?
- Are limitations acknowledged?
- Is the evidence sufficient for the stated conclusion?
- What would the user need to reproduce or verify?
