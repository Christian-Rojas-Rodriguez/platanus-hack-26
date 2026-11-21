# Safety Evidence Auditor

## Lane

Lab transparency trackers.

## Idea

An auditor that converts a model card, safety report, or lab commitment into machine-checkable claims and flags which claims lack reproducible evidence.

Example claim: “The model resists prompt injection in tool-use settings.” The auditor checks the model version, attack set, tool-call and side-effect measurements, dataset availability, reproducibility, and disclosed limitations.

## Why this is different

This is not another model benchmark or safety dashboard. It audits the **evidence behind safety claims** and outputs a claim/evidence/uncertainty graph plus a reproducibility score.

## 12-hour demo

Extract 10 claims from two public safety reports, map the evidence each cites, and score them with a fixed rubric. Show how one impressive claim loses confidence because the dataset, model version, or failure cases are missing.

## Metric

- Claim extraction precision
- Evidence-link coverage
- Reproducibility score agreement with human reviewers
- Unsupported or ambiguous claims found

## Hard critique

- Governance infrastructure can feel abstract in a two-minute demo.
- A language model must not decide truth alone; the rubric and evidence fields must be explicit.
- It measures inspectability, not model safety.
- The buyer is unclear: researchers, regulators, procurement teams, and journalists need different outputs.

## Judgment

- Value: 8/10
- 12-hour feasibility: 9/10
- Innovation: 8.5/10
- Go/no-go: build only if the score changes a real decision about trusting a safety claim.
