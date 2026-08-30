# Luna Advisor Work

**A cost-efficient AI team for ChatGPT Work.**

Luna Advisor Work organizes work like a small AI team. The preferred architecture is: **Luna coordinates everyday work, Terra handles substantial implementation, and Sol enters for difficult decisions or critical review.** Exact model assignment is used only when the current Work runtime exposes and verifies those controls.

## Why it exists

Many tasks mix easy work with difficult work. Researching files, making routine edits, implementing a feature, and deciding a risky architecture do not require the same level of reasoning.

Luna Advisor Work is **efficiency-first**: it tries to use lighter reasoning for predictable work and stronger reasoning only when the task shape justifies it.

## Meet the AI team

When Work exposes exact model routing, the preferred roles are:

- **Luna — Coordinator and everyday worker.** Organizes context, classifies the task, combines results, and verifies the outcome.
- **Terra — Main implementer.** Handles medium and difficult execution that needs more judgment, integration, or debugging.
- **Sol — Senior architect and problem solver.** Enters for ambiguous, high-impact, hard-to-reverse, or deeply complex decisions.
- **Fresh Sol — Independent reviewer.** Reviews critical outcomes in a separate workstream when Work can provide it.

If Work does not expose exact model routing, the same workflow uses generic roles rather than pretending a hidden worker is Luna, Terra, or Sol.

## How it works

```text
                         USER
                           │
                           ▼
                    ┌─────────────┐
                    │   PARENT    │
                    │ Coordinator │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   Simple/routine      Medium work       Complex decision
        │                  │                  │
        ▼                  ▼                  ▼
   light worker       implementer       specialist
        │                  │                  │
        │                  │          specialist defines plan
        │                  │                  │
        │                  ◄──────────────────┘
        │                  │
        └──────────────────┴───────────────┐
                                           ▼
                                    Parent verifies
                                           │
                                      Critical task?
                                       /         \
                                     No           Yes
                                     │             │
                                    DONE    Independent review
```

When exact model control is available, those roles map to Luna, Terra, and Sol. Otherwise, the role contracts remain the same without unsupported model claims.

## Three Work capability levels

Every run begins with a capability check:

- **Tier A — Exact routing.** Work exposes multi-agent execution and enough evidence to select the intended worker model. Luna/Terra/Sol names may be used when verified.
- **Tier B — Work multi-agent.** Work can run parallel agents, but exact worker model identity is not guaranteed. The plugin uses roles such as `implementation-worker` and `complex-specialist`.
- **Tier C — Safe fallback.** The plugin cannot access multiple agents. The parent performs the same structured workflow directly and reports that delegation was unavailable.

This prevents the plugin from claiming a model, reasoning level, fresh context, or sandbox guarantee that Work did not prove.

## The five task levels

- **Mechanical** — repetitive or highly predictable work. Tier A prefers Luna/light.
- **Routine** — clearly defined everyday work. Tier A prefers Luna/medium.
- **Medium** — normal implementation, integration, moderate debugging, or local judgment. Tier A prefers Terra/medium.
- **Complex** — architecture, difficult root-cause analysis, conflicting requirements, or high-impact upstream decisions. Tier A prefers Sol/high for the decision, then Terra for implementation when appropriate.
- **Critical** — security, destructive changes, financial correctness, difficult concurrency, irreversible migrations, or similarly high-impact work. Use the strongest independent path the current runtime can actually prove.

## Why Sol is not used all the time

The goal is not to avoid Sol. The goal is to **use stronger reasoning where it changes the outcome most**.

```text
Efficient pattern:
Parent organizes the task
        ↓
Complex specialist solves the difficult decision
        ↓
Implementation worker executes the agreed plan
        ↓
Parent verifies the result
```

In Tier A, that preferred pattern becomes Luna → Sol → Terra → Luna verification.

## Safety valve: the economical coordinator cannot keep every task

Luna Advisor Work has mandatory escalation triggers. The complex path is required when important issues such as these appear:

- unclear or conflicting architecture;
- security, authentication, or authorization;
- destructive or difficult-to-reverse data changes;
- financial correctness or irreversible external actions;
- difficult concurrency or distributed state;
- large changes affecting several systems;
- repeated failed checks without a clear cause;
- decisions whose mistakes would affect many later workers;
- an explicit request for maximum-quality reasoning.

The system therefore does not depend only on the coordinator's confidence.

## Parallel research, controlled implementation

```text
Research:        Scout A ─┐
                 Scout B ─┼──► Parent combines findings
                 Scout C ─┘

Implementation:             ► One writer ► Parent verifies
```

Parallel work is encouraged for independent reading, repository exploration, comparisons, evidence collection, and test-gap analysis. Shared-state changes normally use **one writer at a time**.

## Designed for ChatGPT Work

Luna Advisor Work targets Work's hosted execution model rather than Codex-local custom-agent TOML files. It deliberately avoids depending on local rollout inspectors or unproven per-agent sandbox guarantees.

## Technical reliability

The repository includes:

- the standard `.agents/plugins/marketplace.json` entry;
- an installable package under `plugins/luna-advisor-work/`;
- `.codex-plugin/plugin.json` and skill metadata following the OpenAI plugin layout;
- an explicit A/B/C runtime capability gate;
- mandatory escalation triggers for high-impact work;
- scoped worker contracts and parent verification rules;
- serialized shared-state writers;
- GitHub Actions verification via `scripts/verify.py` to detect missing files, invalid JSON, package drift, bad marketplace paths, oversized starter prompts, and missing capability-contract markers.

Static packaging can be validated by CI. Exact multi-model routing remains a runtime capability of ChatGPT Work and is never falsely presented as a repository-level guarantee.

## Runtime evidence and efficiency guardrails

Each run must begin with a capability probe and record an execution ID when the
host provides one. Every lane separates the requested model/reasoning from
request acceptance, effective-model attestation, usage verification, tokens,
and cost. Hidden controls fail closed to semantic roles or parent-only work.

The delegation gate accounts for spawn, context-transfer, synthesis, and
verification overhead. Tiny deterministic work stays in the parent, delegated
implementation has one writer, and reviews are added only when risk or an
explicit audit justifies them. See `skills/orchestration/references/runtime-evidence.md`.

## Luna Advisor Work vs. Sol Advisor Work

| | Luna Advisor Work | Sol Advisor Work |
|---|---|---|
| Main philosophy | Efficiency-first | Quality-first |
| Easy work | Keep it light | Delegate when useful |
| Medium implementation | Implementation worker | Implementation worker |
| Complex reasoning | Escalate to specialist | Strong reasoning stays near the control plane |
| Critical review | Independent review when available | Independent review when available |
| Best fit | Frequent everyday workflows | Important or difficult workflows |

**Use Luna Advisor Work when efficiency matters most.**  
**Use Sol Advisor Work when maximum confidence matters most.**

## For technical users

The complete routing and safety contracts live in:

- `skills/orchestration/SKILL.md`
- `skills/orchestration/references/role-contracts.md`
- `skills/orchestration/references/operations.md`

The installable copy is mirrored under `plugins/luna-advisor-work/`, and CI requires both copies to remain identical.

## Attribution

Luna Advisor Work is structurally inspired by [DannyMac180/sol-advisor](https://github.com/DannyMac180/sol-advisor), created by Daniel McAteer and distributed under the MIT License. This Work-native adaptation is maintained separately.
