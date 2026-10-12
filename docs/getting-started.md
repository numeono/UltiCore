# Getting started

This guide covers preparation and onboarding to an existing UltiCore installation. The public repository does not yet contain the source distribution or a tested installer. Cloning it provides documentation and assets, not a working server.

## Preparing a host

UltiCore's current operational guides assume Ubuntu Server, Linux user accounts and groups, systemd, and private network access through Tailscale. A deployment also needs storage, credential handling, and a recovery plan appropriate to the services it runs. This preview makes no tested minimum hardware claim.

Before handing a host to a team, the administrator needs to establish:

1. A working operating system, administrative account, and local recovery access.
2. The intended tailnet membership, network policy, SSH authentication, and service bindings.
3. UltiCore's commands, helpers, groups, permissions, and services from the eventual release package.
4. Organization configuration, credential grants, backup coverage, and recovery-key access.
5. Installation and restore checks on an isolated environment.

The guides describe those responsibilities; they do not replace the pending clean-install and restore tests for the public source distribution. Do not copy a running installation's credential files or private operational snapshot into a public repository.

## Provision an account

On an installed host, an UltiBoss uses the role-aware provisioning commands:

```text
user create ultidev <username>
user create ultiuser <username>
user create ultiboss <username>
agent create <username>
```

Choose the role before provisioning. UltiBoss grants full administrative authority. UltiDev is the ordinary developer role; UltiUser is for narrower access. An autonomous account uses `agent create`, which also provisions its runtime. See the [security model](security-model.md).

Use `user setup <username>` to resume human onboarding. Plain Linux account creation does not perform the UltiCore group, instruction, and runtime setup.

## Configure the organization

An UltiBoss runs:

```bash
setup organization
setup organization show
```

The profile supplies the organization description and internal workspace folder used in generated context. Keep credentials out of it. Choose the workspace folder name carefully; changing it after projects exist needs a separate path migration.

## Orient a teammate

Read `~/permissions.md` and the role section in `~/ULTICORE.md`. Confirm the project folder and any additional path grants. Human instructions contain a generated section and a preserved personal section; put personal notes only in the latter.

For an UltiDev or UltiBoss, the normal orientation commands are:

```bash
commands
files
docs
setup cli
setup git
setup vscode
```

These commands include interactive configuration. Run only the steps the teammate needs. Provider accounts, subscriptions, and service grants belong to that account's onboarding.

An UltiUser does not have the full `setup`, `files`, or `health` interface. The administrator supplies its connection details and authorized project paths. UltiUsers can check software with `software lookup` and file a shared installation request with `software request install`.

## Open the project

Remote editors connect to the teammate's Linux account over the configured SSH route. Authenticate the host before trusting it, then open an authorized project folder. Files and terminal programs run on the server.

Project working files live under `/workspace/files`; code repositories live under `/repos`. Read the project's own instructions first. Start project conversations inside the workspace project when they should contribute a nightly project summary. See [project workflow](project-workflow.md) for how initial working directories determine routing.

`setup terminal` can configure a persistent tmux workflow for a trusted account. This can preserve a session across disconnection when the account's process lifecycle permits it. Reboot ends tmux processes; unattended work that must restart needs a managed service or job.

## Verify the account can work

Check that the teammate can open its project, use its selected coding tool, and perform a small read with each required integration. One tool's connection does not establish access in another tool or in an unattended job.

Use `software lookup <name>` before installing a duplicate. Private tools can live in the account's writable directories. Shared installations require the appropriate authority and change every account's environment.

Open `ulticonsole` for the dashboard, and read [UltiScrum](ultiscrum.md) before assigning work across accounts. Autonomous account onboarding continues in [agent runtime and lifecycle](agent-runtime.md).
