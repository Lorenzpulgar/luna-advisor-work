# Luna Advisor Work role contracts

These contracts target ChatGPT Work and are interpreted through the capability tier declared by `SKILL.md`.

## Naming rule

- Tier A may use exact model lane names only when the runtime exposes evidence for them.
- Tier B uses semantic roles and does not claim hidden model identity.
- Tier C executes the same logical packet in the parent and makes no delegation claim.

A requested model, reasoning level, fresh context, or read-only instruction is not itself proof that the runtime enforced it.

## Shared worker packet

~~~text
ROLE
<mechanical-worker | routine-worker | implementation-worker | complex-specialist>

OBJECTIVE
<Observable outcome and why it matters.>

FILES / ARTIFACT OWNERSHIP
You own only:
- <exact scope>

Preserve concurrent edits and do not modify unowned state.

INTERFACES
- <APIs, schemas, formats, behavior, visual rules, compatibility requirements.>

CONSTRAINTS
- <settled architecture, safety boundaries, excluded scope, style/performance requirements.>

VERIFICATION
- Check: <command, inspection, query, render, consistency test>
  Success: <observable evidence>

RETURN
IMPLEMENTATION REPORT
STATUS: complete | partial | blocked
OBJECTIVE: <one-line restatement>
CHANGES: <artifact-by-artifact summary>
VERIFIED: <checks and actual evidence>
JUDGMENT CALLS: <choices left open by the packet, or none>
GAPS: <unfinished work or none>
~~~

## Mechanical lane

Tier A may request GPT-5.6 Luna/light. Tier B uses `mechanical-worker`. Use for deterministic, repetitive, tightly specified execution. The worker must not redesign architecture, broaden scope, or invent interfaces.

## Routine lane

Tier A may request GPT-5.6 Luna/medium. Tier B uses `routine-worker`. Use for bounded work spanning more context while still having a mostly determined solution. Surface ambiguity instead of turning it into architecture.

## Implementation lane

Tier A may request GPT-5.6 Terra/medium for ordinary non-trivial implementation, integration, moderate refactors, stateful workflows, and debugging with a plausible cause; Terra/high is an evidence-based escalation. Tier B uses `implementation-worker`.

## Complex specialist

Tier A may request GPT-5.6 Sol/high when exact routing is observable. Tier B uses `complex-specialist`. Tier C has the parent perform the same packet as a labeled second-pass analysis.

~~~text
COMPLEX DECISION
PROBLEM: <root problem>
DECISION: <recommended architecture/approach>
INVARIANTS: <must remain true>
IMPLEMENTATION PLAN: <ordered steps>
RISKS: <material risks>
ACCEPTANCE CRITERIA: <observable success conditions>
IMPLEMENTER_SUFFICIENT: yes | no
~~~

The parent translates the decision into an implementation packet and chooses the writer.

## Independent reviewer

Use when risk justifies independent context. Tier A may request Sol/high only when observable; Tier B uses `independent-reviewer`; Tier C performs a disclosed parent second pass.

~~~text
ROLE
Act as an independent final reviewer when operating in a separate workstream. Do not edit or implement fixes.

STATED GOAL
<user outcome>

ACCUMULATED CHANGE SET
<exact changed scope and observable state>

INTERFACES AND CONSTRAINTS
<requirements that must hold>

VERIFICATION EVIDENCE
<parent-observed checks>

REVIEW
VERDICT: ship | fix-first | rethink
REASON: <decisive evidence>
FINDINGS: <precise findings or none>
RESIDUAL RISK: <remaining risk or none>
~~~

Never claim hard read-only isolation unless Work exposes proof. A correction invalidates the prior verdict.

## Parallel read worker

Read workers receive one narrow question, no mutation objective, and a concise evidence-backed return. Multiple readers may run concurrently when independent. The parent resolves conflicts and owns final synthesis.
