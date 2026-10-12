# Agent Runtime

An UltiAgent is a Linux user account whose work is driven by an LLM. Its account owns its runtime, conversations, browser profile and external identities. Shared work belongs in project folders and the task system, where another person or agent can continue it.

UltiAgents have the shared filesystem access of an UltiDev, including shared skills and documentation. Their instructions are deliberately narrower. A short mission and selected skills focus attention without removing permissions. The [security model](security-model.md) describes those permissions and their limits.

## What Runs in the Account

UltiCore provisions the upstream Hermes runtime separately for each UltiAgent. Hermes manages conversations, native delegation and scheduled model work. A launch wrapper injects the account's configured Infisical credentials before starting it. The messaging gateway, scheduled work and task worker use that same wrapper.

| Component | Responsibility |
|---|---|
| Linux account | Home directory, file ownership and operating-system permissions |
| `~/.hermes/SOUL.md` | The agent's authored mission and generated operating instructions |
| Hermes runtime | Model requests, session history, tools and temporary subagents |
| Messaging gateway | Receives conversations and delivers replies |
| Hermes cron | Starts recurring agent work on a schedule |
| Task trigger | Starts eligible work from the account's UltiScrum queue when enabled |
| Launch wrapper | Supplies credentials to the runtime without copying values into prompts |

The gateway remains running between model requests. A stopped gateway makes the agent unreachable through messaging even if its model and credentials still work.

Grant external identities for the mission that needs them. Local Git work needs no GitHub credential; direct GitHub work can use a separate GitHub App with selected repository access. Separate identities allow access to be revoked independently.

## How Work Reaches an Agent

Each Slack integration has its own app and bot user. Invite the agent to relevant channels and mention it to start a conversation. Channel replies use threads, and follow-ups in the active thread can continue without another mention. A top-level request should include the context needed to act; the agent does not automatically receive the channel's entire history.

Provisioning sets one active top-level Hermes session per agent. Another conversation receives a busy response while it is occupied; follow-ups within the same conversation queue for that session. This policy does not lock arbitrary commands launched from an authorized operator's shell.

UltiScrum is the durable route for work crossing accounts. An enabled task trigger watches the recipient's queue and atomically claims eligible work before starting a fresh turn. Passive timeline notes do not wake it. Triggers are installed disabled, and installing them records the existing backlog so enabling one does not unexpectedly execute old tasks. See [UltiScrum](ultiscrum.md) for ownership and review.

Recurring agent work uses Hermes cron. Deterministic maintenance belongs in ordinary scripts and system scheduling when it has no need for a model. Operators inspect both kinds of automation in UltiConsole. Scheduling permissions are broader than ordinary agent editing: UltiBosses, UltiDevs and UltiAgents can manage any UltiAgent's cron jobs through the authorized command.

## Delegation and Human Input

Native Hermes subagents perform temporary work inside the parent account and session. They can investigate separate questions or review a deliverable. The parent remains responsible for checking their results and running appropriate deterministic validation.

A handoff to another UltiAgent is different. It changes who owns durable work and belongs on the task's existing timeline. A temporary reviewer does not replace the task's owner or its acceptance step.

When a step requires a person, Hermes' clarification tool can keep the turn open while it waits for an answer. For a browser login or device approval, the person can use the live [computer-use session](computer-use.md), then return control to the agent. A waiting question is not permission to proceed.

## Provision, Inspect and Maintain

Use `agent create <name>` to provision an account and `agent edit <name>` to change its mission, runtime, credentials or integrations. Provisioning includes a real model request through the launch wrapper; a configuration file alone does not establish that the agent can work.

| Command | Use |
|---|---|
| `agent status <name>` | Inspect runtime, provider, model, credentials and gateway readiness |
| `agent logs <name> -f` | Follow a running turn |
| `agent stop <name>` | Stop the running turn; the messaging gateway is separate |
| `agent schedule <name> list` | Inspect scheduled agent work |
| `agent login <name>` | Enter the account for authorized maintenance |
| `ulticonsole` | Inspect the fleet, jobs, settings and automation |

UltiBosses can manage any agent. UltiDevs can create agents and inspect, stop or log into agents, but ownership checks limit ordinary editing and removal to agents they created. UltiAgents cannot use `agent login` to become another account.

Start a fresh conversation when a mission change must apply immediately. Existing Hermes conversations can retain earlier instructions after a gateway restart; [Context Management](context-management.md) explains why.

Deleting a Linux account does not delete its remote services, credential projects or identities. Use the managed removal workflow and complete the external cleanup it reports.
