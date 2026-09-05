# ⚡ pi-lazy-tools

Lazy-load tool groups on demand in [pi](https://github.com/badlogic/pi) to save context window tokens.

## Why

When you install many pi extensions (Observe, Vault, Slack, Buildkite, etc.), each one registers tools that are included in every system prompt. If you have 80-100+ tools, this can use a meaningful chunk of your context window before you type anything.

This extension categorizes tools into groups and lets you choose which load immediately vs on-demand:

| Mode | Behavior | Context cost |
|------|----------|--------------|
| **always** | Loaded at session start | Full token cost |
| **on-demand** | Loaded when LLM calls `load_tools` or you use `/tools-load` | Zero until needed |
| **off** | Never loaded | Zero |

## Install

```bash
pi install git:github.com/marcuskbra/pi-lazy-tools
```

This is a fork of `ashwin-shopify/pi-lazy-tools` that adds durable group modes, a passthrough for spawned agents, and a config-driven categorization prompt. See "Durability and spawned agents" below.

## Usage

### First Run

On first session start, the extension waits for tool registration to settle, then prompts you to configure tool groups. Later starts restore the saved profile for the current tool inventory without reopening setup. Or accept the default (core always-on, everything else on-demand).

<img width="465" height="430" alt="image" src="https://github.com/user-attachments/assets/14e444a0-7c09-49e7-b658-e19d0160e257" />


### Commands

| Command | Description |
|---------|-------------|
| `/tools-setup` | Open the setup wizard to configure group modes |
| `/tools-load [group]` | Load an on-demand group for this session |
| `/tools-status` | Show current group status |

### Keyboard Shortcut

**Ctrl+Shift+T** — Quick-load a tool group via selector

### How the LLM Loads Tools

The system prompt tells the LLM which groups are available but inactive. When it needs one, it calls:

```
load_tools(groups: ["observe", "vault"])
```

This activates those groups for the rest of the session. The LLM only pays the token cost for tools it actually needs.

### CLI Flag

Disable lazy loading for a session:

```bash
pi --lazy false
```

## Tool Groups

Groups are auto-detected by tool name prefix:

| Group | Description |
|-------|-------------|
| core | read, write, edit, bash, ask, etc. (always on) |
| observe | Logs, metrics, traces, error groups |
| vault | People, teams, projects, missions, pages |
| bk | CI/CD builds, jobs, pipelines |
| slack | Search, threads, channels, DMs |
| data_portal | BigQuery queries, dashboards |
| gcal | Calendar events, availability |
| grokt | Code search across repos |
| memory | Persistent memory bank |
| superpowers | Skills and subagent dispatch |

Actual groups and tool counts depend on what extensions you have installed.

## Config

Saved to `~/.pi/agent/lazy-tools.json`:

```json
{
  "version": 2,
  "groups": {
    "core": "always",
    "memory": "always",
    "observe": "on-demand",
    "vault": "on-demand",
    "slack": "on-demand",
    "buildkite": "off"
  },
  "toolHash": "b230f89df7c1d491",
  "profiles": {
    "b230f89df7c1d491": {
      "groups": { "core": "always", "observe": "on-demand" },
      "toolGroups": "machine-generated cached group definitions"
    }
  },
  "preserveModesBySignature": true,
  "passthrough": {
    "enabled": true,
    "modes": ["rpc", "json", "print"],
    "envMarkers": ["PI_TEAM_ROLE"]
  },
  "categorization": { "minGroups": 8, "maxGroups": 12 },
  "backgroundCategorization": { "enabled": true },
  "debugLogging": true
}
```

## Durability and spawned agents

The config stores global settings and hash-keyed tool profiles. Each profile
owns the grouping and modes for one stable tool inventory. A return to a known
inventory restores its exact profile without a categorization call or setup
modal. The legacy top-level group fields mirror the active profile so earlier
package versions can still read the last-used configuration.

### preserveModesBySignature

When an unseen tool inventory needs a new profile, the extension categorizes it
once and may rename a cluster (for example `team_management` becomes `team`). A
rename used to drop your `always` choice back to `on-demand`. With
`preserveModesBySignature: true`, the new profile inherits the mode of the old
group its tools most came from, so `always` survives renames.

### passthrough

pi has no native notion of a subagent. A team teammate is just a child pi
process reading this same config, and this extension's tool filtering would
strip the `team_message` and `team_shutdown` tools the teammate needs to report
back and shut down. Before the first config exists, known spawned and
non-interactive sessions pass through so an unattended process cannot open the
setup modal. With `passthrough.enabled: true`, later sessions stop filtering
when either the run mode is in `modes` (a pi-native signal covering RPC and
one-shot runs) or one of `envMarkers` is present in the environment (covering
pane-spawned teammates, which run as ordinary `tui` sessions and are only
identifiable by the role marker their spawner injects). Add other spawner
markers, such as a future `PI_SUBAGENT`, to `envMarkers` without a code change.

### categorization

The group-count target and grouping guidance handed to the categorization LLM.
`minGroups`/`maxGroups` default to 8 and 12; set them lower for fewer, broader
groups. `guidance` overrides the default "one service per group" bullets.

### debugLogging

Set `debugLogging: true` to write startup, categorization, and tool-activation
records to `/tmp/lazy-tools-debug.log`. The `/lazy-tools-logging` command toggles
and persists this setting. Set it to `false` after diagnosis.

### backgroundCategorization

When the settled tool inventory has no saved profile, the extension applies a
cached or prefix-based grouping, then creates one profile in the background.
Known inventories restore immediately. Background categorization never opens
setup after the first install. The first prompt after an unseen inventory may
briefly use the fallback grouping until categorization finishes.

The `bench/background-categorization.mts` script shows the effect with the LLM
stubbed to a fixed latency: the awaited startup time drops from the full latency
to roughly zero.

## Development

```bash
pnpm install
pnpm test
```
