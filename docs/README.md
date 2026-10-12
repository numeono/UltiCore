# Documentation

These guides describe UltiCore's current operating model. Start with the overview, then follow the part of the system relevant to the work.

| Guide | What it explains |
|---|---|
| [Overview](overview.md) | How accounts, commands, project files, and the dashboard fit together |
| [Security Model](security-model.md) | Roles, permissions, network access, credentials, and their limits |
| [UltiScrum](ultiscrum.md) | Task ownership, status, handoffs, review, and closure |
| [Project Workflow](project-workflow.md) | Project folders, artifacts, and portable session summaries |
| [Agent Runtime and Lifecycle](agent-runtime.md) | Agent accounts, Hermes, gateways, jobs, and delegation |
| [Computer Use](computer-use.md) | Server browsers, control channels, saved state, and live access |
| [Context Management](context-management.md) | Instruction files, skills, and the context supplied to each runtime |
| [Operations and Recovery](operations.md) | Change history, repository mirroring, maintenance, backups, and restores |
| [Getting Started](getting-started.md) | Onboarding to an existing installation and preparing for deployment |
| [Builder Heuristics](builder-heuristics.md) | The prioritized rules used to build UltiCore |
| [Glossary](glossary.md) | Roles and terms used throughout the guides |

## Scope and Sources

Prepared from the refreshed operational documentation on October 12, 2026. The guides adapt reusable explanations for a public reader. They exclude personal instruction customizations, live account inventories, organization working files, dated session records, and this installation's hardware inventory.

The source documents on an installed server are grouped below. These are server paths, not files shipped in this preview.

| Public guide | Operational sources under `/server/docs/` |
|---|---|
| Overview | `ulticore-overview.md`, `server-architecture.md` |
| Security Model | `ulticore-overview.md`, `networking-and-security.md`, `infisical-and-secrets.md`, `installation-request-system.md` |
| UltiScrum and Project Workflow | `tasks.md`, `reviews.md`, `project-workflow.md`, `project-session-summaries.md` |
| Agent Runtime | `managing-agents.md`, `skill-architecture.md` |
| Computer Use | `computer-use-stack.md`, `setup/initial-server-setup/computer-use-setup.md` |
| Context Management | `ulticore-overview.md`, `server-architecture.md`, `skill-architecture.md`, `skill-code-secrets-and-data.md`, `managing-agents.md` |
| Operations and Recovery | `git-and-backup.md`, `repo-hosting-and-mirroring.md`, `maintenance-and-upgrades.md`, `resource-warning-system.md` |
| Getting Started | `setup/initial-server-setup/`, `setup/new-user/`, and current command help |
| Builder Heuristics and Glossary | `builder-heuristics.md`, `glossary.md` |

Commands in these guides assume an installed UltiCore host and the required account permissions. Run a command's `help` to inspect the version present on that host. The [repository README](../README.md#development-status) records the public release's current scope and outstanding validation.
