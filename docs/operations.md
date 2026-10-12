# Operations and recovery

UltiCore separates managed system files, project repositories, and working data. Each needs its own change history and recovery coverage. A successful Git push does not establish that working files or databases can be restored.

## Record managed changes

Local Git histories track managed content under `/server`, `/agents`, and selected parts of `/workspace`. Home histories use explicit allowlists. Read the tracked files and ignore rules before assuming a directory has version history.

Use `changes <file>` to inspect a managed file's history. For an intentional shared change, record the reason and exact paths:

```bash
sudo /server/scripts/record-change "Clarify the setup procedure" /server/docs/example.md
```

Without paths, the helper can stage unrelated work in the same repository. Automatic commits provide a fallback but may attribute an edit by file ownership or as `auto`; they do not reliably identify the editor.

Change generated instructions through their source documentation and configuration. The instruction watcher regenerates account context, and the skills watcher maintains human skill links. See [context engineering](context-engineering.md).

## Collaborate through project repositories

A team repository can use a bare hub under `/repos/bare`, with working copies under `/repos`. Access depends on the hub's actual permissions. A hub enrolled in the installation's GitHub mirror has a remote named `github`.

The documented mirror fetches remote branches, fast-forwards compatible local branches, and pushes feature branches. It logs divergence instead of forcing either side to match. It excludes the literal branches `main` and `master` from upstream pushes. It does not synchronize all tags, deletions, repository settings, or access rules.

Where the hub tooling is deployed, the usual work cycle is a feature branch, a push to the hub, a successful mirror run, and a reviewed pull request on GitHub. The resulting default branch returns to the hub through a later fetch. Check the installation's schedule and mirror logs before assuming delivery.

Local hooks can restrict ordinary pushes to protected branches. They do not prove that GitHub rejects every direct push, or that a user with broad repository filesystem access cannot alter local files and refs. Treat these as workflow controls whose enforcement depends on the repository configuration.

An agent can use the hub without holding a GitHub credential. Direct API operations can use a dedicated GitHub App installed on selected repositories. The App and its private key still require an explicit grant and a revocation process.

## Inspect health and maintenance

Trusted accounts can start with:

```bash
health
health alerts
hosted
software maintenance
software lookup <name>
```

`health` reports current resource and service conditions. `hosted` reports published services and their backing processes. The resource watcher requires sustained conditions before alerting and distinguishes separate failed executions from repeated observation of one old failure. A successful retry can clear a pending incident without notifying anyone.

Slack delivery is optional and can fail independently of local reporting. Silence does not establish recovery; inspect the current condition and logs.

Maintenance has separate paths for ordinary security updates, reviewed dependency upgrades, and reboot windows. The installed timer units and `software maintenance` are the schedule's source of truth. An administrator's Automatic Updates switch does not interrupt a job already running.

Manual upgrades normally check for active users. The check covers specific session and job mechanisms, not every possible background process. Scheduled maintenance can proceed while people are active. Gateway draining gives existing agent turns time to finish, but a reboot can still interrupt unfinished work. Save progress to files and task outcomes before a planned window.

## Understand backup coverage

Restic provides encrypted filesystem backups according to the installation's configured sources, exclusions, mount boundaries, retention, and hooks. Inspect `/etc/ulticore-backup/config` and the exclusion policy with appropriate administrative access. Keep credential values out of diagnostic output.

The common backup commands are:

| Command | What it establishes |
|---|---|
| `backup dashboard` | Reported backup state, snapshots, and schedule |
| `backup automation` | Configured scheduling and retention |
| `backup list` | Available snapshots |
| `backup start` | Run a filesystem backup |
| `backup verify` | Check repository structure and metadata integrity |
| `backup restore <snapshot> target <directory>` | Restore into a chosen destination, with UltiBoss authority |

`backup verify` does not read every data pack and is not a restore test. A filesystem backup can also complete despite a failed pre-backup hook. Check the latest run's age, result, and hook logs.

A file traversal of a running database does not establish a consistent database backup. Configure the database's supported dump or physical backup method, include its output in the backup policy, and restore it independently during testing.

Keep the recovery password available through an approved store outside the server. A password held only inside its own encrypted backup cannot unlock that backup after the original machine is lost. A repository on another disk in the same machine also needs separate offsite coverage for whole-machine loss.

## Distinguish the private Git snapshot

`backup snapshot` exports selected committed managed files to a private repository. It omits ordinary workspace projects, code repositories, bulk data, and other material outside its explicit source selection. This is an operational recovery mechanism, not a public release export or a full machine backup.

Filename and content checks reduce accidental disclosure but cannot prove that arbitrary tracked text contains no private information. Review the selected content before changing the export boundary. Keep installation configuration, account metadata, and recovery records private.

## Verify restoration

Restore to a fresh, isolated destination. Inspect the result before copying selected files into their intended locations. Do not restore a whole snapshot over a running system.

Recovery evidence should identify the snapshot, configured coverage, recovery environment, commands used, and result. Verify representative files, ownership and permissions, required credentials, database restoration, and application behavior. A machine rebuild also needs packages, service configuration, and network access that a selected Git export may not contain.

The public source distribution's clean-install and restore tests remain pending. These procedures explain what must be verified; they do not report a successful release test. See [development status](../README.md#development-status).
