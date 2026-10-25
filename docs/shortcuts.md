# Keyboard shortcuts

Relay is mostly a point-and-click app, but there are a few keys worth knowing. This page lists every shortcut the app actually handles, and where each one works.

Some things to know up front:

- **There are no global hotkeys.** Every shortcut below works only while the Relay window has focus. None of them reach Relay from another app.
- **Shortcuts can't be remapped.** There's no keybindings screen.
- **There's no stop key.** To stop a run, use **Stop** in the Compiled Mission Plan panel, or **STOP ALL** at the top of the Desktop Control panel.

## Anywhere in the app

| Keys | What it does |
|---|---|
| **Ctrl+K** | Opens or closes the command palette. It works even while you're typing in a text box. |

### Inside the command palette

| Keys | What it does |
|---|---|
| **↑ / ↓** | Move through the results |
| **Enter** | Run the selected command |
| **Esc** | Close the palette. Clicking outside it also works. |

From the palette you can:

- jump to any tab: Define, Schedule, History, Macros, Skills or Insights
- open Settings, the World Model library or Tailor
- run or queue a recent mission, a macro or a skill
- run a schedule right now, run the mission queue, or run a routine
- switch new missions between My Desktop and a Private Workspace, and start or stop a workspace
- use any Tailor action, including walking a ready mission candidate

## The goal box (Define tab → Prompt)

| Keys | What it does |
|---|---|
| **Enter** | Compile the mission. This does the same thing as **Compile Mission**. |
| **Shift+Enter** | Start a new line in your goal |
| **Ctrl+↑** | Bring back an older goal from your history |
| **Ctrl+↓** | Move toward newer goals. Going past the newest brings back the draft you were writing. |
| **Esc** | Stop dictation (only while **Speak** is listening) |

The hint above the goal box shows these, plus how many goals you've saved.

## Live mode command box (Define tab → Live)

| Keys | What it does |
|---|---|
| **Enter** | Send the command |
| **Shift+Enter** | New line |
| **Ctrl+↑ / Ctrl+↓** | Older and newer commands from your history |
| **↑** with the cursor at the very start, **↓** with it at the very end | Also step through history |
| **Esc** | Stop dictation while it's listening |
| **Enter** in the "Label this target…" box | Save the label for a point or region you just picked |

## Compiled Mission Plan panel

### Refining part of a plan

Click **Refine** to turn on selection mode, then:

| Keys or mouse | What it does |
|---|---|
| Click or drag across phases and steps | Highlight them |
| **Ctrl+click** | Add or remove a single item |
| **Enter** | Open the refine dialog for what you highlighted |
| **Esc** | Clear the highlight. Press it again with nothing selected to leave selection mode. |

These keys don't fire while your cursor is in a text field.

### Refine dialog and result windows

| Keys | What it does |
|---|---|
| **Ctrl+Enter** | Run the refine (in the refine dialog), or apply the result (in the refine or Enhance result window) |
| **Esc** | Close the dialog, or throw away the result |

### Editing a step

| Where | Keys | What it does |
|---|---|---|
| A short value field | **Enter** / **Esc** | Save / cancel. Clicking away also saves. |
| A long value field | **Ctrl+Enter** / **Esc** | Save / cancel. Plain Enter adds a new line. |
| The raw step JSON editor | **Ctrl+Enter** / **Esc** | Apply (only if the JSON is valid) / cancel |
| The raw step JSON editor | **Tab** | Insert two spaces, instead of moving to the next field |
| An action or variable picker | **Enter** / **Esc** | Pick the first match or the value you typed / close the picker |
| A selected parameter chip | **Enter** | Open its editor |

### While a run is going

The plan scrolls along with whichever step is running. Pressing **↑, ↓, Page Up, Page Down, Home, End** or **Space** inside the plan stops that auto-scrolling, so you can read in peace. The keys don't do anything else.

## Smaller places

| Where | Keys | What it does |
|---|---|---|
| Model pickers (Settings → Model Routing, and the routing override at the top of the right sidebar) | **Esc** | Close the dropdown |
| Private Workspace → **New Private Workspace** name box | **Enter** / **Esc** | Create / cancel |
| Settings → API Keys → Meterless Runtime connect-link box | **Enter** | Connect |
| Settings → API Keys → OpenAI-compatible endpoint model ID box | **Enter** | Add the model |
| Tailor → Tell | **Ctrl+Enter** | Add what you wrote and keep the panel open |
| Tailor → tour note box | **Enter** | Add the note |
| Tailor walkthrough, editing a step | **Enter** / **Esc** | Save / cancel |
| Guidance tips (the welcome card and the coachmarks) | **Esc** | Dismiss |

## The intro animation

The intro skips itself after a few seconds. To skip it sooner, click anywhere or press **Skip intro**. **Esc**, **Enter** and **Space** also skip it, but only once the intro has keyboard focus, so clicking is the reliable way.

## Not supported

Some windows don't close with **Esc**, including Settings, the Macro library and the World Model library. Use their **X** button.
