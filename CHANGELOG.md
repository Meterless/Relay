# Changelog

This page covers what changed in Relay, newest first and in plain language. Dates are the day the signed build was published to `meterless.ai/Installers/`.

Your installed version is shown under **Settings → Data & Alerts → App updates** ("You're on v…").

---

## Unreleased

These changes are in the source but haven't shipped in a signed build yet.

What's new:
- **Meterless Quick Connect.** Settings → API Keys → Meterless Runtime can now connect from a connect link. You can paste the link (or a screenshot of its QR code) into the Base URL or secret key field, load a QR image, or scan the code with a camera. Relay tries each address the link lists, keeps the first one that answers with your key, and can set every task to use the runtime in one step. There's also a new **App name** field that sets how Relay shows up in the runtime's app traffic. Camera scanning hasn't been tested inside the packaged app yet.

Fixed:
- Typing, key presses and clicks now stop with an error when Windows refuses to bring the target window to the front. Before, they could type into whatever window had focus instead.
- Live mode no longer gets stuck on "thinking" when a model provider fails. When a vision check can't run, it falls back to a UI Automation check.
- Skill drafts made from a recording use the exact text you typed as each parameter's default.
- Two Meterless Runtime errors (a stalled lane, and a class with no route) are no longer retried automatically. The retries could pile up into a long backlog.

---

## 0.8.8 · 2026-09-26

**In short:** coding agents can now drive Relay, pop-up dialogs no longer derail runs, Tailor learns from more than files, and you can use any OpenAI-compatible server.

What's new:
- **Agent Bridge.** Claude Code, Codex, Cursor, Gemini CLI and any other MCP client or script can now control Relay through the `relay` CLI or `relay mcp`. To turn it on, go to Settings → Agent Bridge. From there you:
  - grant each agent a tier: observe, act or autonomous
  - choose actions that always ask you first
  - watch agent activity
  - disconnect every agent with one click

  A header icon shows when the bridge is on. Agent requests for consequential actions open an approval dialog in Relay. The agent kit has a skill, a subagent, a tutorial and MCP configs for the common clients. See [docs/agent-bridge.md](docs/agent-bridge.md).
- **Modal dialog handling.** When a step runs into a dialog the plan didn't expect, Relay reads the dialog's buttons and text, completes or dismisses it to fit the mission, and carries on. This covers Save As, "unsaved changes", confirmations, and browser and in-page pop-ups. Dialogs that look destructive, or that Relay can't decide on safely, pause and ask you. You can change this under Settings → Model Routing → Automation tiers → **Modal dialog handling**: Automatic, Ask me, or Off.
- **OpenAI-compatible endpoints.** Settings → API Keys has a new **OpenAI-compatible endpoint** section. Give it a base URL and an optional key, then click **Discover models**. It works with vLLM, LM Studio, llama.cpp, LiteLLM, a company gateway, or a Meterless box on your network. The models you pick show up in the routing pickers as `compat/<id>`.
- **Tailor can learn more than files.**
  - **Tell:** type or dictate how something works.
  - **Show:** give a narrated tour while Relay notes the apps you visit.
  - **Learn from use:** your saved macros and repeated missions feed it automatically.
  - A Getting Started guide, plus Ctrl+K entries for "Tell Tailor…" and "Give Tailor a tour…".
- The Agent Bridge can list and start Private Workspaces.

Fixed:
- The installed app can now reach model servers on your local network. These calls go out through a native transport.
- `wait_for` steps in a Private Workspace no longer always time out.
- Pressing Stop while Relay was repairing a run could carry over into the next mission. It can't anymore.
- Planning is faster, because the research step before a compile is shorter.
- Long self-repair and data-structuring steps now have time limits, so a run can't hang on them.
- A brief network drop to a local-network model server is retried once.
- You get a clearer message when a vision request goes to a model that can't read images.
- Number filters now read amounts like "$84,641" correctly.
- Tailor fixes:
  - Documents marked local-only were sometimes sent to a cloud model. They aren't anymore.
  - Imports now run one at a time.
  - Cancel works.
  - Plans with password steps compile.
  - Map labels no longer draw over dialogs.

---

## 0.8.7 · 2026-09-10

What's new:
- **Waits show a live countdown with a Continue now button.** This covers every pause in the middle of a run, such as wait steps, waiting for the screen to change, macro pacing and retry back-off. **Continue now** moves on straight away.

Fixed:
- **Stop** and **Pause** now end a wait immediately. Before, you had to sit out the timer.

---

## 0.8.6 · 2026-09-08

What's new:
- **Meterless Runtime as a model provider.** Settings → API Keys → Meterless Runtime has a base URL with **Auto Detect** and **Recheck**, a live online/offline status, and a secret key with **Verify**. Once it's connected, you pick a *mode* (such as Auto, Deep, Fast, Local or Vision) instead of a model. Settings → Model Routing adds one-click **Auto-set to Meterless Runtime** presets: Balanced, Private (on-device) and Fast.

Fixed:
- **Private Workspaces fix themselves mid-run.** If a workspace page crashes, Relay reloads it. If a tab or the whole browser closed, Relay reopens it. Then it re-runs the same step in the same workspace, up to 3 repairs per mission. A workspace that stops answering shows **Not responding** with a **Repair** button.
- Browser sessions recover on their own after a disconnect.

---

## 0.8.5 · 2026-09-03

This is the first public build since 0.7.12, so it includes everything built in between.

What's new:
- **Private Workspaces.** Missions can run in their own background browser, with logins, cookies and downloads kept separate from yours. Switch between **My Desktop** and **Private Workspace** at the top of the Desktop Control panel. Whichever is selected is where new missions run. Workspaces:
  - remember labels for the accounts you signed into (never passwords)
  - keep their own files
  - ask before touching anything on your computer: **Allow once**, **Allow for this mission**, **Always allow** or **Deny**
- **Workspace files.** Data a workspace mission captures is saved as files in that workspace. Later runs can reuse it with `{{workspace.<key>}}`.
- **Tailor.** It's the scissors icon in the header. Drop in your process documents, folders or zip files, and Tailor builds a model of your organization and proposes mission candidates. You can then walk a candidate step by step, test it, run it, save it as a skill and schedule it. Collections can be marked local-only.
- **Claude and ChatGPT history imports.** Tailor can import your exported chat history. It scores each conversation, keeps the ones that describe real work, and explains why it skipped the others.
- Tailor now builds candidates *while* documents import, so you don't have to press Analyze first.

Fixed:
- Starting a workspace no longer fails with "debug port did not open". Relay now takes over or closes a leftover browser and moves to a free port.
- The org map and world map show fewer labels at once. Hovering a node highlights only its connections.

---

## 0.7.12 · 2026-07-31

A small maintenance release. The published notes only say "Release 0.7.12". The one change we can confirm from the source is more reliable API key checks: **Verify** now fails only when the provider actually rejects the key.

---

## 0.7.11 · 2026-07-27

What's new:
- **Update checks and one-click updates.** Relay checks for a newer build at most once a day when it launches, and shows a banner with **Update now**, **Later** and **Don't show again**. **Update now** downloads the signed update, checks its signature, installs it and restarts Relay. Nothing installs without your click. You can also check by hand under Settings → Data & Alerts → **Check for Updates**.
- **New models:** GPT-5.6 (Sol, Terra and Luna), and Kimi K3 through OpenRouter and OpenCode Go.

Fixed:
- Verifying an OpenCode Go key no longer reports a valid key as invalid.
- Fixed a styling build problem.

---

Earlier builds aren't listed here. For what Relay can do today, see [docs/features.md](docs/features.md).
