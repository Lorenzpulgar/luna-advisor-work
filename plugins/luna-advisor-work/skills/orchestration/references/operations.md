# Luna Advisor Work operations

This reference defines runtime-safe, cost-aware routing and verification for ChatGPT Work.

## Capability tiers

Run the `WORK CAPABILITY CHECK` from `SKILL.md` first.

| Tier | What is proven | Allowed routing claims |
|---|---|---|
| A | Multi-agent plus observable per-agent model routing | Exact Luna/Terra/Sol names; reasoning only if separately observable |
| B | Multi-agent/parallel Work execution, exact worker model not proven | Semantic roles only |
| C | No plugin-visible multi-agent execution | Parent-only execution; no delegation claims |

Never infer Tier A from Work Ultra alone.

## Classification matrix

| Class | Tier A preferred lane | Tier B role | Tier C |
|---|---|---|---|
| mechanical | Luna / light | mechanical-worker | parent |
| routine | Luna / medium | routine-worker | parent |
| medium | Terra / medium | implementation-worker | parent |
| complex | Sol / high decision | complex-specialist | parent second-pass complex analysis |
| critical | strongest proven path + independent review | specialist + reviewer | strict parent verification with limitation disclosed |

## Mandatory complex escalation

Escalate regardless of parent confidence when the task materially involves architectural ambiguity, auth/authz or security design, destructive data migration, financial correctness, difficult concurrency/distributed state, wide interface changes, repeated unclear verification failure, or an upstream decision that would propagate across multiple workers.

## Preferred complex pattern

Tier A:

~~~text
Luna parent
  -> parallel read scouts when useful
  -> Sol / high decision packet
  -> parent freezes architecture
  -> Terra / medium or high implements as the single writer
  -> parent verifies observable state
  -> fresh Sol review only when justified and observable
~~~

Tier B keeps the same shape but uses role names instead of model claims:

~~~text
Parent
  -> parallel readers
  -> complex-specialist
  -> implementation-worker
  -> parent verification
  -> independent-reviewer when justified
~~~

Tier C executes the same logical phases in the parent and explicitly reports that specialist/reviewer independence was unavailable.

## Work constraints

- Subagents may inherit parent tools and permissions.
- Do not depend on Codex-local custom-agent TOML registration, local runtime inspectors, or per-agent sandbox enforcement.
- A model/reasoning request is not proof of actual routing.
- Parallelize independent read-heavy work; serialize shared-state writes.
- Never claim model/effort/freshness/isolation evidence the host did not expose.

## Parallel read pattern

Use parallel readers only for independent questions and no mutation objective. Avoid overlapping writers. If multiple writers are unavoidable, ownership must be disjoint and the parent must inspect the combined state.

## Verification

For delegated execution, the parent should:

1. inspect actual changed files/artifacts/state;
2. compare changed scope with ownership;
3. rerun checks or equivalent validation when tools permit;
4. reconcile gaps and judgment calls;
5. escalate when evidence shows higher complexity;
6. state verification gaps explicitly.

## Routing failure policy

If a requested capability/model/effort is unavailable or hidden:

- hard guarantee required by user: stop that lane and report the limitation;
- otherwise downgrade capability tier, preserve task safety, disclose the fallback, and never claim the requested routing was verified.

If the parent cannot tell whether a task is medium or complex and a wrong choice has meaningful downstream cost, bias upward to the complex path rather than guessing downward.

## Review policy

Independent review is for critical/high-risk outcomes, surprising implementation diffs, or tasks where context independence materially improves confidence. Tier A may name Sol only when verified. Tier B uses `independent-reviewer`. Tier C performs a disclosed parent second pass. Any correction invalidates the verdict.
