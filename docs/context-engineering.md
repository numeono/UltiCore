# Context engineering

UltiCore separates instructions that apply to every session from procedures needed for a particular job and evidence belonging to a project. An agent should know its responsibilities before it starts, then read the relevant procedure and source material when the task requires them.

Ordinary files and runtime instruction mechanisms provide that context. A short prompt does not create a permission boundary.

## Account instructions

Humans have `~/ULTICORE.md`. Its generated region supplies organization context and the orientation appropriate to the account's role. UltiDevs and UltiBosses receive the broad overview and command index, with the builder heuristics when opted in. UltiUsers receive a narrower orientation and their grants.

The personal region survives regeneration, apart from managed status blocks. Human Claude Code and Codex accounts point their global instruction files at this source. Repository-specific instructions describe how to work on that project.

An UltiAgent has `~/.hermes/SOUL.md`. The authored portion defines its mission and enduring responsibilities. A managed region supplies its role, operating rules, workspace guidance, commands and reference indexes. It gives Hermes enough orientation to find more information without placing the entire server manual in every prompt.

Claude on an UltiAgent account points at that same instruction file. Delegated Codex workers do not receive an account-level copy of it; their task brief and repository instructions must provide the context they need. A parent should therefore pass the objective, permitted scope, useful source paths and expected result explicitly.

`sync-agents` maintains generated instruction regions from their source documents and command descriptions. Edit the source for a shared rule, the authored mission for an agent-specific rule, or the personal region for an individual's preference. Editing generated prose directly produces a change that the next sync can overwrite.

Runtime session state is separate from file state. Hermes reads instructions when it constructs the session prompt and again during compaction. Saving a mission change does not immediately replace the prompt in an existing conversation. A fresh session is the reliable way to apply it at once.

## Procedures loaded when needed

Shared skills live at `/agents/skills/<category>/<skill>/SKILL.md`. A skill contains a focused procedure, with reusable helper code beside it where necessary. Documentation under `/server/docs` explains the system and why the procedure exists.

Human runtime directories link to the shared library. Hermes can expose a selected set through links in `~/.hermes/skills/`, or the entire library through its external-directory configuration. Provisioning starts with a core baseline; additional skills are selected for the mission.

Hermes initially loads skill names and descriptions, allowing it to identify the relevant procedure without loading every body. Inspect the runtime's effective list with `hermes skills list`. A separate handwritten catalogue would create another description of the same state to maintain.

Skill selection controls discovery, not Linux access. An agent with a small selected set may still have permission to read and edit shared files. The [security model](security-model.md) governs that access.

| Information | Home |
|---|---|
| Enduring agent mission | Authored `SOUL.md` content |
| Shared operating rules | Source documents and generated instruction regions |
| Reusable procedure or helper | Shared skill library |
| Assignment, current owner and outcome | UltiScrum task |
| Project sources and deliverables | Project folders under `/workspace/files` |
| Operational logs and caches | The invoking account's private state directory |
| Credential values | Managed credential storage, outside instructions and projects |

Run logs remain separate from reusable instructions, and project evidence stays out of unrelated startup prompts.

## Task context and portable handoffs

An UltiScrum task holds the assignment and links to supporting context or evidence. Artifacts stay in the project. A handoff preserves the task and its timeline, so the next owner can read the request, decisions and result together. See [project workflow](project-workflow.md) for the folder structure.

Nightly project summaries make completed work discoverable across runtimes. Hermes summaries come from project-tagged task outcomes, without reading private Hermes transcripts or asking a second model to reinterpret them. Work awaiting acceptance can already have a summary, which records its current review state.

Human Claude Code and Codex summaries follow a different path. The publisher selects sessions whose initial recorded working directory belongs to a direct project folder. Starting elsewhere does not become eligible merely because a later message mentions a project or a later command changes directory.

A worker running as the owner retains visible user and assistant prose from the active conversation. It excludes system instructions, reasoning, tool traffic, attachments and child-agent conversations. Credential-pattern redaction precedes a bounded summary request through the same runtime and account. Results are validated and redacted again before publication.

Summaries go into `sessions/hermes/`, `sessions/claude/` or `sessions/codex/` under the project. Raw transcripts stay in private account storage. A failed human summary request leaves its existing routed summary unchanged, and unchanged source content is not summarized again.

Project summaries are readable by everyone with workspace access. Automated redaction cannot guarantee removal of every sensitive statement, so visible project conversations and task outcomes must still suit that audience. The summary preserves useful decisions and next steps; credentials and private runtime state remain outside shared context.
