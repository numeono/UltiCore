# Glossary

UltiCore-specific names and terms used in its commands and workflows.

| Term | Meaning |
|---|---|
| UltiBoss | An administrator in the `sudo` group |
| UltiDev | A human developer with shared development access and no general sudo authority |
| UltiAgent | An autonomous agent account with mission-specific context and no general sudo authority |
| UltiUser | An account scoped to its home, shared workspace, and explicitly granted paths and commands |
| `ultitrusted` | The permission group containing UltiBosses, UltiDevs, and UltiAgents; separate from a role |
| UltiConsole | The browser interface for tasks, files, computers, and role-appropriate system controls |
| UltiScrum | The shared task workflow with six statuses, one owner, and an explicit next actor |
| Next actor | The account whose action is currently needed; it can differ from the owner |
| Task note | A passive timeline update that does not change responsibility or wake an agent |
| Review candidate | A file or folder waiting for a decision in the project's `review/` directory |
| Project tag | The workspace project identity attached to work |
| `ULTICORE.md` | A human account's generated orientation and preserved personal customization |
| Builder heuristics | The ten prioritized guidelines used when building UltiCore |
| Computer use | UltiCore's term for browser use: agents run their own computers, backed by server-side Chromium sessions with programmatic controls and optional live human access |
| Guarded upgrade | An update routed through the dependency review and application workflow |

Read the [overview](overview.md) for the system as a whole, the [security model](security-model.md) for permissions, and [UltiScrum](ultiscrum.md) for task behavior.
