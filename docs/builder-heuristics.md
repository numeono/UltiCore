# Builder Heuristics

The builder heuristics guide how we build and what we build on. They apply to code, infrastructure, commands, skills, and documentation. Each group is in priority order: when two conflict, the higher one wins. On an installed server, `setup heuristics` controls their inclusion in account instructions.

**Call them by name.** Collectively they are the builder heuristics; individually, "builder heuristic N". When you invoke one in a PR, a Slack message, or a note to a teammate, name it and say where it lives: *"that cuts against Standard is best, builder heuristic 4, see `/server/docs/builder-heuristics.md`"*.

## How We Build

**1. The best part is no part.** Before adding a file, dependency, service, config flag, abstraction or script, try to delete the need for it. Reuse what already exists, or show the problem doesn't need solving. Every part added is a part someone must understand, maintain, secure, back up and eventually remove.

**2. First principles: question the requirement.** Ask what outcome is actually needed, which constraints are real and which are assumptions inherited from an earlier decision, and whether a recent change to the product, system, team or tools has made the requirement unnecessary or wrong. Reason from what is true now, not from precedent: the right implementation of a bad requirement is still the wrong result.

**3. Occam's razor: simple is best.** When several solutions fit the facts, prefer the one that introduces the least complexity. Complexity has to earn its place by solving a problem you can name out loud.

**4. Standard is best.** Prefer the boring, well-trodden option: the language's idiom, the framework's default, the tool everyone already has, the pattern already used in the repository or on the server. Match the surrounding code rather than importing your own style. A custom mechanism must be justified by a concrete need the standard one demonstrably fails to meet.

**5. Deterministic is best: programmatic over AI.** We are AI-first in how we build, deterministic in what we ship. Use agents to write scripts, parsers, schemas, migrations, and tests, then let the shipped system run with no model in the loop whenever possible. Use AI at runtime only where determinism genuinely can't reach: open-ended language, judgement over messy or unseen input, a task with no rule you could state. When you do, keep it at the edge behind a narrow boundary (heuristic 7), check its output programmatically, and decide up front what happens when it's wrong.

**6. Maintainable is important.** Write for whoever inherits it. That may be you months later, or an agent with none of your context. Obvious control flow over clever compression; one documented way to do a thing over three undocumented ones. Leave the *why* where the *what* isn't self-evident. If it can't be understood without you in the room, it isn't finished.

**Name things so they explain themselves.** Prefer the verbose name over the terse one for variables, functions, commands and file names alike, so a reader can tell what something is without opening it. Verbose, not long: `client-extract-config` beats `cfg`, and also beats `the-configuration-object-used-by-the-client-extract-skill`.

**7. Modular is important.** Keep concerns in separate, replaceable pieces with narrow boundaries, one job each, swappable without touching their neighbours. Modularity shapes the parts that survive builder heuristics 1 through 5; it is not a licence to add parts.

**8. Production-ready, productizable and open-sourceable.** Build work that could ship: errors handled, sane defaults, deployable by a stranger without you narrating it. Hardcode nothing that would be hard to rip out, including a person's home directory, organization name, hostname or credential, so publishing it on GitHub, or deploying it for a client, takes little more than pushing it. Most of what we build here is the reference implementation for what we sell.

## Choosing Tools, Dependencies, and Services

**9. Open source, and commercially usable.** Prefer open source under permissive licences, such as MIT, Apache-2.0, and BSD. Check the licence *before* adopting: copyleft and source-available licences (GPL/AGPL, SSPL, BSL/Elastic) can impose obligations or restrictions on shipped client work, so they need a deliberate decision, not a default. Closed source is the exception that must be argued for.

**10. Self-hostable, and owned rather than rented.** Favour software we can run on our own hardware. A hosted tier counts only if we could move it in-house later: an open-source server, a documented deploy, exportable data, no proprietary lock-in. All else close to equal, prefer free, one-time or metered pricing over per-seat subscriptions, which tax growth and hand the vendor a pricing lever. Cost is a tiebreaker, not a gate: where a subscription is genuinely the best tool for something mission-critical (Claude Code, OpenRouter, Slack), pay for it without apology, and reserve the pressure for the incidental and the replaceable.

## When a Heuristic Can't Be Met

Some things have no compliant option, such as a client's platform, a vendor API, or a seat-based service with no self-hosted equivalent. Break the heuristic deliberately: say which one and why, keep the offender at the edge behind a swappable boundary (heuristic 7), and don't let it become the precedent for the next decision.

If a request conflicts with these, build what was asked, then say what you'd have done differently. Don't silently substitute your own design.
