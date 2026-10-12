# Glossary

| Term | Meaning |
|---|---|
| User account | A Linux account for a person or autonomous agent, with one UltiCore role |
| UltiBoss | An administrator in the `sudo` group |
| UltiDev | A human developer with shared development access and no general sudo authority |
| UltiAgent | An autonomous agent account with mission-specific context and no general sudo authority |
| UltiUser | An account scoped to its home, shared workspace, and explicitly granted paths and commands |
| `ultitrusted` | The permission group containing UltiBosses, UltiDevs, and UltiAgents; separate from a role |
| Capability grant | Permission to use a particular path or operation without changing an account's role |
| Tailnet | The private Tailscale network used to reach an installation |
| UltiConsole | The browser interface for tasks, files, computers, and role-appropriate system controls |
| UltiScrum | The shared task workflow with six statuses, one owner, and an explicit next actor |
| Owner | The account responsible for a task |
| Next actor | The account whose action is currently needed; it can differ from the owner |
| Handoff | A transfer of responsibility on the same task and timeline |
| Task note | A passive timeline update that does not change responsibility or wake an agent |
| Review candidate | A file or folder waiting for a decision in the project's `review/` directory |
| Artifact | A retained output or evidence file in its owning project |
| Project tag | The workspace project identity attached to work |
| Session summary | A portable handoff derived from an eligible conversation or task outcome |
| Hermes | The external agent runtime used by UltiAgents |
| Gateway | The runtime's persistent messaging process |
| `ULTICORE.md` | A human account's generated orientation and preserved personal customization |
| `SOUL.md` | An UltiAgent's mission and runtime-global instructions |
| `AGENTS.md` | A coding instruction filename; repository copies describe how to work in that repository |
| Skill | A `SKILL.md` workflow and its supporting resources |
| Builder heuristics | The ten prioritized guidelines used when building UltiCore |
| Computer use | Server browser sessions with programmatic controls and optional live operator access |
| Auth seed | Saved browser state used to initialize later sessions; it contains sensitive login data |
| Environment injection | Supplying credentials to a process that needs them; that process can read the values |
| Managed tree | Configuration and documentation maintained in a local Git history |
| Bare hub | A project Git repository used as a local remote without checked-out working files |
| Guarded upgrade | An update routed through the dependency review and application workflow |
| Private Git snapshot | A recovery export of selected committed files to a private remote repository |

Read the [overview](overview.md) for the system as a whole, the [security model](security-model.md) for permissions, and [UltiScrum](ultiscrum.md) for task behavior.
