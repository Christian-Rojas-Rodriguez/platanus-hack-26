# Final AI Safety ideas

## Final result

After restarting from the five open lanes and rejecting the repository’s earlier recommendations, these are the three strongest new directions:

1. **[Safety Evidence Auditor](./safety-evidence-auditor.md)** — strongest structural/transparency idea.
2. **[Chile Scam Mutator](./chile-scam-mutator.md)** — strongest product/demo idea.
3. **[LatAm Safety Gate](./latam-safety-gate.md)** — safest evaluation backup.

None is automatically a winner. Each must pass its go/no-go experiment before coding continues.

## Preview of the three ideas

> Labs publish safety claims, but readers cannot quickly tell which claims are reproducible. Safety Evidence Auditor maps claims to evidence and exposes missing support.

> Chilean scams are rewritten faster than static filters are updated. Chile Scam Mutator generates safe, local variants and measures whether a detector survives them.

> A model can behave safely in neutral English and inconsistently in local high-stakes contexts. LatAm Safety Gate turns that risk into a release test.

### Decision rule

Keep only the idea that produces a meaningful result on its first 30 labelled cases. Do not build a dashboard before the evidence exists.

## Hard rejection of previous ideas

| Idea | Verdict | Reason |
|---|---|---|
| Cheat Detector + Canaries | Reject as copied direction | Reward-hacking benchmarks and detectors now cover this lane directly |
| ScopeProof / mandate and receipt | Reject | Authorization gateways and signed receipts are established |
| ConsequenceGuard / Impact Simulator | Reject | Existing observability, approval, and shadow-execution patterns are too similar |
| Generic harness, MCP scanner, or runtime firewall | Reject | Already present in the repo, the tour, and current products |
| MemoryLineage | Reject | Active research and prior tour projects already cover the core mechanism |
| Generic observability/eval platform | Reject | Existing platforms and open-source eval harnesses cover the category |
| Scheming radar | Reject | Existing incident observatories; weak live demo |
| Anti-vishing | Reject | High implementation risk and prior hackathon precedent |

## Why these three are better

| Criterion | Judgment |
|---|---|
| Criterion | Auditor | Scam Mutator | LatAm Gate |
|---|---:|---:|---:|
| Real value | 8 | 8.5 | 8 |
| 12-hour feasibility | 9 | 9 | 9.5 |
| Differentiation | 8.5 | 8 | 8 |
| Main risk | Abstract demo | Synthetic fraud | Null result |

## Build rule

Do not build a dashboard first. Build the labelled honest and cheating runs first. If the detector cannot distinguish them with deterministic evidence, kill the idea before adding UI.

## Repository basis

This decision follows:

- `docs/ai-safety-track-brief.md`
- `docs/feedback-mentor-2026-11-20.md`
- `research/notas/jaime-aza/mapa-ideas-equipo.md`
- `research/notas/jaime-aza/propuestas.md`
- `research/notas/m-propuesta_de_arquitectura_harness_ai_security.md`

This README is the presentation-facing source of truth. Older recommendation files were removed from this folder to avoid presenting copied or rejected ideas as finalists.

## Two additional experimental ideas

- [1. Eval Mirage](./1-eval-mirage.md) — conditional research backup; build only if the paired experiment reveals a replicated safety degradation.
- [2. Evidence-to-Experiment Compiler](./2-evidence-to-experiment-compiler.md) — structural backup; merge with Safety Evidence Auditor rather than presenting it as a separate platform.

These are not promoted above the main project. Both have explicit go/no-go gates and should be killed if the first experiment produces no meaningful result.
