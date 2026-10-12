# UltiScrum

Most task management systems are needlessly complex. UltiScrum is optimized for lean teams, with only the essentials: who owns the work, whose action is needed next, where the context lives, and what happened. Humans and agents use the same task record throughout the work.

UltiScrum is part of UltiCore. The `task` command and the Tasks tab in UltiConsole read and update the same records under `/workspace/tasks`. Each task has one owner and one timeline. Every live task waits on one account until someone passes it on or closes it.

## Six Statuses

| Status | Meaning | Whose action is needed |
|---|---|---|
| `Open` | Assigned, but not started | Owner |
| `In Progress` | Work is underway | Owner |
| `Blocked` | Work needs a recorded answer, decision or dependency | Named person who can unblock it; the requester by default |
| `In Review` | A result awaits acceptance or further direction | Requester |
| `Implemented` | Completed, with an outcome recorded | Nobody |
| `Canceled` | Deliberately stopped, with a reason recorded | Nobody |

Reading a task does not change its status. Tasks do not expire. Unstarted and blocked work stays visible until someone acts on it, and terminal records remain available with their outcomes and evidence.

## Owner, Requester and Next Action

The owner does the work. The requester put the work in front of that owner: the original sender, or the author of the latest handoff. The next actor is the account whose action is currently needed. Blocking a task or requesting review changes the next actor while keeping its owner.

When an owner finishes work requested by another human account, `task finish` sends it to that requester `In Review`. The requester accepts the result or returns it for changes. The owner remains recorded as the person or agent who did the work; acceptance records who closed it.

Work requested by an agent, and work assigned to oneself, goes directly to `Implemented` on finish. Use `task review` to ask the requester for a decision explicitly when automatic review would not apply.

A handoff transfers the same task to a new owner and queue, resets it to `Open`, and preserves its ID, context and timeline. The handoff author becomes its requester. Use a new task for new work on a subject that already has a completed task, and link the earlier result as context.

## A Short Workflow

These commands run on a configured UltiCore installation. Replace `WORKER` with an account name and `TASK_ID` with the ID returned by `task send`. The example project and its folders must already exist. `task help` lists the installed command's full syntax.

The requester assigns work with enough context to begin:

```bash
task send WORKER "Prepare the deployment plan for review." \
  title "Prepare deployment plan" \
  description "Document the steps, checks and rollback." \
  project files/organizations/example-project \
  context /workspace/files/organizations/example-project/plans
```

The worker reads the queue and claims the task from their own account:

```bash
task receive WORKER
task claim WORKER TASK_ID
```

When the candidate is ready, the worker moves it into project review and records the outcome:

```bash
review /workspace/files/organizations/example-project/plans/deployment-plan.md
task finish WORKER TASK_ID "Prepared the deployment plan for review." \
  evidence /workspace/files/organizations/example-project/review/deployment-plan.md
```

`review` infers the project from this source path and moves the file rather than copying it. It refuses to overwrite an existing candidate. The project folder contains the result, and the task contains the decision waiting on the reviewer.

From the human requester's account, either return the task with a specific change or accept it:

```bash
task resume WORKER TASK_ID "Add the rollback checks before acceptance."
```

Or, after reviewing and moving the accepted file to `artifacts/`:

```bash
task accept WORKER TASK_ID "Accepted the deployment plan." \
  evidence /workspace/files/organizations/example-project/artifacts/deployment-plan.md
```

Acceptance does not move the file for you. The task's evidence should point to the retained result. For a return, `task resume` puts the task back `In Progress` with the same owner and the reviewer's note on its timeline.

## Blockers, Handoffs and Notes

Name what is missing and who can provide it:

```bash
task block WORKER TASK_ID "Need the approved maintenance window." on REVIEWER
```

The named person can answer with `task resume`. The requester, owner or a coordination moderator can also resume blocked work. Without `on REVIEWER`, the task waits on its requester.

Transfer work when a different account should own it:

```bash
task handoff WORKER TASK_ID NEXT_OWNER "Continue from the linked plan."
```

Subsequent commands use `NEXT_OWNER` as the queue, with the same task ID. Terminal work cannot be handed off.

Add context without changing the workflow:

```bash
task note NEXT_OWNER TASK_ID "The plan now includes the test results."
```

A note is a passive timeline entry. It changes no status, owner or next actor, and wakes no agent. Notes work on both live and terminal tasks. Record an outcome with `finish`, a dependency with `block`, and additional context with `note`.

## Following the Work

`task check` lists everything waiting on your action, including reviews and blockers. UltiConsole's My Tasks starts from the same set. Waiting on Others shows work you requested or transferred that needs someone else's action; Everyone includes the team's terminal records too. The task panel shows context, evidence, next steps and the timeline.

For an UltiAgent with its task trigger enabled, a new actionable task starts a fresh Hermes turn. Resuming its task can start another turn. Provisioning installs the trigger but leaves it disabled until an operator enables it. Humans read their tasks on demand. See [agent runtime](agent-runtime.md).

Tasks hold coordination records. Plans, review candidates and deliverables belong in their [project folders](project-workflow.md), linked through `context` or `evidence`. A file alone assigns no work, and an In Review task needs a reference that tells its reviewer what to inspect.

Every account can read and write the shared workspace, including task files. Command checks enforce the intended workflow but are not a security boundary against direct filesystem writes. Keep credentials and material requiring narrower access elsewhere; see the [security model](security-model.md).
