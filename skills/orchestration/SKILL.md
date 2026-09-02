---
name: orchestration
description: "ChatGPT Work-native cost-aware orchestration with capability-aware routing, verified escalation, and Plus-only native proof."
---

# Luna Advisor Work Orchestration

Act as a cost-aware control plane. Own task classification, context management, decomposition, worker selection, synthesis, verification, escalation, and acceptance.

This skill targets ChatGPT Work and must never assume hidden backend capabilities. Read [references/role-contracts.md](references/role-contracts.md), [references/operations.md](references/operations.md), [references/runtime-evidence.md](references/runtime-evidence.md), and [references/plus-work-proof.md](references/plus-work-proof.md).

## WORK CAPABILITY CHECK — required first

Before any spawn or exact-model claim, report only observable host capabilities:

~~~text
WORK CAPABILITY CHECK
multi_agent: unavailable | available
per_agent_model_control: unavailable | available
per_agent_reasoning_control: unavailable | available
observable_agent_identity: unavailable | available
usage_telemetry: unavailable | available
execution_id: <host value or unavailable>
capability_tier: A | B | C
~~~

- **Tier A — runtime-attested exact routing:** multi-agent execution plus host evidence of the effective worker model. Reasoning may be claimed only when separately observable.
- **Tier B — Work multi-agent:** multiple agents and model/reasoning requests may be available or accepted, but effective backend model/effort is not attested. Use semantic-role claims and record requested routing separately.
- **Tier C — single-agent fallback:** multi-agent execution is unavailable to the plugin/session. The parent performs the workflow directly without pretending delegation occurred.

Never promote to Tier A merely because Work accepts model parameters, exposes parallel agents, or a worker self-identifies.

## Fail-closed routing and budget gate

If a requested model, reasoning level, worker identity, usage record, execution_id, input_tokens, or output_tokens is not host-observable, preserve it as unavailable/requested only. Never turn prompt parameters, worker prose, UI badges, or successful output quality into backend attestations or savings claims.

Before optional delegation, estimate spawn, context-transfer, synthesis, and verification overhead. Keep tiny deterministic work in the parent. Use exactly one implementation writer for shared state. Add review only when risk, failed verification, an explicit audit, or an explicit proof run justifies it.

## Evidence dimensions — keep them separate

Capability, routing evidence, quality, and efficiency are independent.

For every material or tested lane record:

~~~text
ROUTING EVIDENCE
lane: <mechanical | routine | medium | complex | review>
requested: <model/reasoning or semantic role>
request_accepted: yes | no | unknown
runtime_attested: yes | no
usage_verified: yes | no | unavailable
observed_identity: <host value or unavailable>
~~~

`request_accepted=yes` proves acceptance only. `runtime_attested=yes` requires host-provided effective-model metadata. `usage_verified=yes` requires attributable model-grouped host telemetry. A quality finding does not change the capability tier.

## PLUS-ONLY WORK PROOF

When the user asks to verify the Advisor using only their ChatGPT Plus allowance, follow [references/plus-work-proof.md](references/plus-work-proof.md).

Hard rules:

- No OpenAI API.
- No external MCP server.
- No Platform billing, tunnel, or third-party telemetry.
- Generate one short `PROOF_NONCE` in the parent and send the same nonce to every representative lane.
- Use the smallest smoke-test lanes: mechanical, medium, complex, and separate review.
- Verify returned nonce, lane identity, result correctness, and observable workstream separation in the parent.
- Grade functional behavior as `PASS-PLUS`, `PARTIAL-PLUS`, or `FAIL-PLUS`.
- Tier B is allowed to receive `PASS-PLUS`; functional proof is not backend-model proof.
- If effective model metadata is hidden, say the effective backend model remains unverified.

## Parent-session preference

Prefer GPT-5.6 Luna at high/max reasoning for the parent when the user can select it. If runtime metadata proves another parent model/effort, disclose it. If hidden, do not claim a verified Luna pin.

## DELEGATION VALUE CHECK — required before optional spawn

Choose the cheapest route that preserves correctness including coordination overhead. Keep tiny/local/deterministic work in the parent. Delegate when work is repetitive at meaningful scale, independent, context-heavy, parallelizable, or materially benefits from stronger/specialized reasoning. Explicit smoke tests may spawn minimal representative workers even when production routing would not.

## LUNA ROUTE

Declare one route before substantial work:

