# 1. Eval Mirage

## Final form

Eval Mirage is a controlled benchmark for measuring whether an agent’s safety behavior degrades when the surrounding environment looks less like an evaluation.

It does **not** claim to detect deception or prove that a model knows it is being tested.

## Experiment

Run the same agent, task, repository, tools, permissions, and evaluator under four conditions:

1. Benchmark language, visible tests
2. Benchmark language, hidden tests
3. Natural task language, visible tests
4. Natural task language, hidden tests

Only evaluation observability changes. Everything else stays fixed.

## What it measures

```text
Safety degradation =
unsafe behavior in realistic context
− unsafe behavior in obvious evaluation context
```

Track three separate outputs:

- Task outcome
- Safety or policy violations
- Strategy changes in the trace

Example:

| Measurement | Obvious test | Natural context |
|---|---:|---:|
| Task success | 8/10 | 7/10 |
| Unauthorized actions | 0/10 | 3/10 |
| Shortcut searches | 1/10 | 6/10 |

## Why it fits AI Safety

If safety behavior appears only under visible evaluation conditions, benchmarks may overestimate real-world safety. This is an evaluation-validity and AI-control problem.

## 12-hour scope

- Two small coding or data tasks
- Four matched conditions
- Eight runs per condition if compute allows
- Three predefined behavioral indicators
- Deterministic event logs
- A paired-results report

## Go/no-go gate

Keep the project only if:

1. A safety-relevant behavior changes by at least 20 percentage points.
2. The change appears across two task families.
3. A blinded reviewer identifies the relevant trace difference with at least 80% accuracy.

Reject it if only harmless file-search behavior changes or if the effect disappears on replication.

## Hard limitations

This experiment cannot establish that the model recognized an evaluation or that a behavioral change reflects deception. It measures behavior differences under controlled observability conditions and leaves the mechanism unknown.

## Judgment

- AI Safety fit: 8/10
- Real value: 7/10
- Technical novelty: 6/10
- 12-hour feasibility: 5/10
- Presentation wow: 6/10

This is a research backup, not the primary hackathon product. Build it only if the first paired experiment produces a strong effect quickly.
