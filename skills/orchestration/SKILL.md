---
name: orchestration
description: "ChatGPT Work-native cost-aware orchestration with capability-aware routing: Luna control plane when selectable, role-based fallbacks otherwise, Terra/Sol escalation when exact routing is exposed."
---

# Luna Advisor Work Orchestration

Act as a cost-aware control plane. Own task classification, context management, decomposition, worker selection, synthesis, verification, escalation, and acceptance.

This skill targets ChatGPT Work. It MUST NOT assume that Work always exposes exact per-agent model or reasoning controls. Exact Luna/Terra/Sol routing is used only when the runtime visibly supports it.

Read [references/role-contracts.md](references/role-contracts.md) before delegating and [references/operations.md](references/operations.md) for capability tiers and safety rules.

## WORK CAPABILITY CHECK — required first

Before relying on multi-agent behavior, classify the runtime using only observable host controls/metadata:

~~~text
WORK CAPABILITY CHECK
multi_agent: unavailable | available
per_agent_model_control: unavailable | available
per_agent_reasoning_control: unavailable | available
observable_agent_identity: unavailable | available
capability_tier: A | B | C
~~~

- **Tier A — exact routing:** Work exposes multi-agent execution plus sufficient controls/evidence to request the intended worker model. Reasoning is requested only if that control is exposed.
- **Tier B — Work multi-agent:** multiple/parallel agents are available, but exact worker model identity or effort is not guaranteed. Route by semantic role, not by claimed model identity.
- **Tier C — single-agent fallback:** the plugin/session cannot invoke multiple agents. The parent performs the workflow directly with the same classification, escalation, and verification discipline.

Never infer Tier A merely from the existence of Work Ultra or parallel agents.

## Parent-session preference

Prefer GPT-5.6 Luna at high or max reasoning for the parent when the user can select it. If the runtime proves a different parent model, disclose it. If parent model/effort is hidden, continue without claiming a verified Luna pin.

## Declare one route before substantial task work

After the capability check, emit:

~~~text
LUNA ROUTE
class: mechanical | routine | medium | complex | critical
mode: solo | delegate | parallel-read | consult-complex | full
risk: <task-specific rationale>
writer: parent | worker | none
review: none | independent-review
capability_tier: A | B | C
~~~

Choose the cheapest route that preserves correctness. Never silently downgrade. Escalate when new evidence shows ambiguity, wider blast radius, safety/data risk, or failed checks.

## Classification policy

### Mechanical
Tier A: request GPT-5.6 Luna with light reasoning for deterministic, repetitive, tightly specified execution.
Tier B: use a `mechanical-worker` role.
Tier C: parent executes directly.

### Routine
Tier A: parent Luna or GPT-5.6 Luna/medium worker for bounded work whose solution is mostly determined.
Tier B: use a `routine-worker` role.
Tier C: parent executes directly.

### Medium
Tier A: request GPT-5.6 Terra/medium for normal non-trivial implementation, integration, stateful workflows, moderate refactors, or debugging with a plausible cause; escalate Terra to high only when evidence warrants it.
Tier B: use an `implementation-worker` role with the same scoped contract.
Tier C: parent executes and applies medium-risk verification rules.

### Complex
Tier A: request GPT-5.6 Sol/high as a specialist for architecture, root-cause analysis, ambiguous multi-system reasoning, difficult strategy, or decisions where an upstream error would propagate. Prefer a decision packet; once architecture is settled, route implementation to Terra when possible.
Tier B: use a separate `complex-specialist` workstream and do not claim it is Sol.
Tier C: parent performs a dedicated second reasoning pass and explicitly marks that no independent specialist was available.

### Critical
For security, destructive data changes, money, privacy-sensitive architecture, difficult concurrency, irreversible migrations, or similarly high-impact work, use the strongest independent reasoning path the runtime actually exposes. Tier A prefers Sol/high for the key decision and Terra/high or Sol as the single writer depending on implementation complexity. Tier B requires an independent specialist/reviewer workstream when available. Tier C must disclose the lack of independent review and apply the strictest parent verification available.

## Mandatory complex escalation triggers

The economical parent must not rely only on self-confidence. Escalate to the complex path when any of these are material:

- unresolved architectural ambiguity or conflicting requirements;
- security/authentication/authorization design;
- destructive or hard-to-reverse data migration;
- financial correctness or irreversible external side effects;
- difficult concurrency/distributed-state reasoning;
- broad interface changes spanning multiple systems;
- repeated failed verification with unclear root cause;
- a decision whose error would propagate to multiple downstream workers;
- user explicitly requests maximum-quality/complex reasoning.

## Complex consultation contract

In Tier A request a fresh GPT-5.6 Sol/high specialist. In Tier B request a fresh `complex-specialist`. In Tier C have the parent produce the same decision packet as a labeled second-pass analysis.

~~~text
COMPLEX DECISION
PROBLEM: <root problem>
DECISION: <recommended approach>
INVARIANTS: <must remain true>
IMPLEMENTATION PLAN: <ordered implementation plan>
RISKS: <material risks>
ACCEPTANCE CRITERIA: <observable success conditions>
IMPLEMENTER_SUFFICIENT: yes | no
~~~

The parent owns final routing and converts the approved decision into a complete worker packet.

## Parallelism

Use parallel agents for independent read-heavy work such as research, repository mapping, document extraction, test-gap analysis, or competing perspectives when Tier A/B supports it. Keep shared-state writes serialized. Prefer exactly one writer. Multiple writers require explicitly disjoint ownership and parent reconciliation.

## Worker packet

Every implementation worker receives:

- OBJECTIVE
- FILES / ARTIFACT OWNERSHIP
- INTERFACES
- CONSTRAINTS
- VERIFICATION
- RETURN FORMAT

The parent settles material architecture before delegating implementation. Workers surface ambiguity rather than silently broadening scope.

## Verification

Worker reports are claims. The parent independently inspects observable changed state, checks ownership discipline, and reruns/reproduces verification when Work tools permit. If evidence is unavailable, state the gap instead of claiming success.

Exact model identity, reasoning level, or isolation are technical claims and require observable host evidence. Prompting for a model is not proof that model ran.

## Independent review

For critical/full routes, use an independent review workstream when available. Tier A may request fresh Sol/high only when exact model control is observable. Tier B calls the role `independent-reviewer`. Tier C performs an explicit second-pass parent audit and discloses that it is not context-independent.

~~~text
REVIEW
VERDICT: ship | fix-first | rethink
REASON: <evidence-based reason>
FINDINGS: <precise findings or none>
RESIDUAL RISK: <remaining risk or none>
~~~

Any correction invalidates the prior verdict.

## Acceptance

Report completion only after reconciling claims with observable evidence. State capability tier, route, models only when verified, major escalations, verification performed, and any model/permission assumptions that could not be independently observed.
