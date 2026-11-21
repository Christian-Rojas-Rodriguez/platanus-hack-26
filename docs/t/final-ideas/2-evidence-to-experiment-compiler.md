# 2. Evidence-to-Experiment Compiler

## Final form

Evidence-to-Experiment Compiler converts a public AI safety claim into a minimal, executable test specification and fails loudly when the claim is too underspecified to reproduce.

It is a technical extension of Safety Evidence Auditor, not a separate document-parsing dashboard.

## Example

Input claim:

> “Our model resists indirect prompt injection in tool-use settings.”

Compiler output:

```text
Model version: specified
Attack definition: missing
Tool permissions: missing
Success criterion: ambiguous
Baseline: missing
Dataset: unavailable
Reproduction status: BLOCKED
```

## Product output

```yaml
claim: "..."
scope: "..."
required_inputs:
  model: "..."
  version: "..."
  prompts: "missing"
  dataset: "missing"
  evaluator: "missing"
metrics:
  primary: "missing"
  baseline: "missing"
reproduction_status: blocked
decision_impact: high
```

The system then generates a small synthetic substitute test where possible. It never presents an LLM-generated confidence score as proof.

## Why it fits AI Safety

Safety claims affect deployment and policy decisions. If external researchers cannot reproduce or inspect the evidence, safety reporting becomes difficult to trust.

This fits governance and verification failure, but it does not directly defend a model. The product value is preventing unsupported claims from being treated as evidence.

## 12-hour scope

- Choose three public safety claims
- Extract the claim and required evidence fields
- Compile each into a reproduction packet
- Implement one deterministic synthetic replay
- Have two people independently classify missing evidence

## Go/no-go gate

Keep the project only if:

1. At least two claims are missing reproduction-critical information.
2. One claim can be replayed with a safe synthetic substitute.
3. An independent reviewer changes a trust or prioritization decision after seeing the report.
4. Two reviewers agree on the missing-evidence classification at least 80% of the time.

Reject it if it only extracts text correctly or produces a checklist that changes no decision.

## Hard limitations

- It cannot prove a safety claim false.
- It cannot reproduce proprietary models or private datasets.
- It must not convert incomplete evidence into a fake numerical confidence score.
- Its demo can become abstract unless the missing evidence visibly blocks a decision.

## Judgment

- AI Safety fit: 7/10
- Real value: 7/10
- Technical novelty: 6/10 after adding executable compilation
- 12-hour feasibility: 8/10
- Presentation wow: 5/10

This is a structural backup only. It should be merged conceptually into Safety Evidence Auditor if that idea remains active.
