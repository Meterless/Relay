# Troubleshooting

If something broke, start here. Most fixes take under a minute.

**Two places to look first:**

- **Settings → System Logs** shows recent errors, warnings and app events. It keeps the last 500. **Copy all** puts them on your clipboard so you can paste them into a bug report.
- **Run results**, under the plan, gives every step a verdict. On a failed run, **Explain this failure** tells you which step broke and why.

---

## Installing and launching

### Windows SmartScreen says the installer is unrecognized

Click **More info**, then **Run anyway**. The installer doesn't have a Windows code-signing certificate yet, so SmartScreen warns about it. Updates installed from inside Relay are different: Relay checks their signature before installing them.

### Antivirus flagged Relay

Relay sends real mouse and keyboard input and reads other apps through UI Automation. Some antivirus tools treat that as suspicious. If yours quarantined it, add an exception for the install folder, `%LOCALAPPDATA%\Meterless Relay\`, then reinstall.

### The app won't open

Work through these in order:

1. **A previous copy may still be running.** Open Task Manager, end any `meterless-relay.exe` process, and try again.
2. **Your data may be damaged.** Close Relay and rename `%APPDATA%\com.meterless.relay` to something else, such as `com.meterless.relay.old`. Reopen Relay. If it starts fresh, the problem was in that folder. You can bring your work back with **Settings → Data & Alerts → Restore from backup**, using an exported backup.
3. **WebView2 may be missing.** Relay's window uses Microsoft Edge WebView2, which comes with Windows 11 and current Windows 10. If it's been removed, install the Evergreen WebView2 Runtime from Microsoft.
4. **Reinstall.** Uninstall Relay and install it again from [the installer](https://meterless.ai/Installers/meterless-relay-latest.exe).

### The intro animation is in the way

Click anywhere, or click **Skip intro**. It also goes away by itself after a few seconds.

---

## Models and keys

### A key says "Invalid" or a model won't answer

1. Open **Settings → API Keys** and click **Verify** next to the key. Check that you didn't paste extra spaces. Relay trims them, but copying out of a password manager can still pick up the wrong text.
2. Click **Save Settings**. Edits on the API Keys and Model Routing tabs don't take effect until you save.
3. Check the provider's own console. Common causes are no credit left, a rate limit, a model your plan doesn't include, or a regional restriction.
4. A VPN or corporate proxy can block provider traffic. Turn the VPN off briefly to test.
5. If one provider is down, pick a model from another provider under **Settings → Model Routing**. The picker at the top of the right sidebar also switches models for a while without changing your settings.

### "Research call failed" (continuing with goal + desktop only)

The research step before planning couldn't run. The plan still compiles from your goal and desktop alone. Usually the Deep Reasoning model is unavailable, or doesn't support search. Pick a different one under **Model Routing**.

### Meterless Runtime shows "offline" or "secret rejected"

- **Offline.** Under **Settings → API Keys → Meterless Runtime**, click **Auto Detect** to try the usual local ports (8088, 8787 and 11434), or enter the base URL by hand and click **Recheck**.
- **Secret rejected.** Your runtime needs a secret key. Paste it into **Runtime secret key** and click **Verify**. Newer runtimes issue the key under Meterless › Setup › Connected apps.

### An OpenAI-compatible server isn't working

Click **Discover models**. What it shows tells you the problem:

| You see | It means |
|---|---|
| **Unreachable** | The base URL is wrong, or the server isn't running |
| **Key rejected** | The key is wrong |
| **HTTP …** | The server answered, but not as an OpenAI-compatible `/models` endpoint |

Base URLs usually end in `/v1`, for example `http://192.168.0.10:8000/v1`. If discovery isn't supported, type the model ID exactly as the server spells it and click **Add**.

### A local WebGPU model refuses a task

That's on purpose. Local models only handle short text tasks. Relay refuses to send them vision steps, web search, full plan compiles or very long inputs, because the result would quietly be worse. For those jobs, use a hosted model, a Meterless Runtime or your own server.

If you see "Local models need WebGPU", your graphics setup doesn't offer WebGPU to Relay.

---

## Windows and runs

### The plan targets the wrong window, or says it can't find one

- Check **Desktop Control → Active Sessions**. The window you meant should be listed there. If it isn't, find it under **Available Windows**, click it, and click **Track (N)**. If the list looks stale, click **OS** to refresh it, and switch to **All OS** to see every window.
- Minimized windows may not show up. Restore them first.
- In the plan panel, an amber **Fix windows** button means a step refers to a window you aren't tracking. Click it to map the step to an open window.
- Remember which tab you're on. The **My Desktop** / **Private Workspace** switch decides where new missions run. A mission compiled for a workspace runs there, not on your desktop, until you compile it again from My Desktop.

