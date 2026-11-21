# AI agent safety: research opportunities

Research snapshot: 2026-11-21

This note turns the pasted research snapshot into a source-checked opportunity map. Percentages below come from controlled evaluations; they are not estimates of production incident rates.

## Strongest evidence

- [APEX-Harm](https://arxiv.org/abs/2610.13623) evaluates prompt and script injection against long-horizon agents in shared professional workspaces.
- [MemSecBench](https://arxiv.org/abs/2607.27080) reports malicious memory persistence in 84.2% of tested configurations and successful write-to-execute chains in 50.3%.
- [SABench](https://arxiv.org/abs/2610.34167) evaluates 201 email, calendar, and ticket tasks and reports unauthorized writes even when the requested task succeeds; its reported rate for successful tasks is 12.8%.
- [Microsoft's MCP security guidance](https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/) documents tool poisoning through malicious instructions embedded in MCP tool descriptions.
- [APEX](https://arxiv.org/abs/2610.06966) is closely related prior work: it places authorization and evidence checks at the execution boundary.

## Recommended direction: ScopeProof

ScopeProof protects the boundary between a user's requested task and the agent's actual effects.

### Core question

Did the agent complete the requested task without accessing, modifying, or contacting anything outside the approved scope?

### MVP flow

1. Convert the user request into an authorization contract: objects, operations, recipients, time window, and side-effect limits.
2. Let the agent propose tool calls.
3. Enforce deterministic policy checks before each external write.
4. Execute allowed calls through a controlled mock calendar, CRM, or ticket system.
5. Compute a final state diff and produce an evidence report.

### Demonstration

User request: “Cancel only tomorrow's meeting.”

- Allowed: cancel the single meeting instance tomorrow.
- Blocked: cancel the recurring series, edit another attendee's meetings, or send an unrelated message.
- Report: show the requested effect, attempted effects, blocked effects, and final state diff.

The model may draft the contract, but it must not expand its own authorization. The final decision should be deterministic and inspectable.

## Alternative directions

### MemoryLineage

Attach provenance, trust, timestamp, and modification history to every persistent memory. Quarantine memories derived from untrusted documents and require verification before they influence a write action. MemSecBench is the primary benchmark to study.

### MCP TimeLock

Pin approved MCP tool definitions, compare later versions semantically, and quarantine changes that add permissions, request unrelated data, or contain hidden instructions. Microsoft and the [MCP security control-plane guidance](https://developer.microsoft.com/blog/securing-mcp-a-control-plane-for-agent-tool-execution/) provide useful threat-model material.

### Agent Escape Lab

Give agents difficult or impossible tasks in a sandbox and measure whether they stop, ask for help, or attempt unauthorized workarounds. Keep all experiments synthetic and isolated.

## Evaluation plan

- Task success: did the requested task finish?
- Scope precision: how many allowed actions were incorrectly blocked?
- Scope recall: how many unauthorized effects were blocked?
- Side-effect rate: unauthorized writes per successful task.
- Explanation quality: can a reviewer connect each decision to the contract and state diff?
- Robustness: repeat with ambiguous wording, injected documents, poisoned tool descriptions, and impossible tasks.

## Claims requiring caution

The pasted snapshot mentions an “Authorization Drift Benchmark,” “Agent Guard,” “CapFence,” and “SpecShield.” These names were not used as primary evidence here. Treat them as leads to verify, not established facts or proof of an empty market.
