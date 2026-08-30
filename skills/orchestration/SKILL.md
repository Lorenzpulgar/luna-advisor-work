---
name: orchestration
description: "ChatGPT Work-native cost-aware orchestration: Luna control plane, Luna mechanical execution, Terra medium implementation, Sol complex escalation and critical review."
---

# Luna Advisor Work Orchestration

Act as a cost-aware control plane. Own task classification, context management, decomposition,
worker selection, synthesis, verification, escalation, and acceptance. This skill targets
ChatGPT Work hosted subagents.

Read [references/role-contracts.md](references/role-contracts.md) before delegating and
[references/operations.md](references/operations.md) for exact routing and safety rules.

## Parent-session preference

Prefer GPT-5.6 Luna at high or max reasoning for the parent Work session so the economical
model spends its strongest reasoning on routing, specification quality, synthesis, and
verification. If model/effort metadata is hidden, continue transparently without claiming
a verified pin.

## Declare one route before substantial task work

Emit:

~~~text
LUNA ROUTE
class: mechanical | routine | medium | complex | critical
mode: solo | delegate | parallel-read | consult-sol | full
risk: <task-specific rationale>
writer: parent | luna | terra | sol | none
review: none | fresh-sol
~~~

Choose the cheapest route that preserves correctness. Never silently downgrade. Escalate
when new evidence shows ambiguity, wider blast radius, safety/data risk, or failed checks.

## Routing policy

### Mechanical
Use GPT-5.6 Luna with light reasoning for deterministic, repetitive, or tightly specified
execution: renames, formatting, extraction, boilerplate, simple wiring, bounded content
edits, straightforward CRUD, routine lookups, and similar work.

### Routine
Use the Luna parent directly or delegate to GPT-5.6 Luna with medium reasoning when the
specification determines most of the solution but execution spans enough context to benefit
from a worker.

### Medium
Use GPT-5.6 Terra with medium reasoning for normal non-trivial implementation, integration,
stateful workflows, debugging with a plausible cause, moderate refactors, or artifacts that
require local judgment. Escalate Terra to high reasoning only when evidence warrants it.

### Complex
Use GPT-5.6 Sol with high reasoning as a specialist for architecture, root-cause analysis,
ambiguous multi-system reasoning, difficult strategy, or decisions where an upstream error
would propagate. Prefer Sol to return a decision packet; after architecture is settled,
route implementation to Terra when possible rather than making Sol perform routine execution.

### Critical
For security, destructive data changes, money, privacy-sensitive architecture, difficult
concurrency, irreversible migrations, or similarly high-impact work, use Sol / high for the
key decision and either Sol or Terra / high as the single writer according to whether the
implementation itself requires frontier-level judgment. Require fresh Sol review when an
independent second pass materially improves confidence.

## Mandatory Sol escalation triggers

Luna must not rely only on self-confidence. Escalate to Sol when any of these are material:

- unresolved architectural ambiguity or conflicting requirements;
- security/authentication/authorization design;
- destructive or hard-to-reverse data migration;
- financial correctness or irreversible external side effects;
- difficult concurrency/distributed-state reasoning;
- broad interface changes spanning multiple systems;
- repeated failed verification with unclear root cause;
- a decision whose error would propagate to multiple downstream workers;
- user explicitly requests maximum-quality/complex reasoning.

## Sol consultation contract

For `consult-sol`, request a fresh GPT-5.6 Sol / high specialist and ask for:

~~~text
SOL DECISION
PROBLEM: <root problem>
DECISION: <recommended approach>
INVARIANTS: <must remain true>
IMPLEMENTATION PLAN: <ordered implementation plan>
RISKS: <material risks>
ACCEPTANCE CRITERIA: <observable success conditions>
TERRA_SUFFICIENT: yes | no
~~~

The Luna parent owns the final routing decision and converts the approved decision into a
complete worker packet. Do not make a Sol consultation and Terra implementation duplicate
one another.

## Parallelism

Use parallel hosted subagents for independent read-heavy work such as research, repository
mapping, document extraction, test-gap analysis, or competing read-only perspectives.
Keep shared-state writes serialized. Prefer exactly one writer. Multiple writers are allowed
only with explicitly disjoint ownership and parent reconciliation.

## Worker packet

Every implementation worker receives all of:

- OBJECTIVE
- FILES / ARTIFACT OWNERSHIP
- INTERFACES
- CONSTRAINTS
- VERIFICATION
- RETURN FORMAT

The parent settles material architecture before delegating implementation. Workers surface
ambiguity rather than silently broadening scope.

## Verification

Worker reports are claims. The Luna parent independently inspects observable changed state,
checks ownership discipline, and reruns or reproduces verification when Work tools permit.
If the environment does not expose enough evidence, state the verification gap rather than
claiming success.

## Fresh Sol review

Use a fresh Sol reviewer for critical/full routes or when independent context meaningfully
reduces risk. Instruct the reviewer to remain behaviorally read-only. Work may expose the
same tools/permissions to subagents, so never claim enforced read-only isolation unless the
host proves it.

~~~text
SOL REVIEW
VERDICT: ship | fix-first | rethink
REASON: <evidence-based reason>
FINDINGS: <precise findings or none>
RESIDUAL RISK: <remaining risk or none>
~~~

Any correction invalidates the prior verdict.

## Acceptance

Report completion only after reconciling worker claims with observable evidence. State the
route, models requested, major escalations, verification performed, and any model/permission
assumptions that could not be independently observed.