### A click lands in the wrong place, or "element not found"

Relay clicks controls by their accessible name. Some apps don't expose names, mostly canvas apps, games and heavily customized interfaces. For those:

- Turn on **Settings → Model Routing → Automation tiers → Vision click fallback**, and give the window a **Mirror** from its Active Sessions card. Relay will find the control in a screenshot instead. This uses vision tokens.
- Or edit the step to use different target text that matches what's on screen.

### Typing went to the wrong window

Windows sometimes refuses to bring a window to the front, for example while another app is grabbing focus or a system dialog is open. Close whatever is holding focus, click **Focus** on the session card, and then click **Retry step**. Builds after 0.8.8 stop the step with an error when this happens, instead of typing into whatever window has focus.

### A dialog popped up and the run paused

When Relay sees **A dialog is in the way**, it found a dialog it couldn't settle safely. Deal with the dialog yourself, then click **Retry step**. You can also skip the step or phase, or cancel the run.

To change how Relay handles dialogs, go to **Settings → Model Routing → Automation tiers → Modal dialog handling**:

- **Automatic** handles safe dialogs and pauses on risky ones.
- **Ask me** always pauses.
- **Off** fails the step instead.

### A step "worked" but shows fail or inconclusive

- **Inconclusive** means Relay couldn't check the step. That's common in apps with poor accessibility support. It's reported honestly instead of being counted as a pass.
- **Fail** means the check ran and the screen didn't match what the plan expected. Click the step in **Run results** to see what was checked. If the expected result is wrong, edit that step's check.
- In the default **Shadow** mode, failed checks never stop a run. If you switched to **Enforce** and it's too strict for a workflow, switch back under **Settings → Model Routing → Runtime verification**.

### The run is just sitting there

Look for the countdown in the plan panel. It means the run is waiting for the screen to change, or on a pause the plan asked for. Click **Continue now** to move on. **Stop** ends the run straight away, even in the middle of a wait.

### A scheduled mission didn't run

- **Was Relay open?** Schedules only run while Relay is open. What happens to a run missed while it was closed depends on the schedule's **If a run is missed** setting.
- **Is it waiting for windows?** A **Waiting for window** badge means a required window isn't open. Click **Fix windows**.
- **Was it auto-paused?** An **auto-paused** badge means it hit its failure limit. Fix the cause, then tick it back on. That resets the count.
- **Was Relay busy?** If **Skip if busy** is on, a run that came due while another mission was running was skipped.

Check **Insights → Alerts** for the reason.

---

## Private Workspaces

### "Debug port did not open", or the workspace won't start

Relay tries to fix this by itself, by taking over or closing a leftover browser and moving to a free port. If it still fails, close every window of that browser and click **Start** again. Make sure a Chromium browser (Chrome, Edge, Brave and so on) is installed. The create form lists the ones it found.

### The workspace says "Not responding"

Click **Repair**. Relay reconnects to the open pages, opens a new page, or relaunches the browser, whichever is needed. During a run it does this by itself, up to 3 times per mission.

---

## Data, backups and updates

### I want to undo a bad import, or get my old setup back

Go to **Settings → Data & Alerts → Automatic backups**. Pick a snapshot and click **Restore**. Restoring merges the snapshot into what you have, with newer items winning by ID. The world model is replaced completely. **Back up now** takes a snapshot right away.

### Moving to a new PC

1. On the old PC, click **Export workspace** under Settings → Data & Alerts. To bring your model routing and verification settings along, tick **Include preferences**.
2. On the new PC, click **Restore from backup**.

API keys are never included, so paste them again on the new PC.

### "Couldn't reach meterless.ai" when checking for updates

Check your connection or proxy, then click **Retry**. If **Update now** fails, nothing was installed. Use **Download installer instead** (or **Download Installer**) and run it by hand.

---

## Agent Bridge

| Problem | Fix |
|---|---|
| `relay doctor` shows ✗ on the discovery file or the bridge | Turn on **Settings → Agent Bridge → Enable Agent Bridge**. Relay has to be running. |
| `tier_insufficient` | Raise the agent's tier in Settings → Agent Bridge → **Agents**, or run `relay hello --tier act` |
| Calls hang for about 2 minutes, then return `approval_timeout` | An approval dialog is waiting in the Relay window |
| `auth_failed` | The bridge restarted and the token changed. Run the command again. |

There's more in [agent-bridge.md](agent-bridge.md).

---

## Still stuck?

Write to **support@meterless.ai**. Include:

- your Windows version
- your Relay version, from **Settings → Data & Alerts → App updates**
- what you were trying to do
- the relevant lines from **Settings → System Logs → Copy all**

If the problem happened during a run, an export from **Run results → Export run report** helps a lot.
