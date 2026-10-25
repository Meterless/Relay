# Frequently asked questions

These are the questions people actually ask, roughly in the order they come up.

## Do I need to know how to code?

No. If you can write an email describing the job, you can use Relay. You describe the workflow in plain language and Relay works out the clicks.

The one setup step is pasting an API key under **Settings → API Keys**, or pointing Relay at a local or self-hosted model. The [getting started guide](getting-started.md) walks you through it.

## Does it work on Mac or Linux?

Not yet. Relay controls apps through native Windows APIs, including UI Automation and Win32 input. Porting that to another OS is a real project, not a switch we can flip. We don't have a date.

If you want to hear when there's news, write to **support@meterless.ai**.

## How much does it cost?

The app is free, released under the [Meterless Permissive Use License](../LICENSE). There's no Relay subscription and nothing is locked.

You pay your model provider directly for model calls, at their rates. Several things keep that low:

- Saved skills replay with no model calls when nothing on screen has changed.
- **Insights → Overview** shows estimated tokens for today and the last 7 days.
- Under **Settings → Data & Alerts** you can set a daily token alert.

To avoid per-token costs altogether, use a local model (a small WebGPU model, a Meterless Runtime, or your own OpenAI-compatible server).

## Is my screen being streamed somewhere?

No. When the model needs to plan, Relay sends the text of your goal and a text description of your windows. Screenshots are sent only for vision checks, and for screen-reading captures. [privacy.md](privacy.md) lists exactly what goes where, including the parts people don't expect.

## Can it mess up my computer?

Relay does what the plan says, and it shows you the plan before anything runs. Phases that send, submit, delete, pay or publish stop at an approval gate and wait for you. Dialogs that sound destructive pause too.

If you give it a vague goal and press Start without reading the plan, though, you can still be surprised. Read the plan the first few times. Leave **Auto approve** off until you trust a workflow.

## What happens when the AI gets something wrong?

There are three safety nets:

1. **You see the plan first.** If a step targets a button that doesn't exist or an app you don't have, you'll spot it and can fix it before anything runs.
2. **Every step gets checked.** After each step, Relay checks the result, using UI Automation first and vision only when needed. It records **pass**, **fail** or **inconclusive**. "Inconclusive" means no check was possible. It's never quietly counted as a pass.
3. **Only clean runs become skills.** Under the default `standard` policy, a run with unchecked critical steps can't become a skill unless you deliberately waive them.

When something does fail, **Explain this failure** in Run results tells you what went wrong.

Verification starts in **Shadow** mode, where it records results but never stops a run. Once results are stable, you can switch to **Enforce** under **Settings → Model Routing → Runtime verification**.

## Which model should I use?

Use something fast and capable for **Desktop Planning**, and a model that can read images for **Vision Analysis**. Both are set under **Settings → Model Routing**. The pickers show a short description of each model and a dot for whether its key is set.

If you want nothing to leave your machine:

- **Local WebGPU models** (Qwen2.5 3B or 7B) handle small text tasks only. Relay won't use them for vision or full plan compiles.
- **A Meterless Runtime** or an **OpenAI-compatible server** on your own hardware can do the full planning job.

## Will my saved missions still work after I restart my apps?

Usually, yes. Saved missions remember which windows they need. Before a run, Relay refreshes the live window list and remaps windows whose IDs changed. Scheduled runs check window readiness first, and wait with a **Fix windows** button if something's missing.

If a plan references a window Relay can't find, the plan panel shows **Fix windows** so you can point it at the right one before you run.

## Can I show Relay instead of describing it?

Yes, in three ways:

- **Record a macro.** On the Macros tab, click **Start recording**, do the job in a tracked window, then click **Stop & save**. You can replay it, chain it with others, turn it into a mission, or distill it into a skill.
- **Live mode.** On the Define tab, switch to **Live** and guide Relay one instruction at a time while it builds the macro.
- **Show Tailor.** Give Tailor a narrated tour of how a process works, and it proposes missions from it.

## How is this different from a macro recorder?

A macro recorder replays a fixed list of clicks. Move one button and it breaks.

Relay does four things a macro recorder doesn't:

- It plans against your desktop as it is right now.
- It clicks controls by name, so moved buttons still work.
- It checks every step and tells you honestly when it couldn't check one.
- It turns runs that worked into skills, which repair themselves when the screen drifts and replay with no model calls when it hasn't.

Recording is one way to feed Relay, not the whole product.

## Can my coding agent use Relay?

Yes. Turn on **Settings → Agent Bridge**, then connect Claude Code, Codex, Cursor, Gemini CLI or any MCP client through the `relay` CLI. You decide what each agent may do, and consequential actions still wait for you. See [agent-bridge.md](agent-bridge.md).

## Can Relay work without taking over my mouse?

For browser work, yes. A **Private Workspace** runs missions in its own browser window, with its own logins, while you keep using your PC. Steps that touch browser menus or system dialogs briefly take the foreground.

Missions on **My Desktop** use your real screen, mouse and keyboard.

## Where do I find my version number?

**Settings → Data & Alerts → App updates** shows "You're on v…". The **Check for Updates** button is there too.

## Where do I get help?

Write to **support@meterless.ai**. Tell us:

- what you were trying to do
- what happened
- your Relay version (shown under Settings → Data & Alerts)
- your Windows version

It also helps to paste the relevant lines from **Settings → System Logs → Copy all**.

For security issues, see [SECURITY.md](../SECURITY.md).
