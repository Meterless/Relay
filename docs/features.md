# What Relay can do

This is the user-facing tour of the app. It's organized by what you're trying to get done, not by what's happening under the hood. If you want the architectural version, the project README in the source repository has it.

## Turn a written instruction into a real workflow

You type what you want done. Relay writes a plan. You look at the plan. You run it. That's the core loop.

The instruction can be specific (*open Outlook, find the most recent email from Alex, forward it to Sam with a one-line note*) or it can be loose (*do the morning report*). When it's loose, Relay leans on what it's learned from past runs to fill in the blanks. When it's specific, Relay follows it more literally.

Plans are shown to you in plain English before any clicks happen. You can cancel at that step with no harm done.

## Pay attention to specific windows

Relay does its best work when you've told it which windows on your desktop matter. You can track up to eight windows at once. Each tracked window gets a stable identity, so Relay refers to it the same way today as it did yesterday, even if you closed and reopened the app.

This is also what fixes the problem most automation tools have with two windows that have the same title. Relay knows them apart at the OS level.

## Verify with screenshots between steps

After Relay clicks something important, it can take a screenshot and look at it before moving on. If the screen doesn't look the way it expected, it pauses and tells you what's off.

You don't have to configure this. It's on by default for steps the planner considers risky (anything that sends, saves, modifies, or deletes). You can turn it off per mission if you're running something you've already seen succeed a hundred times and you want it to fly.

## Pause for your approval before sensitive actions

Some steps shouldn't run without you watching. Sending an email. Submitting a payment. Posting publicly. Anything you'd want one last look at.

Relay marks these as approval gates. When a plan reaches one, the app pings you, shows you a screenshot of exactly what's about to happen, and waits. You click continue or cancel. Nothing happens in the meantime.

You can mark any step in a plan as an approval gate by hand, even ones Relay didn't flag itself.

## Capture what shows up on the screen

When a workflow produces something useful (an extracted table, a generated file, a vision read of a chart), Relay saves it into a workspace. You can scroll back through everything it has ever pulled off your screen for you, by mission.

The workspace holds the last 200 captures. Older ones get rolled off, but you can pin anything you want to keep around.

## Remember workflows so the next run is faster

Every time a mission succeeds, Relay quietly takes notes. Which apps were involved. What the goal looked like. Which steps were doing the real work.

The next time you ask for something similar, that note gets pulled in before the planner writes the new plan. The practical effect is that your second, third, and fourth runs of a similar workflow are shorter and faster. You don't have to do anything to turn this on.

You can browse and delete remembered procedures from the **Memory** tab if you want to start fresh on something.

## Search the web before planning, when it helps

For goals where context matters (*find the current support email for company X and open a draft to them*), Relay can do a quick web search before it writes the plan. This is only on when the model you're using supports it. Gemini does it natively. The setting is in the per-mission options.

You'll see "Researched the web" as one of the early phases in the plan when this happens.

## Record what you do and play it back

If you can't describe what you want, you can show it. Click **Record** in the toolbar. Do the thing on your screen. Click **Stop**. Relay watches and writes a mission plan based on what it just saw you do. You can then run that mission on its own, or use it as the starting point for a similar one.

This is the fastest way to teach Relay something that's easier to demonstrate than to describe.

## Mix and match AI providers per phase

You don't have to commit to one model. You can have Gemini do the web research, Anthropic do the planning, and a local lightweight model do the vision checks, in the same mission. Settings are in **Model routing**.

Most people leave the defaults alone. If you're doing high volume work and want to optimize for cost or speed, this is where to tune.

## Replay any past goal or plan

Every goal you've typed is saved (last 100). Every plan Relay has written is saved (last 80). You can scroll through them with the up and down arrows in the goal box, or open the **History** tab to see them all with timestamps.

Click any past plan to load it. Click run to do it again. Click edit to fork it as the starting point for a new mission.

## Run the same mission across multiple windows

If your workflow needs to touch the same kind of window in several places (three Chrome tabs, two open spreadsheets, four CRM accounts), you can track them all and write one mission that handles them together. Relay keeps the windows distinct and won't confuse the data.

## Keep everything local

Your tracked windows, your past goals, your past plans, your procedural memory, your captured artifacts. All of it lives in a folder on your computer. The only thing that leaves the machine is what gets sent to whichever AI provider you've configured, and you can see exactly what that is in the **Privacy** tab. There's a whole page about this in [privacy.md](privacy.md).

---

If something in here sounds interesting and you want to try it, the [getting started guide](getting-started.md) is the fastest way to feel any of this work in practice.
