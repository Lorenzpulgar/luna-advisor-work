# Luna Advisor Work

**A cost-efficient AI team for ChatGPT Work.**

Luna Advisor Work organizes GPT-5.6 Luna, Terra, and Sol like a small team. Instead of using the most powerful model for every step, it starts with the most economical model and only brings in more intelligence when the task truly needs it.

The main idea is simple: **Luna coordinates everyday work, Terra handles substantial implementation, and Sol is called for difficult decisions or critical review.**

## Why it exists

Many real tasks contain a mix of easy and difficult work. Researching files, making routine edits, organizing information, implementing a normal feature, and deciding a risky architecture are not the same kind of problem.

Using Sol for every single step can be unnecessary. Luna Advisor Work tries to keep quality high while spending stronger reasoning only where it has the most value.

This makes it an **efficiency-first** orchestrator.

## Meet the AI team

- **Luna — Coordinator and everyday worker.** Understands the task, organizes context, chooses the right specialist, handles routine work, combines results, and checks the final outcome.
- **Terra — Main implementer.** Handles medium and difficult execution that needs stronger judgment, integration, or debugging.
- **Sol — Senior architect and problem solver.** Enters when the problem is ambiguous, high-impact, difficult to reverse, or requires deep reasoning.
- **Fresh Sol — Independent reviewer.** For critical outcomes, a new Sol session can review the result from a clean perspective.

## How it works

```text
                         USER
                           │
                           ▼
                    ┌─────────────┐
                    │    LUNA     │
                    │ Coordinator │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   Simple/routine      Medium work       Complex decision
        │                  │                  │
        ▼                  ▼                  ▼
      LUNA               TERRA               SOL
   Light/Medium          Medium/High          High
        │                  │                  │
        │                  │          Sol defines the plan
        │                  │                  │
        │                  ◄──────────────────┘
        │                  │
        └──────────────────┴───────────────┐
                                           ▼
                                     LUNA verifies
                                           │
                                      Critical task?
                                       /         \
                                     No           Yes
                                     │             │
                                    DONE      Fresh SOL review
```

In plain English:

1. **Luna looks at the task and decides how difficult it is.**
2. Simple and repetitive work stays with Luna.
3. Normal non-trivial implementation goes to Terra.
4. Difficult architecture, unclear root causes, or high-impact decisions go to Sol.
5. When possible, Sol makes the difficult decision and Terra performs the implementation. This avoids using Sol for routine execution after the hard thinking is already finished.
6. Luna checks the actual result.
7. Critical work can receive an independent review from a fresh Sol.

## The five task levels

Luna Advisor Work classifies work into five easy-to-understand levels:

- **Mechanical** — repetitive or highly predictable work. Usually Luna with light reasoning.
- **Routine** — clearly defined everyday work. Usually Luna with medium reasoning.
- **Medium** — normal implementation, integration, moderate debugging, or work requiring local judgment. Usually Terra.
- **Complex** — architecture, difficult root-cause analysis, conflicting requirements, or decisions that affect many later steps. Usually Sol for the decision, then Terra for implementation when appropriate.
- **Critical** — security, destructive changes, financial correctness, difficult concurrency, irreversible migrations, or similarly high-impact work. Sol is required for the key decision and a fresh Sol review may be added.

## Why Sol is not used all the time

Sol is most valuable when a mistake in reasoning would affect everything that comes after it.

For example:

```text
Bad use of Sol:
Sol reads files → Sol renames things → Sol writes boilerplate → Sol runs routine checks

Better use of Sol:
Luna organizes the task
        ↓
Sol solves the difficult architectural decision
        ↓
Terra implements the agreed plan
        ↓
Luna verifies the result
```

The goal is not to avoid Sol. The goal is to **use Sol where stronger reasoning creates the biggest improvement**.

## Safety valve: Luna cannot keep every task for itself

A cheaper coordinator has one important risk: it might underestimate how difficult a task really is.

To reduce that risk, Luna Advisor Work has mandatory escalation rules. Luna must bring in Sol when important issues such as these appear:

- unclear or conflicting architecture;
- security, authentication, or authorization;
- destructive or difficult-to-reverse data changes;
- financial correctness or irreversible external actions;
- difficult concurrency or distributed state;
- large changes affecting several systems;
- repeated failed checks without a clear cause;
- decisions whose mistakes would affect many later workers;
- an explicit request for maximum-quality reasoning.

So the system does not depend only on Luna saying, “I think I can handle this.”

## Parallel research, controlled implementation

Like Sol Advisor Work, Luna Advisor Work can ask several agents to investigate independent parts of a problem at the same time.

```text
Research:        Scout A ─┐
                 Scout B ─┼──► Luna combines findings
                 Scout C ─┘

Implementation:             ► One writer ► Luna verifies
```

Parallel work is useful for reading documents, exploring repositories, comparing alternatives, collecting evidence, or finding missing tests.

For changes to shared files or artifacts, Luna Advisor Work normally prefers **one writer at a time** so agents do not overwrite or contradict each other.

## Recommended path for a difficult task

```text
Luna coordinates
      ↓
Parallel research if useful
      ↓
Sol / High solves the difficult decision
      ↓
Terra / Medium or High implements the plan
      ↓
Luna verifies the result
      ↓
Fresh Sol reviews if the outcome is critical
```

This is the core philosophy of Luna Advisor Work: **cheap coordination, strong implementation, frontier reasoning only when needed.**

## Designed for ChatGPT Work

Luna Advisor Work is designed around **ChatGPT Work hosted subagents** rather than local Codex custom-agent files.

It focuses on:

- choosing the right model for the shape of the task;
- keeping everyday coordination inexpensive;
- parallel research and exploration;
- escalating difficult reasoning to Sol;
- using Terra as the main implementation workhorse;
- keeping shared-state changes controlled;
- verifying worker claims instead of blindly trusting them;
- independent review for critical outcomes.

It does not claim per-agent sandbox isolation or hard model guarantees unless Work actually exposes that evidence.

## Luna Advisor Work vs. Sol Advisor Work

Both projects use the same family of models, but they optimize for different priorities.

| | Luna Advisor Work | Sol Advisor Work |
|---|---|---|
| Main coordinator | Luna | Sol |
| Main priority | Efficiency | Maximum quality |
| Simple work | Luna | Luna when delegated |
| Medium implementation | Terra | Terra when delegated |
| Complex reasoning | Escalate to Sol | Sol already leads |
| Critical review | Fresh Sol | Fresh Sol |
| Best fit | Frequent everyday workflows | Important or difficult workflows |

A simple way to choose:

**Use Luna Advisor Work when efficiency matters most.**  
**Use Sol Advisor Work when maximum confidence matters most.**

## For technical users

The public README intentionally keeps the explanation simple. The exact routing policy, mandatory escalation rules, worker contracts, verification behavior, and Work-specific safeguards live in:

- `skills/orchestration/SKILL.md`
- `skills/orchestration/references/role-contracts.md`
- `skills/orchestration/references/operations.md`

## Attribution

Luna Advisor Work is structurally inspired by [DannyMac180/sol-advisor](https://github.com/DannyMac180/sol-advisor), created by Daniel McAteer and distributed under the MIT License. This Work-native adaptation is maintained separately.
