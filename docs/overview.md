# Overview

UltiCore is a self-hosted platform for human-agent collaboration, built on Ubuntu Server. It connects Linux accounts, agent runtimes, Slack, browser computers, development tools, project files, credentials, and automation into a shared working environment for people and AI agents.

It builds on projects including Hermes Agent for autonomous work, Infisical for credentials, and Xpra for browser access. UltiCore adds account provisioning, shared project structure, task coordination, context management, computer-use controls, and a dashboard for operating the system. People and agents work on the same projects through separate Linux accounts with role-appropriate permissions.

The organization using an installation is configured separately from UltiCore itself. Its name, description, and internal workspace folder come from `/server/organization.json`, managed by `setup organization`. Reusable tools and documentation should not assume a particular organization, person, or hostname.

## Accounts and Interfaces

Each account holds one role: UltiBoss, UltiDev, UltiAgent, or UltiUser. An UltiBoss administers the machine. UltiDevs and UltiAgents work in shared development areas without general administrative authority. UltiUsers receive narrower access and explicit grants for additional paths or commands.

The [security model](security-model.md) explains the distinction between filesystem permission and the context supplied to a runtime. A short instruction file does not make an account a security sandbox.

People can use a terminal, a remote editor, their chosen coding CLI, or UltiConsole. Autonomous agents use the same files and commands through their own accounts. The `ulticonsole` command opens the dashboard. Tasks and Files are available to all roles; additional server and agent controls depend on the signed-in account.

UltiConsole's Computers interface provides access to authorized server browser sessions and account files. Access to another account's computer depends on role and target account. The shared computer is communal; it should be treated as shared working state.

## Where Things Live

| Path | Purpose |
|---|---|
| `/server/docs` | Explanations of the system and its operating procedures |
| `/server/tools` | Custom commands available through `PATH` |
| `/server/scripts` | Implementation helpers, including narrowly authorized privileged operations |
| `/agents/skills` | Shared task-specific guidance and supporting code |
| `/agents/coordination` | Agent inventory and runtime coordination |
| `/workspace/files/organizations` | Client and partner project working files |
| `/workspace/files/<organization-folder>` | The configured organization's internal projects |
| `/workspace/files/meetings` | Meeting sources and related intake work |
| `/workspace/tasks` | Shared task records |
| `/repos` | Code repositories and working copies |
| `/data` | Storage selected and configured for the installation |
| `/home/<account>` | Personal configuration, runtime state, and private account files |

Every account can read and write shared working files in `/workspace`. Restricted work and credentials belong elsewhere. Code belongs in `/repos`; project plans, review candidates, and evidence belong in the owning workspace project.

On a trusted account, `files` builds the documented directory map from folder READMEs. `files all` expands collapsed entries, and `files current` explores the current tree. `docs` lists operational documentation. These commands report the actual installation rather than a fixed inventory in a guide.

## How Work Moves

Read a project's `README.md` or `CONTEXT.md` before adding files. Use [UltiScrum](ultiscrum.md) when work crosses accounts. The task names its owner and next actor, links the relevant material, and records handoffs and outcomes on one timeline.

The [project workflow](project-workflow.md) places incoming material in `intake/`, approaches in `plans/`, review candidates in `review/`, and retained outputs in `artifacts/`. Session summaries preserve a useful handoff while raw conversations remain private.

## Instructions and Commands

Human accounts receive `~/ULTICORE.md`; autonomous agents receive mission-specific runtime instructions. Shared skills hold narrow procedures and load when needed. Operational docs explain why those procedures exist. See [Context Management](context-management.md).

Custom commands encode provisioning, permissions, change tracking, and recovery conventions. Use a provided command when it covers the action. `commands` lists the commands visible to the account, and `<command> help` explains its arguments.

For an existing host, continue with [getting started](getting-started.md). For the maintenance and recovery model, read [operations](operations.md).
