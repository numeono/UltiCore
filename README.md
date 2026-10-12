<p align="center">
  <img src="assets/ulticore-banner.svg?v=lt-clear-gap" alt="UltiCore infrastructure for human-agent collaboration" width="1200" />
</p>

# UltiCore

UltiCore is self-hosted software that runs on top of Ubuntu Server and turns it into a shared working environment for people and AI agents. It connects the operating system, agent runtimes, Slack, browser computers, development tools, project files, credentials, and automation so humans and agents can work together on the same projects.

Give an agent a role, talk to it in Slack, and let it work with the tools and services you authorize. It can write code, operate websites, run recurring jobs, and pass work to another agent or back to a person for review. Your team can open the same project files, take over a browser session, and continue the work with its context intact.

UltiCore builds on open-source projects including Ubuntu, Hermes Agent, Infisical, and Xpra. It adds the shared workspace, account provisioning, task coordination, browser controls, context management, and administration needed to run them together as a human-agent team.

This repository is a documentation preview ahead of the first public alpha. See [Development Status](#development-status) for release readiness.

## AI Teammates on Your Own Server

Each autonomous agent has its own Linux account, mission, selected skills, browser profile, and configured service access. Agents can receive work through Slack, run scheduled routines, or pick up actionable tasks. Their files and runtime state persist between conversations, and you manage their access and lifecycle on your own infrastructure.

UltiConsole brings the team into one browser interface: tasks, project files, agent settings, jobs, automations, server health, and browser computers. Developers can also work through SSH, a remote editor, Claude Code, Codex, or the command line.

Read [Agent Runtime](docs/agent-runtime.md) and [Getting Started](docs/getting-started.md).

## Human-Agent Collaboration

People and agents share project files, reusable skills, and an explicit workflow for handing work to each other. A developer can prepare a plan, an agent can implement it, and a person can review the result in the same project. Each participant has a separate account with permissions appropriate to their role.

UltiScrum keeps coordination small: six statuses, one task owner, an explicit next actor, and a timeline that survives handoffs. Tasks link to the plans, review candidates, and deliverables they concern. Work requested by another human returns to that person for acceptance.

Read [UltiScrum](docs/ultiscrum.md), [Project Workflow](docs/project-workflow.md), and the [Security Model](docs/security-model.md).

## Computer Use You Can Join

Agents work in real server-side browsers with saved logins. UltiCore combines DOM controls with mouse, keyboard, and clipboard operations so an agent can move between ordinary web forms, visual interfaces, and canvas-based editors. File uploads, screenshots, session recording, and a separate demo workflow are part of the same toolset.

When a task needs a person, open an authorized live portal to see the same browser and take control. Complete a login or approval, inspect the result, then let the agent continue. The browser session provides a shared place to work through steps that cannot be completed through an API alone.

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
| [Xpra](https://github.com/Xpra-org/xpra) and Chromium | Server-side browsers and live remote access |
| Git | Source collaboration and managed configuration history |
| restic | Encrypted backups governed by the installation's recovery policy |
| systemd | Services, scheduled system work, and process lifecycle management |

UltiCore connects these foundations to Slack, GitHub, coding tools, and the services your agents need. You host the workspace and agent processes, choose their model providers, and configure access to connected services.

## Operations Built Into the Workspace

Provision accounts and agents through role-aware commands. Manage credentials centrally, record shared changes, inspect failed jobs, and review software updates from the same environment where the team works. Backups and recovery procedures cover the operational side of keeping a shared server useful.

Read [Operations and Recovery](docs/operations.md) and the [Builder Heuristics](docs/builder-heuristics.md) behind the design.

## Development Status

UltiCore is preparing for its first public alpha and open-source release. This repository currently contains documentation and visual assets describing the running system. The source distribution and a reproducible installation package are not included yet.

Before publishing the source distribution, the actual export still needs review, clean-install testing, and restore testing. Publishing these guides does not establish that those release checks have passed.

Start with the [Overview](docs/overview.md), browse the [Documentation Index](docs/README.md), or watch the repository for release updates.
