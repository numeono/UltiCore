> Development status: UltiCore's first public alpha is expected to be pushed to this repository by the end of this week, Sunday, October 18, 2026. This repository currently contains documentation and visual assets; source code and an installation package are not available yet. Source export review, clean-install testing, and restore testing are still pending. See [Development Status](#development-status).

<p align="center">
  <img src="assets/ulticore-banner.svg?v=lt-clear-gap" alt="UltiCore infrastructure for human-agent collaboration" width="1200" />
</p>

# UltiCore

UltiCore is a self-hosted platform for human-agent collaboration that integrates with your existing tools. UltiCore installs on your own hardware on top of Ubuntu Server and gives you autonomous agents that write code, run their own computers, and work alongside your team through Slack. You get shared project workspaces, task assignment and review, reusable skills, context management across sessions, scheduled automation, and live computer sessions you can join and control. Role-based accounts, centralized credentials, version control, backups, and a dashboard bring the whole environment under your team's management.

Assign a task in chat. Let an agent work on its computer. Join its live computer session when it needs your help, then review the result in the same project. Files, task history, and recorded project context stay available for whoever picks up the work next.

Underneath, UltiCore brings Ubuntu, Hermes Agent, Infisical, Xpra, and other open-source projects into one managed environment. It connects the operating system to agent runtimes, Slack, GitHub, credentials, computers, and automation, then adds the pieces a human-agent team needs: shared projects, lightweight task handoffs, context management, interactive computer use, and a central dashboard.

Your server. Your choice of models. A workspace your whole team can build on.

## Give Your Agents a Place to Work

Each autonomous agent has its own Linux account, mission, selected skills, computer with saved logins, and configured service access. Agents can receive work through Slack, run scheduled routines, or pick up actionable tasks. Their files and runtime state persist between conversations, and you manage their access and lifecycle on your own infrastructure.

UltiConsole brings the team into one browser interface: tasks, project files, agent settings, jobs, automations, server health, and computers. Developers can also work through SSH, a remote editor, Claude Code, Codex, or the command line.

Read [Agent Runtime](docs/agent-runtime.md) and [Getting Started](docs/getting-started.md).

## Move Work Between Humans and Agents

People and agents share project files, reusable skills, and an explicit workflow for handing work to each other. A developer can prepare a plan, an agent can implement it, and a person can review the result in the same project. Each participant has a separate account with permissions appropriate to their role.

UltiScrum keeps coordination small: six statuses, one task owner, an explicit next actor, and a timeline that survives handoffs. Tasks link to the plans, review candidates, and deliverables they concern. Work requested by another human returns to that person for acceptance.

Read [UltiScrum](docs/ultiscrum.md), [Project Workflow](docs/project-workflow.md), and the [Security Model](docs/security-model.md).

## Join Your Agent on Its Computer

Agents run their own computers with saved logins. UltiCore combines DOM controls with mouse, keyboard, and clipboard operations so an agent can move between ordinary web forms, visual interfaces, and canvas-based editors. File uploads, screenshots, session recording, and a separate demo workflow are part of the same toolset.

When a task needs a person, open an authorized live portal to see the same computer and take control. Complete a login or approval, inspect the result, then let the agent continue. The computer session provides a shared place to work through steps that cannot be completed through an API alone.

Read [Computer Use](docs/computer-use.md).

## Context Management Across Sessions

A team's knowledge should survive the conversation that produced it. UltiCore separates account instructions, reusable skills, project source material, and task outcomes so each has a place to live and a way to be found.

Project folders collect plans, evidence, and retained results. Nightly automation creates portable handoffs from agent task outcomes and redacted excerpts of eligible human coding sessions. Handoff generation runs locally without model or API calls; raw transcripts remain private. People and agents can pick up the project's recorded context in a later session or another tool.

Read [Context Management](docs/context-management.md).

## Built on Open-Source Foundations

UltiCore integrates existing projects and adds the workflows that connect them.

| Foundation | Its Role in UltiCore |
|---|---|
| Ubuntu Server and Linux accounts | The host operating system, file ownership, and role permissions |
| [Hermes Agent](https://github.com/NousResearch/hermes-agent) | Agent execution, messaging gateways, scheduling, skills, and delegation |
| [Infisical](https://github.com/Infisical/infisical) | Central credential storage and injection into authorized processes |
| [Xpra](https://github.com/Xpra-org/xpra) and Chromium | Agent computers and live remote access |
| Git | Source collaboration and managed configuration history |
| restic | Encrypted backups governed by the installation's recovery policy |
| systemd | Services, scheduled system work, and process lifecycle management |

UltiCore connects these foundations to Slack, GitHub, coding tools, and the services your agents need. You host the workspace and agent processes, choose their model providers, and configure access to connected services.

## Operations Built Into the Workspace

Provision accounts and agents through role-aware commands. Manage credentials centrally, record shared changes, inspect failed jobs, and review software updates from the same environment where the team works. Backups and recovery procedures cover the operational side of keeping a shared server useful.

Read [Operations and Recovery](docs/operations.md) and the [Builder Heuristics](docs/builder-heuristics.md) behind the design.

## Development Status

UltiCore's first public alpha and open-source release are expected to be pushed to this repository by Sunday, October 18, 2026. This repository currently contains documentation and visual assets describing the running system. The source distribution and a reproducible installation package are not included yet.

Before publishing the source distribution, the actual export still needs review, clean-install testing, and restore testing. Publishing these guides does not establish that those release checks have passed.

Start with the [Overview](docs/overview.md), browse the [Documentation Index](docs/README.md), or watch the repository for release updates.
