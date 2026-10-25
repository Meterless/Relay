# Agent Bridge: let a coding agent drive Relay

The Agent Bridge lets a coding agent work your Windows desktop through Relay. That could be Claude Code, Codex, Cursor, Gemini CLI, Windsurf, a VS Code agent, any other MCP client, or a plain script. The agent connects in one of two ways:

- **The `relay` command-line tool.** Every command prints JSON.
- **An MCP server.** Run `relay mcp` and the agent talks to it over stdio.

Whichever way it connects, the agent goes through the same engine your own missions use. It clicks controls by their *name*, found through Windows UI Automation, instead of guessing pixel positions. Every step gets a verdict, and anything that sends, submits, deletes, pays, publishes or signs out waits for you to approve it in Relay.

## How it's protected

- The bridge only listens on `127.0.0.1`, so nothing on your network can reach it.
- It uses a random token that changes every time the bridge starts. The token is written to a discovery file at `%APPDATA%\com.meterless.relay\bridge\bridge.json`, which is how the CLI finds Relay without any setup.
- It turns down requests that come from a web page in a browser.
- An agent can never read your API keys, the bridge token, or credentials you type yourself.
- Text an agent types is never logged. Only its length is.
- Every call is labeled with the agent's name in Relay's activity list. Runs an agent starts are marked with its name in the action journal.
- The bridge only works in the Relay desktop app. You can't turn it on from a browser preview.

## 1. Turn the bridge on

1. Open **Settings → Agent Bridge**.
2. Tick **Enable Agent Bridge**. The status line changes to *Listening on 127.0.0.1:&lt;port&gt;*.
3. A robot icon appears in Relay's header. Click it to see which agents are active, or hit **Disconnect all**.

Also on this tab:

| Setting | What it does | Default |
|---|---|---|
| **Tier for new agents** | What an agent can do the first time it connects | `observe` |
| **Always ask me, even for autonomous agents** | Kinds of action that always wait for you, whatever the tier: Send, Submit / confirm, Delete, Payment, Publish / post, Sign out / account, Destructive navigation, Destructive shell | Delete, Payment, Sign out / account and Destructive shell are ticked |
| **Approval timeout (seconds)** | How long an agent waits for your answer before it gives up | 120 |
| **Plan compiles per agent per day** | A cap on how many times an agent can ask Relay's planner to compile a plan | 20 |
| **Fixed port** | `0` picks a free port each time | 0 |
| **Allow agent clicks/typing while a mission runs** | Lets an agent act while one of your missions is running. This is risky, because it can corrupt the run. | Off |
| **Regenerate token** | Issues a new token right away | |
| **Disconnect all & disable** | Stops agent runs, denies any pending approvals, revokes the token and turns the bridge off | |

The **Agents** list shows every agent that has connected, with its call, run and approval counts. Each one has a dropdown where you set its tier.

## 2. Tiers

You grant tiers **per agent name**, so give each agent a name that stays the same.

| Tier | The agent can | Consequential actions |
|---|---|---|
| `observe` | List windows, find controls, take screenshots, and read state, runs, skills, the Data Vault and artifacts. It can also validate plans and poll events. It never touches anything. | Not applicable |
| `act` | Everything above, plus click, type, press keys, scroll, navigate, read a window's full text, run skills and plans, compile plans, and control runs | Always asks you first |
| `autonomous` | The same as `act`. It can also approve ordinary pauses in runs **it started**. | Runs them without asking, except the kinds you ticked under **Always ask me** |

An agent can ask for more access with `relay hello --tier act` (or `autonomous`). Relay shows you a dialog with two buttons, **Grant &lt;tier&gt;** and **Keep current tier**. Tiers never go up without you.

Some approvals are always yours: approval gates in plans, dialogs that need a decision, and Private Workspace host-access requests. Relay's own **Auto approve** toggle never applies to runs an agent started.

## 3. Install the CLI

The CLI isn't a separate download yet. It lives in the `cli/` folder of the Relay source tree, needs Node 18 or newer, and has no dependencies. If you have that folder:

```bash
cd <relay-repo>/cli
npm link            # puts `relay` on your PATH
relay doctor        # checks the discovery file, the bridge, auth and your tier
```

