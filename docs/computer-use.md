# Computer use

UltiCore gives an account a real Chromium browser on a virtual display. An agent can drive it with commands, and a person can watch or take control through a browser portal. Both see the same page and use the same login state.

The browser renders into an Xpra display even when nobody is watching. In this stack, `headless` means that no portal is published; it does not mean that the page is unrendered. Plain page fetches and API requests remain available when an interactive browser is unnecessary.

## One session, several ways to act

`computer-use headless [URL]` starts or resumes the account's browser for automated work. `computer-use start [URL]` starts or resumes it with portal access appropriate to the launch context. The account has one live session, so later work should reuse it rather than create competing browsers.

| Control | Suitable work | Verification |
|---|---|---|
| DOM | Read page structure, navigate, fill fields, click controls and upload files | Read the resulting page state or query the destination service |
| Pixels | Canvas content, visual controls and elements the DOM cannot address | Inspect a screenshot or copy resulting content as text |
| Clipboard | Paste tables or text into canvas editors and read selected content back | Compare copied text with the intended content |

The DOM commands use Chromium's DevTools Protocol over a loopback connection. They activate the target tab so the visible browser follows the work. For multiple tabs, select the target explicitly and take a fresh snapshot after navigation; element references belong to the page state that produced them.

DOM snapshots include reachable same-origin frames. Cross-origin frames are reported but cannot be addressed through that DOM path. Use their own accessible page or the pixel controls when needed. Canvas applications often expose their toolbar in the DOM while drawing the document itself as pixels, which makes clipboard operations useful for grids and editors.

Use `computer-use dom upload` to supply a server file directly to the browser's file input. Clicking an upload button can open a native chooser outside the page and block subsequent actions. Verify that the destination stored the file.

## Persistent logins

A session starts from a saved profile seed and writes updated authentication state back during normal cleanup. Seeds retain cookies and selected browser storage, along with browsing history. They do not restore the previous session's open tabs.

The default seed is used for ordinary sessions. A named seed selected with `--seed <name>` keeps a separate collection of logins, useful when an account sometimes needs a different service identity. Choose the seed deliberately before opening privileged work. Logging into a privileged service in the default seed makes that login available to later sessions using it.

Seeds contain live credentials and stay in protected account storage. Inspect access with `computer-use auth show`; remove a seed through `computer-use auth clear <name>`. Browser and API identities can differ, so an API returning a record does not establish browser access to it.

For password entry, the secret-aware browser commands obtain the selected credential through the managed secret path. Credentials should not pass through model-visible command arguments or pasted transcripts. Human involvement remains necessary for factors that the account cannot complete, such as a device-bound approval.

## Watching and sharing

`computer-use watch` creates a portal for an existing session, including one started headlessly. It returns a token-bearing link and holds the session open long enough for a handoff. The link grants control of a logged-in browser and must go only to its intended viewers.

Access combines the session token with network policy. A resolved launching device can receive a device-restricted portal; eligible unidentified remote launches use an enumerated set of visible tailnet peers. Other contexts can use loopback access through an SSH tunnel. A headless session publishes no portal until requested.

An account can expose its own browser. Directly watching another account's private session requires access to its protected token, so cross-account watching is an UltiBoss operation. An agent can instead generate a link for its own session and give it to the person helping.

The Shared computer is a deliberate exception to individual ownership. Every UltiCore account can use its one communal profile, and several people can connect to the same live portal. Everyone sees and controls the same browser; concurrent clicks can interfere. Logins and browser state on Shared are shared with its users. It provides no separation between those people.

## Evidence and completion

`computer-use screenshot` captures the visible display. `computer-use capture start` records the existing session without changing its resolution or presentation, and `capture stop` finalizes the recording while leaving the browser open. Use the separate `demo` workflow when presentation pacing and styling matter.

Recordings contain visible browser data. Retain evidence with the owning project's artifacts, appropriate to that folder's audience. Video does not replace a backup or confirmation that a change reached its destination.

After a mutation, verify the result through a read-only API, copied text or a fresh page load. A toast or closed dialog is page feedback, not sufficient evidence by itself.

Finish automated work with `computer-use finish`. An unshared session closes promptly; a shared session waits for its link hold and viewers before normal cleanup. Activity-based cleanup and periodic sweeps handle abandoned sessions. Managed Hermes agents use this browser stack by default, but that configuration is an operating guardrail, not a security sandbox against code they can run in their account. See the [security model](security-model.md).