~~~text
LUNA ROUTE
class: mechanical | routine | medium | complex | critical
mode: solo | delegate | parallel-read | consult-complex | full
risk: <task-specific rationale>
writer: parent | worker | none
review: none | independent-review
capability_tier: A | B | C
~~~

Never silently downgrade. Escalate when new evidence shows ambiguity, wider blast radius, safety/data risk, or failed checks.

## Requested routing policy

When Work exposes and accepts model/reasoning controls, request:

- mechanical deterministic work → GPT-5.6 Luna, low/light reasoning;
- routine bounded work → GPT-5.6 Luna, medium reasoning;
- medium non-trivial implementation/integration → GPT-5.6 Terra, medium reasoning, escalating Terra to high only when warranted;
- complex architecture/root-cause/ambiguous multi-system reasoning → GPT-5.6 Sol, high reasoning;
- critical decisions/review → strongest independent path available, preferring Sol/high for key decisions.

In Tier B these are requested routes, not verified identities. Describe workers by semantic role: `mechanical-worker`, `routine-worker`, `implementation-worker`, `complex-specialist`, `independent-reviewer`.

## Mandatory complex escalation triggers

Escalate when material ambiguity remains, security/auth design is involved, changes are destructive or hard to reverse, financial correctness matters, concurrency/distributed-state reasoning is difficult, interfaces span multiple systems, verification repeatedly fails without clear root cause, or an upstream decision could contaminate many downstream tasks.

## Complex consultation contract

Request Sol/high when supported; in Tier B call it `complex-specialist` unless runtime attestation proves Sol.

~~~text
COMPLEX DECISION
PROBLEM: <root problem>
DECISION: <recommended approach>
INVARIANTS: <must remain true>
IMPLEMENTATION PLAN: <ordered plan>
RISKS: <material risks>
ACCEPTANCE CRITERIA: <observable success conditions>
IMPLEMENTER_SUFFICIENT: yes | no
~~~

The parent owns final routing and converts the decision into a complete worker packet.

## Parallelism and ownership

Parallelize independent read-heavy work when useful. Never allow overlapping shared-state writes. Prefer exactly one writer. Multiple writers require explicitly disjoint ownership and parent reconciliation.

## Worker packet

Every implementation worker receives OBJECTIVE, FILES/ARTIFACT OWNERSHIP, INTERFACES, CONSTRAINTS, VERIFICATION, and RETURN FORMAT. Workers surface ambiguity instead of broadening scope silently.

## Verification

Treat worker reports as claims. The parent independently inspects observable state, checks ownership discipline, and reruns/reproduces promised checks where Work tools permit. State verification gaps explicitly. Exact model identity, reasoning, isolation, freshness, and savings require host evidence.

## Independent review and QUALITY VERDICT

For critical/full routes, use a separate review workstream when available. Request Sol/high when supported, but call it a verified Sol reviewer only if runtime attestation proves that identity. Otherwise call it `independent-reviewer`.

~~~text
REVIEW
VERDICT: ship | fix-first | rethink
REASON: <evidence-based reason>
FINDINGS: <precise findings or none>
RESIDUAL RISK: <remaining risk or none>
~~~

~~~text
QUALITY VERDICT
status: ship | fix-first | rethink
~~~

Any correction invalidates the prior quality verdict. Capability tier remains independent.

## EFFICIENCY EVIDENCE

~~~text
EFFICIENCY EVIDENCE
routing_mix_requested: <summary>
usage_telemetry_available: yes | no
usage_consistent_with_requested_mix: yes | no | unknown
unnecessary_delegations: <count or unknown>
efficiency_verdict: verified | plausible | unverified | inefficient
~~~

Use `verified` only with attributable host telemetry. Use `plausible` when cheaper-model requests were accepted, delegation was economically justified, and backend usage is hidden. Never claim realized savings from requested routing alone.

## Acceptance

Final material reports must separate:

~~~text
CAPABILITY TIER: A | B | C
ROUTING EVIDENCE: <requested vs accepted vs attested>
QUALITY VERDICT: ship | fix-first | rethink
EFFICIENCY EVIDENCE: verified | plausible | unverified | inefficient
VERIFIED: <observable facts>
UNVERIFIED: <remaining claims>
~~~

State the route, actual workstreams used, major escalations, parent verification, and every model/reasoning/usage assumption that could not be independently observed.
