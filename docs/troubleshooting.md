# Troubleshooting

If something broke, start here. Most of the common stuff has a fix that takes under a minute. The list is roughly ordered from most-common to less-common.

## The app takes forever to open the first time

Normal. The first launch can take anywhere from thirty seconds to a couple of minutes, depending on your machine. Relay is unpacking its model cache, setting up local storage, and registering with Windows. After the first launch, it opens in two or three seconds.

If you've waited more than five minutes on the first launch and nothing has happened, see "The app won't open at all" further down.

## Windows SmartScreen warned that the installer is unrecognized

Click **More info**, then **Run anyway**. Our installer is signed, but SmartScreen builds reputation over time, and new releases sometimes haven't accumulated enough of it yet. The signature is valid. You can verify it by right-clicking the installer, going to **Properties → Digital Signatures**, and confirming the publisher name. *(confirm before publishing)*

If your antivirus quarantined the installer outright, see the next item.

## Antivirus flagged Relay as suspicious

A few antivirus tools mistake Relay's input injection code for malware because the same Windows APIs that drive automation are also what some malware uses. The fix is to add an exception:

1. Open your antivirus settings.
2. Find the exclusions or allowlist section.
3. Add the Relay install folder (usually `C:\Program Files\Meterless Relay\`) and the executable inside it.
4. Reinstall Relay if the installer was quarantined and deleted.

This is annoying and we know it. The signed installer reduces how often this happens, but doesn't eliminate it.

## Login or API key isn't working

Open **Settings → Models**. Confirm the key is pasted with no extra spaces at the start or end. Click **Test connection**.

Common causes when the test fails:

- The key has regional restrictions that don't match where your machine is. Gemini in particular has some regional gates on the free tier.
- The key has run out of credits or hit a rate limit. Check the provider's console.
- There's a corporate firewall or VPN sitting between Relay and the model provider's servers. Try turning the VPN off briefly to confirm.

If the key tests fine in Relay but missions still fail with an auth error mid-run, force-close Relay and reopen it. The settings sometimes cache the previous key for a few minutes.

## The model isn't loading

This usually means one of three things:

1. The model name in your settings has been deprecated by the provider. Open **Settings → Models** and pick a current model from the dropdown.
2. Your account doesn't have access to that specific model. Some providers gate larger models behind paid tiers.
3. The provider is having an outage. Check their status page. Relay can't fix their downtime, but you can switch to a different provider in the meantime under **Model routing**.

## A mission fails because Relay can't find a window

This almost always means a tracked window got closed, or was never tracked in the first place. Open the **Tracked Windows** panel on the left and confirm the window you expected Relay to use is in the list and still has a thumbnail.

If the underlying app got restarted, click the refresh icon next to the tracked window. Relay will reattach to the new instance.

If you wrote a goal that mentions an app by name but never tracked it, Relay will tell you in the plan inspector. Track the window and run the plan again.

## Multi-monitor clicks land in the wrong place

If you're on Windows and your secondary monitor is set to a different DPI scaling than your primary, clicks can land slightly off. The fix:

1. Right-click the desktop and pick **Display settings**.
2. Set both monitors to the same scaling (usually 100% or 125%).
3. Sign out and back in. Windows requires this for the scaling change to apply everywhere.

This is a Windows quirk, not something Relay does wrong, but it can be fixed.

## Vision verification keeps failing on a step that actually worked

The vision check is comparing the live screen to what the planner expected. If the expectation was too strict (it was looking for a specific text label that's now slightly different), the check fails even though the workflow is fine.

Two ways to handle it:

- Loosen the check. Open the plan, find the step, change the verification from **Strict** to **Loose**. Loose just checks that the right window is in focus and roughly the right area of the screen looks plausible.
- Turn the check off for that step. Right-click and pick **Skip verification**. Use this if you've watched the step succeed several times and you're sure of it.

## Relay crashes after a Windows update

Windows updates occasionally change which APIs are available, and Relay sometimes needs an update to keep up. Check the **Releases** page for a new version. If there isn't one, file a bug report including the version of Windows you updated to, and we'll get a patch out.

In the meantime, the previous build of Relay is still installed under the **Programs and Features** uninstaller list with the option to roll back.

## Settings reset after an update

Settings live in `%APPDATA%\Meterless Relay\` *(confirm before publishing)*. If they got wiped, it usually means the update migrated to a new format and your previous settings didn't make it across.

Restore from the auto-backup:

1. Close Relay.
2. Go to `%APPDATA%\Meterless Relay\backup\`.
3. Find the most recent dated folder.
4. Copy `settings.json` from that folder back into the parent directory.
5. Reopen Relay.

We auto-back-up settings on every update. The backups are kept for thirty days.

## The app won't open at all

In order from most-likely to least-likely:

1. **A previous instance is still running.** Open Task Manager, look for `meterless-relay.exe`, end it, and try again.
2. **The local data folder got corrupted.** Move `%APPDATA%\Meterless Relay\` to your desktop (don't delete it, in case you want to restore it). Reopen Relay. It'll start fresh. If it now opens, your old folder had something bad in it and you can copy your `keys.json` back if you want to keep your API keys.
3. **A Windows visual C++ runtime is missing.** Install the latest Visual C++ Redistributable from Microsoft. Relay depends on it and most machines already have it, but a fresh Windows install sometimes doesn't.
4. **The install is genuinely broken.** Uninstall and reinstall. Your data folder survives uninstall, so you don't lose anything.

If none of that works, file a bug report. Include what happens when you try to launch (does anything appear in the system tray? does the process briefly show in Task Manager and then die?), and we'll dig in.

---

## Still stuck?

Email us at **<support@meterless.ai>**. Tell us your Windows version, your Relay version (under **Settings → About**), and what you were trying to do when it went wrong. Logs live in `%APPDATA%\Meterless Relay\logs\` and attaching the most recent one helps a lot.
