# Project workflow

A project folder holds the shared context needed to continue work: received material, plans, review candidates, retained results and conversation summaries. Read its `README.md` or `CONTEXT.md` before adding files or structure.

UltiCore uses two project roots:

```text
/workspace/files/organizations/<project>/
/workspace/files/<organization-folder>/<project>/
```

The first holds client and partner work. The second holds internal projects under the organization folder configured during setup. `setup organization show` displays that configuration. Code repositories live under `/repos`; their plans, review evidence and working context belong in the related workspace project.

Every account, including an UltiUser, can read and write the shared workspace. A project folder is not a private access boundary. Keep credentials and material requiring restricted access outside it; see the [security model](security-model.md).

## The project folders

Creating a project through UltiConsole Files creates these base folders. The dashboard protects the folders from renaming, moving and deletion while allowing their contents to change.

| Folder | What belongs there |
|---|---|
| `intake/` | Original material received from a client or another source |
| `plans/` | Proposed or active approaches |
| `review/` | Candidates awaiting a human decision |
| `artifacts/` | Approved or retained outputs and evidence |
| `logbook/` | Dated records of work, changes and decisions |
| `sessions/hermes/` | Handoffs derived from UltiAgent task outcomes |
| `sessions/claude/` | Shared summaries of eligible Claude Code conversations |
| `sessions/codex/` | Shared summaries of eligible Codex conversations |

Work commonly moves from intake through planning and review to retained artifacts. For example, an `example-project` folder might receive a brief in `intake/`, develop a proposal in `plans/`, and move the candidate to `review/` for a decision. After acceptance, the final proposal belongs in `artifacts/`. The logbook records the decision; its task links to the result.

Use `review FILE [PROJECT]` to move a candidate into review. Pair that file move with `task review` or `task finish` for tracked work. The file move and task transition are separate actions. After acceptance, move the retained result to `artifacts/` or its permanent project location and update the evidence reference. The [UltiScrum guide](ultiscrum.md) shows a complete example.

UltiConsole Files exposes `/workspace/files`. Keep deliverables there and link them from task records under `/workspace/tasks` through `context` or `evidence`.

## Start the conversation in its project

The nightly publisher routes a human conversation by the initial working directory recorded by its coding tool. Start Claude Code or Codex inside the direct project folder, or one of its subfolders:

```bash
cd /workspace/files/organizations/example-project
codex
```

The same routing rule applies to `claude`. Starting in a repository under `/repos`, a home directory or another location does not qualify, even if a later turn changes directory into the workspace project. Leave an explicit handoff in the project for that work. An UltiAgent's work gets its project from the task's `project` field.

## What the nightly summaries contain

The nightly workflow publishes eligible handoffs into the three `sessions/` folders. Hermes summaries come from project-tagged task records with an outcome, including finished work awaiting acceptance `In Review`. This path reads task records and does not summarize Hermes transcripts through another model.

For human Claude Code and Codex sessions, a worker running as the owning account reconstructs the active conversation. It retains visible user and assistant prose and excludes instructions, reasoning, tool traffic, attachments and child-agent conversations. Credential-pattern redaction runs before the worker sends the bounded text to the same runtime provider under that account's login. There is no fallback to another provider. The result is validated and redacted again before publication.

Raw transcripts remain private in the owning account's home directory. Published summaries are shared workspace material. Redaction cannot guarantee removal of every sensitive statement, so conversations started in project folders must be suitable for that audience and must not contain credentials.

Later publications update a source's existing summary when it changes. For human sessions, matching copies inside the routed project are refreshed together. A valid rewind or revert that removes all retained visible user turns replaces existing matching summaries there with a content-free tombstone. Copies exported outside that project remain outside publisher control.

A summary records its source conversation or task outcome. It does not freeze the project files or guarantee that a reported check still holds. Before continuing, read the current files and task state. Before stopping, leave a handoff with the outcome, verification performed, unresolved decisions and exact artifact paths.
