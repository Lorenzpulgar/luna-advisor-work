# Luna Advisor Work

A cost-aware ChatGPT Work orchestrator derived conceptually from the MIT-licensed Sol Advisor architecture by Daniel McAteer.

## Goal

Use GPT-5.6 Luna as the economical control plane for routing, context management, synthesis, and routine verification, while escalating intelligence only when task shape requires it:

- **Luna / Light** — mechanical, deterministic, repetitive work.
- **Luna / Medium** — routine bounded execution.
- **Terra / Medium** — normal non-trivial implementation and integration.
- **Terra / High** — difficult execution after evidence of added complexity.
- **Sol / High** — architecture, ambiguous systems reasoning, deep root-cause analysis.
- **Fresh Sol / High** — independent review for critical/high-risk outcomes.

## Core policy

1. Classify the task before substantial work.
2. Use the cheapest lane that preserves correctness.
3. Escalate mandatory high-impact categories to Sol even if Luna feels confident.
4. Prefer Sol for decisions and Terra for implementation once architecture is settled.
5. Parallelize independent read-heavy work.
6. Serialize shared-state writes and prefer exactly one writer.
7. Treat all worker reports as claims until the parent verifies observable state.
8. Never claim model pins, reasoning effort, or sandbox isolation that Work did not expose.

## Recommended complex path

```text
Luna parent
  -> read scouts in parallel (optional)
  -> Sol / High decision
  -> Terra / Medium|High implementation
  -> Luna verification
  -> fresh Sol review if critical
```

See `skills/orchestration/SKILL.md` and `skills/orchestration/references/` for the complete contracts.

## Attribution

This project is structurally inspired by [DannyMac180/sol-advisor](https://github.com/DannyMac180/sol-advisor), distributed under the MIT License. This Work-native adaptation is maintained separately.
