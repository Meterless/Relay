# Privacy

Most of what Relay does happens on your computer. Some of it doesn't. This page says which is which, as plainly as we can.

## Where your data lives

Relay keeps everything in two folders on your PC:

| Folder | What's in it |
|---|---|
| `%APPDATA%\com.meterless.relay\` | Settings, including your API keys (`settings.json`); macros, skills and verification verdicts; automatic backups; Tailor documents and models; Private Workspace profiles and files; run artifacts; the Agent Bridge discovery file |
| `%LOCALAPPDATA%\com.meterless.relay\EBWebView\` | The app's web storage: mission history, goal history, schedules, the Data Vault, insights, system logs and other app state |

Two more locations come into play only if you use the features behind them:

- **The app itself** installs to `%LOCALAPPDATA%\Meterless Relay\`.
- **Launch debug browser** (in the optional Chrome DevTools tier) uses a separate browser profile at `%LOCALAPPDATA%\MeterlessRelay\cdp-profile`.

**Settings → Data & Alerts → Your data** lists the main kinds of data Relay stores, with their sizes, and lets you view or clear each one. The Data Vault doesn't appear in that list. You manage it under **Insights → Data**.

### A note on API keys

Your keys are stored in `settings.json` in the app data folder. They are **not encrypted** there, so anyone who can read files in your Windows account can read them. Each key is sent only to its own provider, or for the Meterless Runtime and OpenAI-compatible keys, only to the base URL you entered. Keys are never included in a workspace export or backup, and the Agent Bridge can't read them.

## What gets sent to your model provider

Relay calls whichever provider you set up under **Settings → API Keys** and **Model Routing**. That could be Google, Anthropic, OpenAI, OpenCode Go, OpenRouter, a Meterless Runtime, or an OpenAI-compatible server you point it at. The provider handles that data under its own policy.

**When you compile a mission**, the request can include:

- The text of your goal.
- A short research request about the goal, sent to your Deep Reasoning model. If that model is Gemini, it can run a Google Search.
- A text description of your desktop: the title, program name and size of each **tracked** window, plus the **top 10 open windows** on your screen, whether you track them or not. A mission that runs in a Private Workspace leaves out your desktop windows entirely.
- Short summaries of procedures that worked before (procedural memory).
- Up to 12 Data Vault entries, each shortened to its first 80 characters.
- A compact summary of Relay's world model of your apps and sites.
- Your Tailor org summary, but only for missions that came from Tailor, or if you turned on **Inject the org matrix into ordinary Define compiles**.

**While a mission runs**, a few kinds of step can send screen content:

- **Capturing data** sends the text or a screenshot of the window being read, so the model can pull out the values you asked for.
- **Vision checks**, and **Vision click fallback** if you turned it on, send a screenshot of the window being checked.
- **Modal dialog handling** sends the dialog's title, text and button labels. If vision click is on and the dialog has no readable text, it sends a screenshot instead.
- **Self-repair, macro healing and skill repair** send the failing step and what's on screen around it.

**When you ask for it:**

- **Enhance** and **Refine** send your plan.
- **AI explanation** sends the short failure summary, not your raw logs. **Explain this failure** on its own never calls a model.
- **Tailor's Analyze** sends chunks of your documents to your planning model. It shows an estimated cost before anything is sent, and skips collections marked local-only. Turn off **Allow cloud synthesis** under Settings → Model Routing → Tailor, and document text never leaves your machine.

Relay doesn't stream your screen. It doesn't scan your files. It only records your keystrokes while you're recording a macro, and then only keys pressed in tracked windows.

If you use a local WebGPU model or a Meterless Runtime set to local-only modes, those calls stay on your machine or your network.

## Other network traffic

- **Update checks.** At launch, at most once a day, Relay sends a request to `meterless.ai/Installers/` to see whether a newer installer exists. Your data isn't part of that request. Downloading an update only happens when you click **Update now**.
- **Local models.** The first time you pick a local WebGPU model, Relay downloads the runtime and the model weights (several GB) from `esm.run`, `cdn.jsdelivr.net` and Hugging Face.
- **Reading PDFs in Tailor** loads the PDF reader from `cdn.jsdelivr.net`. Your documents aren't uploaded anywhere.
- **The Agent Bridge** listens only on `127.0.0.1`, so nothing on your network can reach it.

## What this version doesn't do

- **No usage analytics or crash reporting.** Relay 0.8.8 has no telemetry. If that ever changes, we'll say so in the changelog and on this page first.
- **No uploading of your data.** Missions, captures, history and artifacts stay in the folders above.
- **No passwords in macros.** Values in macros that look like passwords can be masked, and you can type them yourself at replay time. Private Workspaces keep only account *labels*, never passwords.

## Things worth knowing

- **Relay uses your clipboard.** Reading a window's text works by focusing the window and sending Ctrl+A, Ctrl+C, so it replaces whatever was on your clipboard.
- **Typed text is never logged in full.** The action journal records how many characters were typed, with masked secrets hidden. The Agent Bridge logs only the length of what an agent typed.
- **A debug port is open to your whole PC.** With the optional Chrome DevTools tier, and inside Private Workspaces, the browser listens on a local debug port. Any program on your computer that knows the port can drive that browser. Nothing on your network can reach it.

## What you control

- **Clear a kind of data** under Settings → Data & Alerts → **Your data**. Settings can't be cleared there. Clear Data Vault entries under Insights → Data.
- **Take your data with you** using **Export workspace** (API keys are left out), or bring it back with **Restore from backup**.
- **Clear the system logs** with **Clear logs** under Settings → **System Logs**.
- **Forget what Relay learned** with Insights → Memory → **Forget this procedure** or **Clear all**.
- **Switch providers any time.** Nothing you've saved is tied to a provider.
- **Start completely fresh.** Close Relay, then delete the two folders listed at the top of this page.

---

Questions this page doesn't answer: write to **support@meterless.ai**.
