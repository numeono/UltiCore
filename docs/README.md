# Documentation

These guides describe UltiCore's current operating model. Start with the overview, then follow the part of the system relevant to the work.

| Guide | What it explains |
|---|---|
| [Overview](overview.md) | How accounts, commands, project files, and the dashboard fit together |
| [Security model](security-model.md) | Roles, permissions, network access, credentials, and their limits |
| [UltiScrum](ultiscrum.md) | Task ownership, status, handoffs, review, and closure |
| [Project workflow](project-workflow.md) | Project folders, artifacts, and portable session summaries |
| [Agent runtime and lifecycle](agent-runtime.md) | Agent accounts, Hermes, gateways, jobs, and delegation |
| [Computer use](computer-use.md) | Server browsers, control channels, saved state, and live access |
| [Context management](context-management.md) | Instruction files, skills, and the context supplied to each runtime |
| [Operations and recovery](operations.md) | Change history, repository mirroring, maintenance, backups, and restores |
| [Getting started](getting-started.md) | Onboarding to an existing installation and preparing for deployment |
| [Builder heuristics](builder-heuristics.md) | The prioritized rules used to build UltiCore |
| [Glossary](glossary.md) | Roles and terms used throughout the guides |

## Scope and sources

Prepared from the refreshed operational documentation on October 12, 2026. The guides adapt reusable explanations for a public reader. They exclude personal instruction customizations, live account inventories, organization working files, dated session records, and this installation's hardware inventory.

The source documents on an installed server are grouped below. These are server paths, not files shipped in this preview.

| Public guide | Operational sources under `/server/docs/` |
|---|---|
| Overview | `ulticore-overview.md`, `server-architecture.md` |
| Security model | `ulticore-overview.md`, `networking-and-security.md`, `infisical-and-secrets.md`, `installation-request-system.md` |
| UltiScrum and project workflow | `tasks.md`, `reviews.md`, `project-workflow.md`, `project-session-summaries.md` |
| Agent runtime | `managing-agents.md`, `skill-architecture.md` |
| Computer use | `computer-use-stack.md`, `setup/initial-server-setup/computer-use-setup.md` |
| Context management | `ulticore-overview.md`, `server-architecture.md`, `skill-architecture.md`, `skill-code-secrets-and-data.md`, `managing-agents.md` |
| Operations and recovery | `git-and-backup.md`, `repo-hosting-and-mirroring.md`, `maintenance-and-upgrades.md`, `resource-warning-system.md` |
| Getting started | `setup/initial-server-setup/`, `setup/new-user/`, and current command help |
| Builder heuristics and glossary | `builder-heuristics.md`, `glossary.md` |

Commands in these guides assume an installed UltiCore host and the required account permissions. Run a command's `help` to inspect the version present on that host. The [repository README](../README.md#development-status) records the public release's current scope and outstanding validation.
