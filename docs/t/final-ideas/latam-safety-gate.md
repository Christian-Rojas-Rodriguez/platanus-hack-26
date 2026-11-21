# LatAm Safety Gate

## Lane

Spanish/LatAm safety evaluations.

## Idea

A release gate for models used in high-stakes Latin American services. It checks whether safety behavior remains stable when the same scenario changes across country, institution, dialect, code-switching, and social context.

```text
Same risk → Chilean bank support → Mexican bank support → public-service context
         → neutral Spanish → local slang → mixed Spanish/English
```

## Why this is different

Large multilingual benchmarks already exist, including [XL-SafetyBench](https://www.microsoft.com/en-us/research/publication/xl-safetybench-a-country-grounded-cross-cultural-benchmark-for-llm-safety-and-cultural-sensitivity/) and [LatAm-RT](https://aclanthology.org/2026.pandora-1.11/). Therefore this must not be pitched as “a Spanish benchmark.”

The narrower contribution is a **release gate for high-stakes regional workflows**, using paired tests that keep the underlying risk constant while changing local context.

## 12-hour demo

1. Define 30 paired tests for a Chilean public-service or banking assistant.
2. Change dialect, country context, and code-switching while holding the risk constant.
3. Run a baseline model or guardrail.
4. Flag inconsistent decisions.

## Metric

- Pairwise safety consistency
- Unsafe completion rate
- False refusal rate
- Regression count between model versions
- Local-context coverage

Target: expose at least one reproducible safety regression that an English-only suite misses. If no regression appears, report a null result and reject the product claim.

## Hard critique

- This is not blue ocean at the benchmark level.
- Cultural adaptation can become subjective or tokenistic.
- Thirty tests cannot represent Latin America.
- The release-gate framing is more useful than a leaderboard, but the buyer is mostly research and governance teams.
- Prompts must be pre-registered before results are seen.

## Judgment

- Value: 8/10
- 12-hour feasibility: 9.5/10
- Innovation: 8/10
- Go/no-go: safest research backup, not the main product.