If you'd rather not use `npm link`, run `node <relay-repo>/cli/relay.mjs <command>` instead.

`relay doctor` checks each link in the chain and tells you how to fix whatever fails. If your tier is still `observe`, it also says how to raise it.

## 4. Connect your agent over MCP

```bash
relay mcp-config                    # prints every snippet, with your real path filled in
relay mcp-config --client cursor    # just one: claude, cursor, vscode, codex, gemini, windsurf
```

It prints ready-to-paste setup for:

- **Claude Code**: a `claude mcp add relay --scope user -- node <path>/relay.mjs mcp` command
- **Claude Desktop, Cursor, Windsurf, Gemini CLI**: an `mcpServers` JSON block
- **VS Code**: a `.vscode/mcp.json` block
- **Codex**: a `~/.codex/config.toml` block

If you used `npm link`, any client can use the short form. Settings → Agent Bridge shows the same snippet with a copy button:

```json
{
  "mcpServers": {
    "relay": { "command": "relay", "args": ["mcp"] }
  }
}
```

The MCP server names the agent after its client (for example `claude-code`). The CLI uses `--agent <name>`, or `$RELAY_AGENT_NAME`, and falls back to `relay-cli`.

`relay mcp-config` prints a ready-made config for each client.

### Give Claude Code the playbook

```bash
relay install-skill                 # copies the relay-desktop-control skill to .claude/skills/
relay install-skill --with-agent    # also adds the relay-operator subagent to .claude/agents/
```

Add `--dir` or `--agent-dir` to install somewhere else, and `--force` to overwrite files already there. Restart your agent session afterward so it picks up the new files.

## 5. CLI commands

`relay help` lists everything. `relay help <command>` shows how to use one command.

**Look around** (observe tier)

| Command | Usage |
|---|---|
| `state` | Engine status, sessions, queue and connected agents |
| `capabilities` | Every bridge method, the tier it needs, and whether you can call it |
| `hello` | `relay hello [--tier observe\|act\|autonomous]` |
| `windows` | `relay windows [--filter <text>]` lists window ids to use with `--window` |
| `find` | `relay find (--window <id> \| --window-title <t>) --query <text> [--type button]` finds a control by name without clicking it |
| `screenshot` | `relay screenshot (--window <id> \| --window-title <t>) [--out shot.png] [--max-width 1400]` |
| `skills` / `skill show <id>` | List saved skills and their parameters / show one |
| `status` | `relay status [--logs 15]` shows the current run, pending approvals, verdicts and recent logs |
| `runs` | `relay runs [--limit 10]`, or `relay runs show <runId\|planId>` |
| `vault` | `relay vault [list]`, or `relay vault get <key>` |
| `artifacts` | `relay artifacts [--plan-id <id>]` lists files runs saved, as absolute paths |
| `agents` | Agents seen this session, with their tiers and activity |
| `events` | `relay events [--since 0] [--topics run_complete,approval_needed] [--timeout-ms 25000] [--follow]` |
| `plan validate` | `relay plan validate <plan.json\|->` |

**Act** (act tier)

| Command | Usage |
|---|---|
| `focus` | `relay focus (--window <id> \| --window-title <t>)` |
| `click` | `relay click (--window <id> \| --window-title <t>) (--target "Send" [--type button] \| --rel-x N --rel-y N \| --x N --y N) [--button right] [--allow-fallback]` |
| `type` | `relay type (--window <id> \| --window-title <t>) (--text "…" \| <text>) [--target "Subject"]` |
| `keys` | `relay keys (--window <id> \| --window-title <t>) <key> [key…]`, or `--keys ctrl+shift+n` |
| `scroll` | `relay scroll (--window <id> \| --window-title <t>) --delta -5` (negative scrolls down) |
| `navigate` | `relay navigate [--window <id> \| --window-title <t>] --url https://…` |
| `wait-for` | `relay wait-for [--title-contains "Inbox"] [--window-title <t> --target "Compose"] [--timeout-ms 10000]` |
| `read` | `relay read (--window <id> \| --window-title <t>) [--max-chars 50000] [--out file.txt]` gets a window's full text by focusing it, then sending Ctrl+A and Ctrl+C |
| `skill run` | `relay skill run <id\|name> [--param k=v …] [--params-json {…}] [--wait] [--queue] [--timeout-ms N]` |
| `plan run` | `relay plan run <plan.json\|-> [--wait] [--queue] [--timeout-ms N]` |
| `plan compile` | `relay plan compile --goal "…" [--out plan.json]` |
| `wait` | `relay wait [--until settled\|terminal\|approval\|change] [--plan-id <id>] [--timeout-ms 120000]` |
| `stop`, `pause`, `resume`, `retry`, `skip-step`, `skip-phase` | Control the current run |
| `approve` | Approve the paused run. This needs the autonomous tier and only works when nothing consequential is waiting. |
| `approval wait` | `relay approval wait <approvalId> [--timeout-ms 60000]` keeps waiting on a pending approval |

