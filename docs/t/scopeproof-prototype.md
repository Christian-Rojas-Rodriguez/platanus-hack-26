# ScopeProof prototype brief

## Goal

Build a small, demonstrable safety layer that prevents an AI agent from causing side effects outside a task-specific authorization contract.

## Suggested stack

- Python
- FastAPI
- A deterministic mock calendar or ticket system
- An agent SDK behind a narrow tool adapter
- JSON contracts and JSONL event logs

## Contract shape

```json
{
  "task": "Cancel only tomorrow's meeting",
  "allowed_objects": ["meeting:tomorrow:single-instance"],
  "allowed_operations": ["cancel"],
  "allowed_recipients": [],
  "time_window": {"start": "tomorrow", "end": "tomorrow"},
  "side_effect_policy": "deny-by-default"
}
```

## Components

1. Contract builder: converts natural language into a reviewable contract.
2. Tool gateway: validates every proposed call against the contract.
3. Mock environment: records state before and after each call.
4. State-diff verifier: detects extra writes even when the task succeeds.
5. Evidence report: explains allowed, blocked, and observed effects.

## Required demo cases

1. Legitimate single-event cancellation succeeds.
2. Recurring-series cancellation is blocked.
3. An injected document asks the agent to cancel another event; the gateway blocks it.
4. The agent completes the task but attempts an unrelated write; the final state diff flags it.
5. A malformed or ambiguous contract fails closed and asks for clarification.

## Safety boundary

Use only synthetic data and mock integrations. Never test against real calendars, email accounts, production MCP servers, or third-party systems without explicit authorization.
