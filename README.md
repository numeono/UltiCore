<p align="center">
  <img src="assets/ulticore-banner.svg?v=lt-clear-gap" alt="UltiCore infrastructure for human-agent collaboration" width="1200" />
</p>

# UltiCore

UltiCore is a shared development environment built for **human-agent collaboration**. It gives people and autonomous agents a common workspace, project context, and task workflow so they can build together, hand off work, and review results while keeping context and responsibility clear.

Each participant works through a separate Linux account with role-based permissions. The system brings together account provisioning, agent runtimes, browser computers, credentials, and server operations. UltiConsole provides a browser interface; the same installation also exposes commands for people, agents, and automation.

## Development Status

UltiCore is preparing for its first public alpha. This repository currently contains documentation and visual assets. The guides describe the running system and its operating model; the source distribution and a reproducible installation package are not included yet.

Before publishing the source distribution, the actual export still needs review, clean-install testing, and restore testing. Publishing these guides does not establish that those release checks have passed.

Start with the [overview](docs/overview.md), or browse the [documentation index](docs/README.md).

## Security Model

Everyone working on UltiCore gets a standard Linux user account with one of four roles: UltiBoss, UltiDev, UltiAgent, or UltiUser. The roles distinguish administrative authority and filesystem reach from the context supplied to a coding tool or autonomous agent.

An UltiAgent has the same shared filesystem reach as an UltiDev, with a narrower mission and skill set. An UltiUser has narrower filesystem permissions. Shared workspace files are accessible to every account, while credentials belong outside that workspace.

Read the [security model](docs/security-model.md) for roles, network access, privileged helpers, credential handling, and the limits of these controls.

## UltiScrum

Most task management systems are needlessly complex. UltiScrum is optimized for lean teams, with only the essentials needed to assign work, pass it between people and agents, and get a decision on the result.

Each task has one owner, one timeline, and an explicit next actor. Six statuses describe progress. Project folders hold the work itself, and task records link to the relevant files. Review makes acceptance a visible step.

Read [UltiScrum](docs/ultiscrum.md) and the [project workflow](docs/project-workflow.md).

## Agent Computer-Use System

UltiCore runs browser sessions on the server. Agents can use DOM controls, mouse and keyboard input, and clipboard operations. A person can open an authorized live portal to inspect or take over a session. Saved browser state belongs to the account running it.

Read [computer use](docs/computer-use.md) for session control, browser profiles, recording, and access rules.

## Autonomous Agent Stack

An UltiAgent combines a Linux account, the Hermes runtime, a defined mission, selected skills, and explicitly configured service access. Persistent gateways receive messages; scheduled and transient jobs cover other execution patterns. Shared tasks record responsibility across accounts.

Read [agent runtime and lifecycle](docs/agent-runtime.md).

## Context Management

UltiCore separates the context an account always receives from the guidance it loads for a particular job. Human accounts use `ULTICORE.md`; UltiAgents use `SOUL.md`. Shared skills contain narrow workflows, documentation explains the system, and project summaries let work continue across tools and sessions.

Read [Context Management](docs/context-management.md) and the [builder heuristics](docs/builder-heuristics.md).

## Working with an Existing Installation

The [getting started guide](docs/getting-started.md) covers account onboarding and the commands used after deployment. [Operations and recovery](docs/operations.md) covers managed changes, repository workflows, maintenance, backups, and restore verification.

The public guides use generic examples. An installation's account names, network policy, credentials, schedules, and recovery configuration belong in its own private records.