**Plumbing**

| Command | What it does |
|---|---|
| `doctor` | Checks the connection end to end and prints fixes |
| `mcp` | Runs as an MCP server over stdio |
| `mcp-config` | Prints MCP config snippets |
| `install-skill` | Installs the agent skill (and, with `--with-agent`, the subagent) |
| `call` | `relay call <method> [--params-json '{…}'] [--param k=v …]` is a raw escape hatch to any bridge method |
| `version` | Prints the CLI and bridge API versions |

**Global flags**

| Flag | Meaning |
|---|---|
| `--window`, `-w <id>` | A window id from `relay windows` (`native_<hwnd>`), or a bare hwnd |
| `--window-title`, `-t <t>` | A case-insensitive piece of the window title, used instead of an id |
| `--agent <name>` | The agent name you grant tiers to |
| `--bridge-file <path>` | Use a different discovery file |
| `--no-wait-approval` | Return `pending_approval` right away instead of waiting for you |
| `--pretty` | Human-readable output for list commands |

### Exit codes

| Code | Meaning |
|---|---|
| `0` | OK |
| `1` | Error. Details are printed as JSON on stderr, often with a hint. |
| `2` | Usage error |
| `3` | Approval is pending, was denied, timed out, or can only be given in the Relay app |

## 6. What happens at an approval

1. A gated call waits while Relay shows you the agent's name, the action, the window and the evidence.
2. If you **Approve**, the action runs and the agent's call returns the result.
3. If you **Deny**, the agent gets `approval_denied`. That answer is final.
4. If nobody answers before the timeout, the agent gets `approval_timeout`, and nothing happened.

Typing, scrolling, focusing, waiting and reading are never gated on their own. What gets gated is the click or key that commits something: a Send button, Ctrl+Enter, Alt+S, Shift+Delete, or navigating to a sign-out or checkout page. Relay decides this with fixed rules. Nothing an agent puts in its request can make an action count as not consequential.

## A five-minute try

```bash
relay doctor
relay windows --filter notepad --pretty
relay find -t notepad --query "File"
relay hello --tier act                  # click "Grant act" in Relay
relay type -t notepad --text "Hello from the relay CLI"
relay click -t notepad --target "Edit" --type menuitem
relay keys -t notepad escape
```

`relay help <command>` shows every flag for any command.

## Common errors

| Code | What to do |
|---|---|
| `bridge_disabled` | Turn on Settings → Agent Bridge |
| `not_running` | Relay is closed. Start it. |
| `auth_failed` | The token changed because the bridge restarted. Try again; the CLI re-reads the token on every call. |
| `tier_insufficient` | Raise the agent's tier in Settings → Agent Bridge → Agents, or run `relay hello --tier act` |
| `element_not_found` | No control with that name was found. Nothing was clicked or typed. |
| `run_in_progress` / `engine_busy` | A mission is running. Use `relay wait`, or pass `--queue`. |
| `rate_limited` | The agent has used up its daily plan compiles |
| `platform_unsupported` | Desktop actions need the Relay desktop app on Windows |
| `connection_revoked` | You clicked **Disconnect all** |
| Calls hang for about 2 minutes, then return `approval_timeout` | An approval is waiting for you in the Relay window |
