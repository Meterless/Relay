# Privacy

Most of what Relay does happens on your computer. Some of it doesn't, and it's worth being specific about which is which, because the difference matters.

## What stays on your machine

- **Your tracked windows.** The list of windows you've told Relay to pay attention to. Never sent anywhere.
- **Your past goals.** Every instruction you've ever typed. Saved in a local file. Never sent anywhere except as part of a model call you initiate.
- **Your past plans.** The structured workflows Relay generated for you. Saved locally. Never sent on their own.
- **Your procedural memory.** The notes Relay takes about workflows that succeeded. Local file.
- **Your workspace artifacts.** Everything Relay has captured from your screen for you, including screenshots, extracted text, files it produced. Local folder.
- **Your API keys.** The keys you've pasted for Gemini, OpenAI, or Anthropic. Stored encrypted on your machine. Sent only to that provider's servers when Relay calls them on your behalf.
- **Your settings.** Your keybindings, theme, model routing preferences, everything in the settings panel. Local.

All of this lives under `%APPDATA%\Meterless Relay\` *(confirm before publishing)*. You can open it in File Explorer right now if you want to see exactly what's there.

## What gets sent to an AI provider when you use Relay

When you type a goal and hit send, Relay puts together a request and sends it to whichever model provider you've configured. That request contains:

- The text of your goal.
- A text description of your tracked windows (their titles, the apps they belong to, their rough sizes and positions).
- A short summary of relevant past plans, if any apply to this goal.
- For vision verification steps, the actual screenshot of the tracked window that's being checked.
- The schema the model is supposed to fill in (which is the same every time and doesn't contain anything personal).

That's it. Relay doesn't send a continuous feed of your screen. It doesn't send your file system. It doesn't send your other open apps that aren't being tracked. It doesn't send your typing keystrokes outside of what's in the goal box.

The provider you picked (Google, OpenAI, Anthropic, or a local model) handles that data according to their own policy, which we link to from **Settings → Privacy**. If you're using a local model, nothing leaves your machine at all.

## What is never sent anywhere

- Files on your computer that Relay didn't open as part of a mission you started.
- Windows or apps you haven't tracked.
- Keystrokes you type outside of the Relay goal box.
- Your microphone, camera, or any audio.
- Telemetry about how you use Relay. We don't ship Relay with crash analytics or usage analytics turned on. There's nothing phoning home in the background.

If you opt in to send a bug report from inside the app, that report contains the recent log file, your app version, and your Windows version. Nothing else. You see it before it sends.

## What you control

- **You can wipe all local data at any time.** Settings → Privacy → **Clear all Relay data**. This deletes the entire `%APPDATA%\Meterless Relay\` folder. Relay restarts fresh.
- **You can delete a single past goal, plan, or artifact** from the History or Workspace tabs. Right-click, delete. It's gone.
- **You can switch to a different provider** for any reason, at any time. Your local data isn't tied to a provider.
- **You can run a local model** instead of a hosted one. Setup is in **Settings → Models → Local**. We document a few that work well.
- **You can run Relay fully offline** as long as you're using a local model. The desktop control layer doesn't need the internet.

## A note on what we'd like to keep doing

We don't add analytics later as a surprise. If a future release of Relay changes anything about what does or doesn't leave your machine, we'll say so in the changelog, on launch the first time you open that version, and in a paragraph at the top of this page.

If we ever can't keep that promise (say, a future feature genuinely requires sending more data and we can't make it optional), we'll be clear about it and you'll have the choice to update or not.

---

If you have a specific question that isn't answered here, send it to us. The contact info is in the [README](../README.md). We'd rather over-explain than have you wondering.
