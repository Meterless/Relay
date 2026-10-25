# Example goals

These goals are written the way Relay's planner handles best. Copy one, change the names to match your setup, and paste it into **Define → Prompt**. If you're new, read the [getting started guide](../docs/getting-started.md) first.

## What makes a goal compile well

- **Name the windows.** Say "the Q3 Ledger in Excel" or "the vendor portal in Chrome", and **track** those windows before you compile. The planner only knows about windows it can see.
- **Say what to capture and what to call it.** For example: "read every invoice number into a list called `open_invoices`". Named captures can feed later steps, loops and deliverable files.
- **Say where the result goes.** A cell, an email draft, a file name.
- **Mark the point of no return.** Phrases like "stop before sending" or "wait for my approval before submitting" become approval gates. Relay adds gates to sends, submits, deletes and payments by itself anyway, but saying it out loud makes the plan easier to read.
- **One job per goal.** If two jobs are unrelated, make them two missions, then chain them in the queue or a routine.

After you compile, read the plan. Most of these goals compile to between 3 and 6 phases.

---

## 1. Reconcile and draft, then stop for approval

> In the vendor portal in Chrome, open the Open invoices page, select all, and export the CSV. In the Q3 Ledger in Excel, compare each vendor's portal amount with the ledger amount and write "match" or the difference in a new Reconcile column. Then draft an email in Outlook to finance@example.com that lists every mismatch and any vendor missing from the ledger. Stop for my approval before sending.

**Track first:** the portal tab in Chrome, the ledger in Excel, and Outlook.

**What to expect:** an export phase, a reconcile phase that reads and writes the ledger, and a compose phase. A final send phase carries an approval gate. Relay pauses there with the draft on screen, and **Cancel** ends the run without sending anything.

## 2. Do the same thing for every item in a list

> In the Support inbox in Outlook, capture the subject line of every unread email from the last 24 hours as a list called `tickets`. For each ticket, search for its subject in the help desk tab in Chrome and capture the ticket's status. Then write a summary file named `ticket_status` that lists each subject with its status.

**Track first:** Outlook and the help desk tab.

**What to expect:** a capture phase, then a phase that repeats once for each item in `tickets`, up to 50 items. If the list is empty, that phase is skipped instead of failing. A last `save_artifact` step writes the summary file, which you'll find under **Insights → Files**.

## 3. Capture once, reuse in later runs

> Open the pricing page for our Pro plan in Chrome, read the current monthly price, and capture it as `pro_price`.

Then, in a separate mission on another day:

> In the pricing sheet in Excel, type {{vault.pro_price}} into cell B4 on the Competitors tab and save the workbook.

**What to expect:** when a run finishes, Relay copies its captured values into the Data Vault under their names. Empty values and values it had to guess are never stored. The second mission picks up the value with `{{vault.pro_price}}`. **Insights → Data** shows the value and its last few versions. You can also add a **data watch** there that alerts you, or starts another mission, when `pro_price` changes.

## 4. A weekly report on a schedule

> Every Monday: in the analytics dashboard tab in Chrome, set the date range to last week, read the sessions, sign-ups and conversion rate, and add them as a new row at the bottom of the Weekly KPIs sheet in Excel with last Monday's date in column A. Save the workbook.

**Track first:** the dashboard tab and the KPI workbook.

**Compile it without the "every Monday" part,** run it once, and check the results. Then schedule it on the **Schedule** tab: set **Recurrence** to **Weekly**, tick Monday, and set a time. Under **Window readiness**, Relay checks that both windows are open before each run. An optional **Auto-pause after consecutive failures** turns the schedule off if the dashboard changes and the run keeps failing. Remember that schedules only run while Relay is open.

## 5. File downloads by what's inside them

> In File Explorer, open the Downloads folder and capture the names of every PDF added today as a list called `new_pdfs`. For each PDF, open it, read the document type from the first page (invoice, receipt or contract), close it, and move the file into the matching subfolder under Documents\Filed. Ask me before moving anything you can't classify.

**Track first:** File Explorer, opened on Downloads.

**What to expect:** a capture phase, then a loop over `new_pdfs`. Asking "ask me" usually leads the planner to give that phase the *ask you* failure policy. Check the plan for it. With that policy, a failed step pauses with **Retry step**, **Skip step & continue** and **Skip phase** instead of guessing.

## 6. Turn a good run into a zero-cost skill

Take any goal above. Once it has run cleanly, open the **Skills** tab and click **Save as skill** on the **Last run completed** card. Relay suggests parameters, such as the month, the recipient or the folder, and you review them before saving.

Next time you type a similar goal, Define offers **You have a skill for this**. **Run** replays the verified steps with no model calls unless something on screen has changed. If something has, the skill repairs that step and asks you whether to keep the fix.

---

## Contributing an example

If you've built a workflow that others would find useful, open a pull request that adds a Markdown file to this folder. Include:

- the goal text, exactly as you pasted it
- the windows you tracked
- a short description of the plan it produced

Remove account names, client names and real figures first.
