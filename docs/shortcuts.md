# Keyboard shortcuts

The handful of shortcuts that actually make a difference, listed in roughly the order you'll want to learn them. All of these are configurable in **Settings → Keybindings** if any of them clash with something else you use.

## The two you'll use every day

**Ctrl+Enter** — Run the plan that's currently in the inspector. Same as clicking the **Run** button, but you don't have to take your hands off the keyboard.

**Ctrl+Shift+Esc** — Global emergency pause. *(confirm before publishing)* This works even if Relay isn't the focused window. If a mission is running and you need it to stop right now, this is the one. It pauses cleanly between steps rather than killing the process, so the next time you hit Continue it picks up where it left off.

## In the goal box

**Up arrow** (with an empty composer) — Scroll back through the last 100 things you asked Relay to do. Press it again to keep going further back.

**Down arrow** — Come back toward the present. Eventually you're back to a blank composer.

**Ctrl+L** — Clear the composer. Faster than selecting and deleting.

**Ctrl+R** — Pull up the last successful plan and rerun it without retyping the goal. Useful for "do the thing I just did, again."

**Shift+Enter** — New line inside a goal. Plain Enter sends. We're aware some apps do this the other way around.

## Tracking and inspecting windows

**Ctrl+T** — Open the "track a new window" picker. The list is sorted by most-recently-focused, so the window you just had open is at the top.

**Ctrl+1 through Ctrl+8** — Jump to tracked window 1 through 8. The preview in Relay scrolls to it and the underlying native window comes to the front.

**Ctrl+Shift+1 through Ctrl+Shift+8** — Take a fresh screenshot of that tracked window without running anything. Useful for confirming what Relay sees right now.

**Ctrl+Backspace** (with a tracked window selected) — Stop tracking it. Doesn't close the underlying app.

## During a run

**Space** — Pause the current mission. Press again to resume. This is the polite version of Ctrl+Shift+Esc. Use it when you have time to wait for the current step to finish.

**Ctrl+→** — When the run is paused at an approval gate, this is "continue." Same as clicking the Continue button.

**Ctrl+←** — When paused at an approval gate, this is "cancel the rest of the mission." The work done so far is saved. Nothing further runs.

**Ctrl+S** (during a run) — Snapshot the current desktop state. Saves a record of every tracked window's current contents to your workspace. Good for "I want to come back to this exact moment later."

## Moving around the app

**Ctrl+1 through Ctrl+4** (with Alt held, so **Ctrl+Alt+1** etc.) — Switch between the main tabs: Workflow, Workspace, History, Settings.

**Ctrl+F** — Search inside the current tab. In Workspace, it searches captured artifacts. In History, it searches past goals and plans.

**Ctrl+,** — Open Settings. Standard Windows convention.

**Ctrl+Q** — Quit Relay. Will ask first if a mission is mid-run.

## Power-user moves

**Hold Shift while clicking Run** — Run the current plan in dry-run mode. Relay walks through every step and tells you what it would have done, without actually clicking or typing anything. Best way to inspect a complicated plan you don't fully trust yet.

**Hold Ctrl while clicking a past plan in the History tab** — Fork it. Opens a new editable copy of the plan so you can change a step or two before running, instead of running it as-is.

**Double-click a tracked window's thumbnail** — Pop it out into its own resizable preview window. Useful on a multi-monitor setup where you want to watch what's happening on your second screen.

**Right-click a step in the plan inspector** — Mark it as an approval gate, or change its failure policy (continue, retry, halt). You don't have to memorize this; the menu is self-explanatory once you open it.

---

If you change any of these in **Settings → Keybindings** and then want to get back to the defaults, there's a **Restore defaults** button at the bottom of that page that does exactly what it says.
