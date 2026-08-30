# Luna Advisor Work operations

This reference defines the cost-aware routing and verification rules for ChatGPT Work.

## Work constraints

- Hosted subagents may accept requested model and reasoning controls when the host exposes them.
- Subagents may inherit parent tools and permissions.
- Do not depend on Codex-local custom-agent TOML registration, local runtime inspectors, or per-agent sandbox enforcement.
- Parallelize independent read-heavy work; serialize shared-state writes.
- Never claim model/effort/isolation evidence the host did not expose.

## Classification matrix

| Class | Default model | Effort | Typical work |
|---|---|---|---|
| mechanical | Luna | light | deterministic edits, extraction, formatting, simple wiring |
| routine | Luna | medium | bounded execution with mostly settled solution |
| medium | Terra | medium | non-trivial implementation, integration, moderate refactor/debugging |
| complex | Sol | high | architecture, ambiguity, deep root-cause reasoning |
| critical | Sol + Terra/Sol writer | high | high-impact or irreversible work, plus fresh Sol review when useful |

## Mandatory Sol escalation

Escalate regardless of Luna confidence when the task materially involves architecture ambiguity,
auth/authz or security design, destructive data migration, financial correctness, difficult
concurrency/distributed state, wide interface changes, repeated unclear verification failure, or
an upstream decision that would propagate across multiple workers.

## Preferred complex pattern

~~~text
Luna parent
  -> parallel read scouts when useful
  -> fresh Sol / high decision packet
  -> Luna synthesizes and freezes architecture
  -> Terra / medium or high implements as the single writer
  -> Luna verifies observable state
  -> fresh Sol review only if critical/high risk
~~~

Do not pay Sol to perform routine execution after the hard decision is settled unless Terra is
not sufficient.

## Parallel read pattern

Good:

~~~text
Scout A: map interfaces/dependencies; no writes.
Scout B: inspect tests/regressions; no writes.
Scout C: research relevant documentation; no writes.
Parent: synthesize and classify.
Writer: one Luna/Terra/Sol implementation lane.
~~~

Avoid overlapping writers. If multiple writers are unavoidable, ownership must be disjoint and
the parent must inspect the combined state.

## Verification

For delegated execution, the Luna parent should:

1. inspect actual changed files/artifacts/state;
2. compare the changed scope with ownership;
3. rerun checks or equivalent validation when the current tools permit;
4. reconcile gaps and judgment calls;
5. escalate when evidence shows higher complexity than initially classified;
6. state any verification gap explicitly.

## Routing failure policy

If a requested model/effort is unavailable or hidden:

- If the user required a hard pin, stop that lane and report the limitation.
- Otherwise use the closest appropriate available lane only when doing so preserves task safety,
  disclose the fallback, and do not claim the requested routing was verified.

If Luna cannot tell whether a task is medium or complex and the downstream cost of a wrong choice
is meaningful, bias upward to a Sol consultation rather than guessing downward.

## Review policy

Fresh Sol review is for critical/high-risk outcomes, surprising implementation diffs, or tasks
where context independence materially improves confidence. The reviewer is behaviorally read-only
unless the host explicitly proves stronger isolation. Any correction invalidates the verdict.
