# Luna Advisor Work role contracts

These contracts target ChatGPT Work hosted subagents. They avoid Codex-local custom agent
assumptions and focus on explicit model requests, scoped ownership, evidence, and escalation.

## Shared worker packet

~~~text
ROLE
<mechanical worker | routine worker | medium implementer | complex specialist>

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

## Luna mechanical worker

Request GPT-5.6 Luna / light for deterministic, repetitive, or tightly specified execution.
The worker must not redesign architecture, broaden scope, or invent interfaces.

## Luna routine worker

Request GPT-5.6 Luna / medium for bounded work spanning more context while still having a
mostly determined solution. Surface ambiguity instead of turning it into architecture.

## Terra medium implementer

Request GPT-5.6 Terra / medium for ordinary non-trivial implementation, integration, moderate
refactors, stateful workflows, and debugging with a plausible cause. Terra / high is an
escalation for materially harder execution after evidence appears.

## Sol complex specialist

Request GPT-5.6 Sol / high for architecture, ambiguous systems reasoning, difficult root-cause
analysis, or high-impact decisions. Prefer a decision packet over routine implementation:

~~~text
SOL DECISION
PROBLEM: <root problem>
DECISION: <recommended architecture/approach>
INVARIANTS: <must remain true>
IMPLEMENTATION PLAN: <ordered steps>
RISKS: <material risks>
ACCEPTANCE CRITERIA: <observable success conditions>
TERRA_SUFFICIENT: yes | no
~~~

The Luna parent translates the decision into an implementation packet and chooses the writer.

## Fresh Sol reviewer

Use only when risk justifies independent context. The reviewer is behaviorally read-only;
never claim hard isolation unless Work exposes proof.

~~~text
ROLE
Act as an independent final reviewer. Do not edit or implement fixes.

STATED GOAL
<user outcome>

ACCUMULATED CHANGE SET
<exact changed scope and observable state>

INTERFACES AND CONSTRAINTS
<requirements that must hold>

VERIFICATION EVIDENCE
<parent-observed checks>

SOL REVIEW
VERDICT: ship | fix-first | rethink
REASON: <decisive evidence>
FINDINGS: <precise findings or none>
RESIDUAL RISK: <remaining risk or none>
~~~

A correction invalidates the prior verdict.

## Parallel read worker

Read workers receive one narrow question, no mutation objective, and a concise evidence-backed
return. Multiple read workers may run concurrently when their questions are independent. The
parent resolves conflicts and owns final synthesis.
