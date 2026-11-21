# Chile Scam Mutator

## Lane

AI-fraud defence for Chile.

## Idea

A red-team and defense harness that generates culturally realistic Chilean scam variants from one seed message, then measures whether an existing detector still recognizes the fraud after wording, channel, urgency, and relationship cues change.

This is not a generic scam classifier. The product is the adaptive evaluation loop:

```text
Seed scam → Chilean mutation engine → detector → failure analysis → safer rule
```

## Why this is different

Generic spam and fraud filters already exist. The gap is evaluating them against rapidly rewritten, locally plausible scams: fake bank support, fake government benefits, family impersonation, delivery problems, and WhatsApp voice-note context.

## 12-hour demo

1. Start with one benign message and one fictional scam template.
2. Generate 30 safe synthetic variants in Chilean Spanish.
3. Run a baseline detector.
4. Show missed variants and the reason for failure.
5. Add a narrow defense rule and rerun the frozen set.

## Metric

- Detection recall before and after the defense
- False-positive rate on benign messages
- Mutation coverage by scam family
- Time to discover a blind spot

Target: improve recall from roughly 20% to at least 80% on one defined mutation family without collapsing benign precision. The actual numbers must be measured.

## Hard critique

- SafeLine and other anti-scam products make a generic detector unoriginal.
- Synthetic scams can exaggerate the problem and do not prove real-world protection.
- WhatsApp integration is unnecessary and risky for the hackathon.
- Keep all messages fictional; never target real people or financial accounts.
- It may be judged as cybersecurity rather than AI safety unless the adaptive AI red-team loop is central.

## Judgment

- Value: 8.5/10
- 12-hour feasibility: 9/10
- Innovation: 8/10
- Go/no-go: build only with a clear baseline detector and a pre-declared mutation family.
