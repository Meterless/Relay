# What Relay can do

This is a tour of the app, organized by what you're trying to get done. Button and tab names are written the way they appear in Relay. If you're brand new, start with [getting-started.md](getting-started.md).

**Contents**

- [Turn a sentence into a plan you can read](#turn-a-sentence-into-a-plan-you-can-read)
- [Point Relay at the right windows](#point-relay-at-the-right-windows)
- [Run it on real apps](#run-it-on-real-apps)
- [Know whether it actually worked](#know-whether-it-actually-worked)
- [Stay in control of risky steps](#stay-in-control-of-risky-steps)
- [Get data out and reuse it](#get-data-out-and-reuse-it)
- [Run it later, or on its own](#run-it-later-or-on-its-own)
- [Teach by showing: macros and Live mode](#teach-by-showing-macros-and-live-mode)
- [Make it cheap and repeatable: skills](#make-it-cheap-and-repeatable-skills)
- [See what happened: Insights](#see-what-happened-insights)
- [Turn your documents into missions: Tailor](#turn-your-documents-into-missions-tailor)
- [Work off-screen: Private Workspaces](#work-off-screen-private-workspaces)
- [Let a coding agent drive: Agent Bridge](#let-a-coding-agent-drive-agent-bridge)
- [Choose your models](#choose-your-models)
- [Find anything fast](#find-anything-fast)
- [Own your data](#own-your-data)
- [Stay up to date](#stay-up-to-date)

---

## Turn a sentence into a plan you can read

You type the job in the **Define** tab and press **Compile Mission**. Relay looks at the windows you track, adds what it already knows, and writes a structured mission plan. What it already knows includes past procedures that worked, values earlier runs captured, and its world model of your apps. Before it plans, Relay runs a short research pass with your Deep Reasoning model, which uses Google Search when that model is Gemini.

The plan is grouped into **phases** and **steps**. Each step has an action, a target window, and a check for afterwards. Each phase has a failure policy: retry, skip, abort, or ask you. Nothing has run at this point.

In the **Compiled Mission Plan** panel you can:

- **Edit any step inline.** You can also edit a step's raw JSON. **Undo** and **Redo** step through your changes.
- **Enhance** the whole plan. Relay compares the plan with your original goal, then shows a before-and-after summary of its suggested improvements before anything changes.
- **Refine** only part of it. Highlight phases or steps, describe what should change, and only those parts are rewritten.
- **Fix windows** when a step refers to a window you haven't tracked. Relay maps it to one that's open.

Plans are checked before they're saved. If a step can't run as written, you're told which one and why.

## Point Relay at the right windows

The **Desktop Control** panel, on the **My Desktop** tab, is where you choose which windows Relay may use.

- **Available Windows** lists the open windows. Select some and click **Track (N)**. **All OS** / **Focused** switches between every window and just your picks. **OS** refreshes the list.
- **Active Sessions** shows the windows you're tracking, each with **Focus**, **Mirror** (a live preview through Windows screen sharing) and an **X** to stop tracking.
- **Capture** adds a standalone screen share. **STOP ALL** ends every session.
- The center preview has four layouts: **Z-index** (stacked like your real desktop), **Spread**, **Grid** and **Focus** (one large window with thumbnails beside it).

Saved missions remember which windows they need. If a window ID has changed since then (because you restarted the app, say), Relay remaps it before it runs.

## Run it on real apps

Relay drives your apps with real Windows input: focus, clicks, typing, key chords, scrolling and navigation.

- **Clicks target controls by name.** When a step says "click Send", Relay finds the control with that name in the Windows accessibility tree. A button that moved doesn't break the step.
- **Vision click fallback** is optional. Turn it on under Settings → Model Routing → Automation tiers. Some custom apps, canvas apps and games don't expose names. With this on, Relay finds the control in a screenshot with your vision model instead. It costs tokens and needs a Mirror on that window.
- **The Chrome DevTools Protocol tier** is also optional, and also lives under Automation tiers. In a Chromium browser started with a debug port, Relay gets a real page-load signal and clean page text instead of copying from the screen. It's off by default, and Relay can launch a debug browser with a separate profile for you.
- **Waits show a countdown** with **Continue now**. **Stop** and **Pause** take effect straight away, even mid-wait.
- **For-each loops.** A phase can repeat for every item in a list an earlier step captured, such as each row, each file or each email. That's up to 50 items, and an empty list simply skips the phase. In the step editor, the current item appears in the variable picker under **Loop**.

## Know whether it actually worked

After a step runs, Relay can check that it did what it should. It uses a free UI Automation check first, and vision only when needed. Every step gets a verdict:

| In Run results | Meaning |
|---|---|
| **pass** | The check ran and the screen matched |
| **fail** | The check ran and the screen didn't match |
| **inconclusive** | No check was possible. It's shown honestly, never counted as a pass. |
| **skipped** | The step was skipped |

**How strict runs are:** Settings → Model Routing → **Runtime verification**.

| Mode | Behavior |
|---|---|
| **Off** | No checks |
| **Shadow** (default) | Checks are logged but never fail a run |
| **Enforce** | A failed check fails the step |

Once shadow results have been stable for long enough, a **Promote to Enforce** button appears.

**How strict skills are:** a separate *verification policy* decides whether a run counts as clean enough to become a skill.

| Policy | Rule |
|---|---|
| `standard` (default) | Every critical step must pass, or be waived by you on purpose |
| `strict` | No waivers |
| `lenient` | Only a failed step blocks it |

You can set the policy per schedule, and when you review a skill before saving it.

When something fails, **Explain this failure** builds a short summary of what went wrong, locally and without a model call. **AI explanation** sends just that summary to your model for a plain-English read. **Export run report** saves the run as JSON.

## Stay in control of risky steps

- **Approval gates.** Phases that send, submit, delete, pay or publish stop at **Approval Required** until you click **Approve & run phase** or **Cancel**. **Auto approve** in the plan panel skips gates while it's ticked, so leave it off for anything important.
- **Ask-me failures.** A phase can be set to ask you when a step fails. You then get **Retry step**, **Skip step & continue**, **Skip phase** and **Cancel**.
- **Modal dialog handling.** When a dialog the plan didn't expect appears (Save As, "unsaved changes", a confirmation, a browser pop-up), Relay reads its text and buttons, completes or dismisses it to fit the goal, and continues. Dialogs that sound destructive, or that it can't decide on safely, pause with **A dialog is in the way**. Choose **Automatic**, **Ask me** or **Off** under Settings → Model Routing → Automation tiers.
- **Secrets in recordings.** Macros can mask values that look like passwords (**Scan secrets** finds them). When you replay, you can type a masked secret yourself instead of storing it.

## Get data out and reuse it

- **Captures.** Steps can read text from a window or page and save it under a name, called a storage key. Later steps in the same run use it as `{{storage_key}}`.
- **Data Vault.** When a run finishes, its captured values are saved under their storage keys and kept beyond the run, along with their last few versions. Empty values and values Relay had to guess are never saved. Any later mission can use one as `{{vault.<key>}}`, and the planner sees a short list of what's in the vault when it plans. You can browse, copy or delete values under **Insights → Data**.
- **Deliverable files.** A `save_artifact` step writes a real file built from captured data, such as a report, a summary or code a run collected. Relay picks the file type from the content: HTML, JSON, Markdown, code or plain text. Files runs produce are listed under **Insights → Files**, with **Open with the default app** and **Show in folder**.
- **Workspace files.** Missions in a Private Workspace save what they gather as files in that workspace, and later runs can reuse them as `{{workspace.<key>}}`.

## Run it later, or on its own

**Schedules** (the **Schedule** tab):

- **Once**, **Daily**, **Weekly** (tick the days) or **Monthly** (pick the day of the month), with optional end dates and run limits.
- **Window readiness.** Before each run Relay checks that the windows it needs are open. It can reopen a URL, or wait and show **Waiting for window** with a **Fix windows** button.
- **If a run is missed** because Relay was closed, you choose between **Run it as soon as Relay opens** and **Skip to the next scheduled occurrence**.
- **Auto-pause after consecutive failures.** You pick the number. The schedule turns itself off and alerts you.
- **Skip if busy**, plus a per-schedule verification policy.
- Schedules made from a macro can **recompile from the current recording** before each run.
- Schedules only run while Relay is open.

**Watches**:

- **A schedule can watch a captured value** and alert you when it changes, starts or stops containing some text, or when a number goes up or down. It can also run a macro, skill, mission or routine when that happens. The first run only records a starting value.
- **Data watches** (**Insights → Data**) do the same for any Data Vault key, whichever run updates it.
- Anything a watch starts goes into the queue. It never interrupts a run already going.

**Mission queue and routines** (**Insights → Queue** and **Routines**):

- Line up missions, macros and skills, then click **Run queue**.
- Each item can run **always**, **if prev ✓** (only after the previous item succeeded) or **if prev ✗** (only after it failed).
- **Stop on failure** and **Stop after current** let you end a queue early.
- **Save as routine** keeps the lineup so you can run it, queue it, or schedule it daily.

## Teach by showing: macros and Live mode

**Macros** (the **Macros** tab):

- **Recording.** Click **Start recording** (you need a tracked window first), do the job, then **Stop & save**. Steps are anchored to UI elements rather than screen coordinates.
- **Replay.** **Replay** lets you set the speed and parameters. **Heal drifted steps** is on by default: if a target has moved, Relay makes one small vision correction and offers it as a new revision.
- **Preview** is a dry run. It checks that every window and element can be found right now, without sending any input.
- **Chain.** Tick two or more macros and chain them into a single mission.
- **Timeline** is a revision-tracked step editor. You can reorder steps, add waits, add approval points, turn values into parameters, and mask secrets.
- Other buttons: **To mission** (turn a recording into a plan), **Schedule**, **Queue**, and **Distill to skill** after a good replay.
- Each recording shows a health label (healthy, drifting, broken or unrun) and a fidelity score.

**Live mode** (**Define → Live**, or **LIVE** on a tracked window's card):

- Start a live session on one window and tell Relay what to do next, one instruction at a time.
- **Observe** lets it look before acting.
- When you're done, **Finalize Macro** turns the session into a macro you review before saving. It can also become a skill draft.

## Make it cheap and repeatable: skills

A **skill** is a verified run saved with parameters, for example `month` or `recipient`.

- **Saving.** After a clean run, the Skills tab offers **Save as skill**. Relay suggests parameters, and you review them before anything is saved. A macro replay can do the same with **Distill to skill**.
- **Replaying.** When nothing on screen has changed, a skill replays with **zero LLM calls**. When something has drifted, it repairs the step and asks you to **Keep + new version** or **Discard fix**.
- **Stats.** Each skill card shows **DER** (the share of steps that ran with no model call), cost per run, repairs, number of runs, and version.
- **Suggestions.** When a new goal matches a saved skill, Define shows **You have a skill for this**, with **Run** and **Queue**.

**Procedural memory** is separate from skills. Relay automatically notes which procedures worked in which apps, and feeds the best matches to the planner as "you've done this before" hints. You can review it, and forget entries one at a time or all at once, under **Insights → Memory**.

## See what happened: Insights

The **Insights** tab has eight sections. Everything in it is computed locally.

| Section | What's there |
|---|---|
| **Overview** | Runs, pass rate, verdicts, estimated tokens today and over 7 days, repairs, enforcement readiness, pass rate by day, flaky and most-failing steps (with **Re-run**), skill DER and cost, macro health, and run report export |
| **Queue** | The mission queue |
| **Routines** | Saved lineups |
| **Data** | The Data Vault and data watches |
| **Journal** | A per-run record of what changed: windows that appeared or closed, where it navigated, how many characters it typed (secrets masked), and which steps were consequential. It can be filtered to runs you started or runs started by agents. |
| **Alerts** | Run results, schedule starts and waits, auto-pauses, watch triggers, skill suggestions, token-threshold alerts, and a "while you were away" digest |
| **Memory** | Procedural memory |
| **Files** | Files runs produced |

The Insights tab shows a red dot when there are unread alerts. To get Windows notifications when Relay is in the background, or an alert when the day's estimated token use passes a threshold, go to **Settings → Data & Alerts → Notifications & cost alerts**.

## Turn your documents into missions: Tailor

Open **Tailor** with the scissors icon in the header. The badge counts mission candidates that are ready.

- **Add knowledge.** Drop in documents, folders or zip files, or paste text. You can also import an export of your **Claude or ChatGPT history**: Tailor scores each conversation, keeps the ones that describe real work, and tells you why it skipped the rest.
- **Tell** it how something works, by typing or dictating.
- **Show** it with a narrated tour: Relay notes the apps you visit while you talk.
- **Learn from what you do.** It can learn from your saved macros and the missions you repeat. You can switch this off.
- **What it builds.** Tailor maps your processes, systems and vocabulary into an org model, flags contradictions between documents, and proposes **mission candidates**. For each candidate you can **Walk it** step by step, **Test**, **Run now**, **Save as skill**, **Schedule** or **Queue**.
- **Keeping it local.** A collection can be marked local-only. With **Allow cloud synthesis** off (Settings → Model Routing → Tailor), document text never leaves your machine. Before an **Analyze** pass sends anything, Tailor shows an estimated token cost.

## Work off-screen: Private Workspaces

Switch the Desktop Control panel to **Private Workspace** and create one with **New Private Workspace**. You give it a name, pick a detected Chromium browser, and choose whether it keeps logins between runs.

- **Missions run in the workspace's own browser window**, with logins, cookies and downloads separate from yours. You keep your screen and mouse, except for steps that touch browser menus or system dialogs. It is not a security sandbox, and it can't run shell commands.
- **Your computer stays off-limits by default.** Anything that needs a file or window on your desktop asks first: **Allow once**, **Allow for this mission**, **Always allow** or **Deny**.
- **Accounts are labels only.** Passwords are never stored. When a step needs one, Relay pauses so you can type it.
- **It repairs itself mid-run.** If the page crashes or the browser closes, the workspace reloads or relaunches. A workspace that stops answering shows **Not responding** with a **Repair** button.
- **Scheduled workspace missions** run only while Relay is open.

## Let a coding agent drive: Agent Bridge

Settings → **Agent Bridge** lets Claude Code, Codex, Cursor, Gemini CLI or any MCP client control Relay, through the `relay` CLI or `relay mcp`.

- It only listens on your own computer, and uses a token that rotates.
- You set a tier for each agent: **observe**, **act** or **autonomous**.
- Consequential actions still wait for you.

There's a full guide in [agent-bridge.md](agent-bridge.md).

## Choose your models

- **Hosted providers** (Settings → API Keys): Google (Gemini), Anthropic (Claude), OpenAI (GPT), OpenCode Go (open models) and OpenRouter (many vendors). Keys are checked with **Verify**.
- **Per-task routing** (Settings → Model Routing): separate models for **Desktop Planning**, **Vision Analysis** and **Deep Reasoning**. The picker at the top of the right sidebar overrides them for a while without changing your settings.
- **Meterless Runtime.** Point Relay at a local-first Meterless router on this PC or your network. You can use **Auto Detect**, or paste a connect link. Then you choose *modes* (Auto, Deep, Fast, Local, Vision and others) instead of models. **Auto-set to Meterless Runtime** routes all three tasks in one click.
- **OpenAI-compatible endpoint.** Any server that speaks `/models` and `/chat/completions`: vLLM, LM Studio, llama.cpp, LiteLLM, a company gateway. **Discover models** lists what it serves, and the ones you pick show up as `compat/<id>`.
- **Local WebGPU models.** Qwen2.5 3B and 7B can run inside Relay on your GPU (about 2.5 GB and 5 GB). They download on first use and are opt-in. They only handle short text tasks: Relay won't send them vision, web search, full plan compiles or long inputs. They're not a replacement for a full planning model.
- **Retries and usage.** Failed model calls retry automatically, and estimated token use is tracked under Insights.

## Find anything fast

Press **Ctrl+K** anywhere to open the command palette. From there you can:

- jump to a tab
- run or queue a recent mission, a skill or a macro
- run a schedule now
- run the queue or a routine
- switch between My Desktop and a workspace
- reach every Tailor action

All shortcuts are in [shortcuts.md](shortcuts.md).

The **World Model library** (the globe icon in the header) shows the local map Relay keeps of the programs, sites, windows and elements it has seen. It's what helps Relay cope when windows change.

## Own your data

Everything lives on your machine. **Settings → Data & Alerts** shows it all:

- **Workspace backup & restore.**
  - **Export workspace** saves one file with your macros, skills, mission history, schedules, verdicts, procedural memory and world model. API keys are never included.
  - **Restore from backup** merges a backup into what you have.
  - **Automatic backups** are snapshots taken on launch and on a timer, with **Back up now** and **Restore**.
- **Your data.** The main kinds of data Relay stores, such as macros, skills, history, schedules, verdicts, memory, logs, the journal and Tailor, each with its size. You can view each one as raw JSON or clear it.
- **System Logs** (its own Settings tab). Recent errors and warnings, with **Copy all** and **Clear logs**.

How data moves is covered in [privacy.md](privacy.md).

## Stay up to date

Relay checks for a new build at launch, at most once a day. **Update now** downloads the update, checks its signature, installs it and restarts Relay, and only happens when you click it. You can also check by hand, and see your version, under **Settings → Data & Alerts → App updates**.

The changes in each release are in the [changelog](../CHANGELOG.md).
