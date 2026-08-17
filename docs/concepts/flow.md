# Flow

Flow is Gentle AI's name for a repeatable operational process: the checklist, state, gates, artifacts, evidence, verification, delegation points, and optional SDD/RDD hooks that help a team run the same work safely more than once.

A Skill teaches an agent what good looks like. A Flow tells the agent how to move work through an operation and prove what happened.

## Quick path

1. Use a Skill when the problem is mostly judgment, rules, or quality criteria.
2. Use a Flow when the work has state, handoffs, gates, or external evidence to keep synchronized.
3. Keep Flow v0 small: a structured checklist, optional SDD hooks, and final evidence. Do not turn it into a new authority system.

## Skill versus Flow

| Concept   | Owns                                                                            | Example                                                                                    |
| --------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Skill     | Knowledge, rules, heuristics, examples, and acceptance criteria.                | "Write reviewable docs", "apply repository conventions", "avoid dangerous commands".       |
| Flow      | Operational state, ordered steps, gates, artifacts, evidence, and verification. | "Keep a GitHub Project item synchronized while an SDD change moves from tasks to archive". |

A Skill can be used inside a Flow. A Flow can require several Skills. They solve different problems.

## What Flow is

A Flow is useful when the operation has more to coordinate than a single prompt can safely remember:

- state transitions, such as `planned -> in_progress -> verified -> done`
- step ownership, including agent delegation or human-controlled checkpoints
- gates that decide whether the next step is allowed
- artifacts that should exist at specific points
- evidence that proves an external system, board, issue, or repository state changed as expected
- verification that checks the operational outcome
- optional hooks into SDD phases or RDD lifecycle moments

## What Flow is not

Flow must not replace existing Gentle AI control planes.

| Boundary         | Flow may do                                                                  | Flow must not do                                                                                    |
| ---------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| SDD              | Provide operational hooks around proposal, tasks, apply, verify, or archive. | Replace proposal/spec/design/tasks, invent requirements, or mark implementation complete by itself. |
| RDD              | Provide context and evidence that can accompany a completed candidate.       | Approve content, classify review risk, select lenses, mint receipts, or satisfy delivery gates.     |
| Agents           | Describe which operation needs delegation or verification.                   | Become a new agent scheduler or bypass the orchestrator's routing rules.                            |
| Chains           | Record chain-related operational evidence.                                   | Replace PR chain planning, branch policy, or delivery strategy.                                     |
| Review authority | Preserve evidence for a later review.                                        | Inspect private authority stores, infer approval, or fabricate receipt status.                      |

## Relationship to SDD

SDD owns the product and implementation lifecycle: proposal, specs, design, tasks, apply, verify, and archive. Flow can add operational steps around those phases.

Example: `github-project-task-flow` for an external design-system project.

| SDD phase       | Flow hook                                                                 | Evidence                                             |
| --------------- | ------------------------------------------------------------------------- | ---------------------------------------------------- |
| Tasks           | Ensure or synchronize a GitHub Project item for the selected demo issue.  | Project item identifier, issue URL, intended status. |
| Apply           | Move the item to `In Progress` when implementation starts.                | Before/after status snapshot.                        |
| Verify          | Check that the board state and task evidence match the implemented state. | Query result, status value, linked evidence.         |
| Archive or sync | Close or update the final status after the change is complete.            | Final board status, issue status, archive note.      |

The Flow does not decide whether the implementation satisfies the spec. It only keeps the external operational system honest and observable.

## Relationship to RDD

RDD happens after there is a completed candidate. It freezes exact bytes, classifies risk from evidence, selects zero, one, or four review lenses, emits a receipt when the lifecycle approves, and delivery gates reuse that receipt.

Flow can help RDD by preserving operational context:

- which external issue or project item the candidate claims to affect
- which SDD phase created or verified the evidence
- what external state changed before and after the implementation
- what verification was performed outside the repository

Flow cannot help RDD by approving anything. RDD approval belongs only to the receipt-driven review lifecycle and its gates.

## When to use Flow

Use Flow when at least one of these is true:

- the work spans repository state plus an external system, such as GitHub Projects, an issue tracker, or release notes
- the same operation will be repeated across changes
- evidence must be gathered at several points, not only at the end
- SDD phases need operational side effects or checks
- the team wants a demoable checklist without introducing a new runtime authority

Avoid Flow when a simple Skill, README, or one-off checklist is enough.

## Flow v0 shape

Flow v0 is intentionally small and documentation-first. A Flow v0 contract can be a YAML fixture with:

- `schema` and `name`
- `scope` and safety boundaries
- `state` values
- ordered `steps`
- optional `sdd_hooks`
- optional `rdd_hooks`
- expected `artifacts`
- `verification` checks
- explicit `non_goals`

Flow v0 should be treated as a structured checklist plus evidence contract, not as a stable public runtime schema.

## First pilot

The first demo Flow is `github-project-task-flow`: a simulated contract in this repository that can be used to explain a live demo against the separate `Stack-and-Flow/design-system` GitHub Project.

See [`../demos/flow-sdd-rdd-demo.md`](../demos/flow-sdd-rdd-demo.md) and [`../demos/fixtures/github-project-task-flow.yaml`](../demos/fixtures/github-project-task-flow.yaml).
