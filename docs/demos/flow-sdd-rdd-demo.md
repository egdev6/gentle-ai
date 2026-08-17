# Flow + SDD + RDD demo

This demo explains Flow as the operational layer around SDD and RDD. The live target is the separate `Stack-and-Flow/design-system` project and its GitHub Project board. This repository contains only the concept docs, guide, and simulated fixture contract.

## Quick path

1. Open the Flow concept: [`../concepts/flow.md`](../concepts/flow.md).
2. Open the illustrative contract: [`fixtures/github-project-task-flow.yaml`](fixtures/github-project-task-flow.yaml).
3. Walk through how one clearly marked demo issue moves through SDD phase hooks.
4. Finish by showing where RDD begins: after a completed candidate exists, with exact bytes frozen and receipt gates handled by RDD, not Flow.

## Demo promise

The demo should prove one narrow idea:

> Flow can coordinate operational evidence around SDD work and preserve useful context for RDD without replacing either system.

## Safety boundaries

| Area            | Demo rule                                                                        |
| --------------- | -------------------------------------------------------------------------------- |
| Live repository | Use `Stack-and-Flow/design-system` only for the live target.                     |
| This repository | Docs and simulated fixtures only. No live GitHub mutation from this repo.        |
| Demo issue      | Use a clearly marked demo issue, for example `[Flow demo] Button token cleanup`. |
| GitHub Project  | Use a safe demo item or sandbox project area. Do not move real roadmap work.     |
| RDD             | Do not claim RDD approval until the actual RDD lifecycle emits a receipt.        |

## Narrative

### 1. Start with the concept

Explain the distinction:

- Skill = knowledge, rules, criteria, and examples.
- Flow = repeatable process with state, steps, gates, artifacts, evidence, verification, delegation, and optional SDD/RDD hooks.

Then name the boundary: Flow v0 is a structured checklist plus evidence contract. It is not a new authority system.

### 2. Show the fixture contract

Open `docs/demos/fixtures/github-project-task-flow.yaml` and point to four parts:

| Contract part   | What to show                                                                 |
| --------------- | ---------------------------------------------------------------------------- |
| `scope`         | The live target is external; this repo only stores the simulated contract.   |
| `state`         | The operation has visible progress states.                                   |
| `steps`         | Each SDD phase hook has an expected action and evidence.                     |
| `verification`  | A checker verifies board state and evidence; it does not perform RDD review. |

### 3. Walk through the SDD angle

Use a clearly marked demo issue in `design-system` and narrate the Flow hooks around a normal SDD run.

| SDD phase       | Flow action                                                                     | Expected evidence                                   |
| --------------- | ------------------------------------------------------------------------------- | --------------------------------------------------- |
| Tasks           | Ensure or sync the GitHub Project item for the demo issue.                      | Issue URL, project item identifier, planned status. |
| Apply           | Move the item to `In Progress` when implementation starts.                      | Before/after board status snapshot.                 |
| Verify          | Check that the board state matches the implemented state and recorded evidence. | Verification note with query result and status.     |
| Archive or sync | Move the item to final status or close/update the issue.                        | Final board status, issue status, archive note.     |

The important point: SDD still owns requirements, design, implementation tasks, and verification against the spec. Flow only coordinates the external operational evidence.

### 4. Walk through the RDD angle

After the candidate is complete in the live project, explain where RDD starts:

1. A candidate exists.
2. RDD freezes the exact candidate bytes.
3. RDD classifies risk from evidence.
4. RDD selects zero, one, or four lenses.
5. RDD finalization emits a receipt only if the lifecycle approves.
6. Delivery gates reuse that receipt.

Flow can provide context such as the demo issue, project item, SDD phase evidence, and external board snapshots. Flow never approves the candidate and never mints the receipt.

## Expected evidence

For a successful demo, collect evidence like this:

| Evidence                                             | Source                                              | Why it matters                                      |
| ---------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| Flow contract                                        | `docs/demos/fixtures/github-project-task-flow.yaml` | Shows the planned operational checklist.            |
| Demo issue link                                      | `design-system` GitHub issue                        | Ties the operation to a visible external work item. |
| Project item before/after                            | GitHub Project board snapshot or query output       | Shows operational state changed as expected.        |
| SDD task/apply/verify notes                          | SDD artifacts or session transcript                 | Shows Flow hooks aligned with SDD phases.           |
| RDD receipt or gate output, if enabled and completed | Gentle AI RDD lifecycle output                      | Shows RDD authority separately from Flow.           |

## Suggested talk track

```text
This is not a new review system. Flow records how an operation should move and what evidence it should leave behind.

SDD still decides what we are building and whether the implementation matches the spec.
RDD still starts only after a candidate exists, freezes exact bytes, and owns receipt-based delivery gates.
Flow sits beside them: it keeps the GitHub Project task synchronized and makes the evidence easy to verify.
```

## What not to claim

- Do not claim Flow replaces SDD, RDD, agents, chains, or review authority.
- Do not claim the fixture is a stable public runtime schema.
- Do not claim the demo issue is production workflow automation.
- Do not claim board-state verification is content approval.
- Do not claim RDD approval unless a real RDD receipt was emitted for the exact candidate.
- Do not mutate live project data from this repository.

## Reset after the live demo

If the live demo changes a sandbox GitHub Project item, return it to the agreed demo state or close the clearly marked demo issue. Record any remaining state in the demo notes so future runs start from a known baseline.
