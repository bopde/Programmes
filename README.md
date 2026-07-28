# Programme Manager

A single-file, locally hosted budgeting and programme management app — a "Notion-light database tool with a budgeting addition". No installation, no server, no dependencies: open `index.html` in a desktop browser (Chrome or Edge recommended).

1. Getting started
   a. Open `index.html` in your browser (double-click the file).
   b. Enter a programme name on the start screen — each programme is a separate instance.
      i. Data autosaves to the browser as you type (see the "Saved" stamp in the header).
      ii. Every programme created on this computer is listed on the start screen.
      iii. A "Welcome & guide" page is created as the first Notes page of every programme — a friendly, in-app version of this README. Delete it whenever you like (it behaves like any other Notes page).
      iv. Switch or combine programmes from the dropdown beside the programme name: pick another programme to jump to it, or pick "All programmes (overview)" for a read-only, unified roll-up.
         1. The overview gives one budget across every programme (per-programme subtotals plus a grand total), one calendar showing every programme's events and due/completed actions, and one action list grouped under each programme's name.
         2. Switch back to any single programme to edit it.
   c. Use 💾 Save to write a portable `.programme.json` file, and 📂 Open to load one.
      i. The `.json` file is plain structured text — drop it (or the 📝 Markdown snapshot) straight into an AI model for analysis and interrogation.
      ii. Ctrl/Cmd-S also saves.
   d. Use 📥 Data for a spreadsheet round-trip of contracts and financial data.
      i. Download current data (opens in Excel), edit or add rows, save as CSV, and re-upload — this replaces the old fixed import template. `import-template.csv` remains a worked example of the format.
      ii. One row per item, ordered contract → po → line → invoice, matched on contract/PO/line/invoice numbers — re-uploading updates existing items instead of duplicating them.
      iii. A `po` row with a blank `contract_number` becomes a standalone PO; put its supplier in the `supplier` column. Contracts also carry a `what` (contract name) column.
      iv. If a file has no recognised `type` column (e.g. a report exported from elsewhere), the importer now says so clearly instead of silently doing nothing.
   e. Data entry: Tab moves to the next field, Enter moves down the column (Excel-style), and long text fields wrap as you type.
      i. PO lines can be copied (⧉) and pasted (📋) whole — the target keeps its own line number.
      ii. Tab-separated values pasted from Excel fill across a PO line row, or across consecutive forecast periods.
      iii. Contracts, POs, PO lines, forecast lines, tasks and links can be reordered by dragging their ⠿ handle (within their own group).
      iv. Contracts and POs fold/unfold (▼/▶) so long lists stay manageable.
   f. Customise in ⚙ Settings: task states, task priorities, task tags, calendar tags and forecast statuses.
   g. 🗑 Trash — deletes are recoverable. Deleting a contract, PO, PO line, invoice, forecast line, task, event, notes page or link moves it to the Trash (last 50), where it can be restored or permanently purged.
2. Tabs
   a. Budget
      i. Overview — a read-only summary with one row per contract and per standalone PO (no double-counting): for what, supplier, contract #, PO #s, line count, original budget, variations, current value, end date, actuals, remaining. The "For what" column shows the contract's name (falling back to the contract number so a row is always identifiable). Nothing is edited here; → jumps to the detail, and the templated/custom views and archived filter still apply.
         1. Time and dropdown filters (the same controls as Forecast & phasing): filter by supplier, contract # or WBS, and tick "in FY" to scope the Actuals column to a financial-year window (the financial-year picker is shared with Forecast & phasing). Remaining always shows the true budget left, regardless of the window.
      ii. Contracts · POs · Lines — contracts (supplier, supplier number, total value, end date, contract name) hold POs, which hold PO lines (line number, WBS element, spend code, GL code, value). Variations are recorded against the contract: original value + variations = current contract value, and the reconcile badge checks PO lines against that current value. POs can also be added standalone with no contract; "+ PO" opens a form with the contract shown as n/a for standalone, a default line 10, and "+ Add line" for more (each with value, WBS, spend and GL code). Invoices attach to each PO line. Dropdown filters (Supplier, Contract #, WBS) and view templates (Active, Everything, Unreconciled, Archived only) narrow the list; archived contracts/POs/lines are hidden unless you pick a view that shows them.
      iii. Forecast & phasing — quarterly only, following the July–June financial year (Q1 FY27 = Jul–Sep 2026); a "Financial year" picker sets the window and dropdown filters (Supplier, Contract #, WBS) narrow it. Rows are contracts, standalone POs, and a "Planned (not yet contracted)" bucket; ▶ expands one to manage its forecast lines. You phase on the forecast lines only — the row above is the read-only sum of its lines. Lines under a contract/PO default to status "Committed" (options: Committed / In progress / Complete) and pick a PO + PO line; lines in the Planned bucket default to "Planned" and take a manual estimated value and likely supplier. Each line also carries a "what for", Start/End dates. Type a value (`5,000`) or a percentage of remaining budget (`25%`). Forecast lines can be archived (🗄) and hidden with the "show archived" toggle. "act" shows invoiced actuals per period; paste tab-separated values from Excel to fill several quarters at once.
         1. Actual vs forecast — each quarter counts the greater of its forecast or its actual toward the budget, so invoicing a quarter you already forecast no longer double-counts and tips the line "over budget". Where an actual differs from the forecast a Δ chip flags it in the cell (red when the actual exceeds the forecast, green when it is under).
         2. Columns — "Actuals (period)" shows only what is invoiced inside the chosen financial-year window, and "Remaining" is the budget still uncommitted once each quarter's greater-of forecast/actual is taken. Set the window to a year and read Remaining to see, at a glance, whether there is enough budget for that period.
         2. Convert a planned spend to a contract — set a Planned item's status to "Committed" (or use its "→ Contract" button) to open a form that creates the contract, PO and PO line (or attaches to an existing contract/PO, or a standalone PO). The forecast line keeps its phasing through the conversion, and any task, event or note linked to the planned spend follows through and re-points to the new contract (a ↩ badge on the line shows how many links are attached).
      iv. Views — templated views (Full detail, Financial summary, By supplier, By location, Contract register) plus a custom view builder (choose columns, grouping, filter) with saved views.
      v. Archiving — contracts, POs, PO lines and budget lines all have an archive button (🗄) alongside delete; archived items are hidden from default views and dropdowns but keep their history and can be shown or restored (↩) at any time.
   b. Calendar
      i. Month view by default; switch to week or day.
      ii. Tags (Milestone, Meeting, Hui, Activation/Activity, Deadline — customisable in ⚙ Settings) colour and filter events; each event also has an Organiser field, and event notes are the place for hui notes.
      iii. Tasks with due dates appear automatically on the calendar as an empty box (☐, i.e. not yet done), and completed actions show on their completion date as a bare tick (✓). The ☐ Tasks and ✓ Done chips in the toolbar filter task and completed-action pills in or out.
   c. Actions
      i. Endlessly nestable task list — Enter adds the next task, Tab/Shift-Tab nests/un-nests; all top-level items sit tight against the left edge and children indent under a guide.
      ii. Each task has name, a priority flag (click to cycle), owner/person, tags, links, due date, a manually-editable last-actioned date, completion date, state (a dropdown — pick any state directly, including reversing a completed task back to "To do" without having to reopen it) and notes. Notes stay hidden under the task — a 🗒 indicator appears when a note exists, and clicking it expands/collapses the note. The row's action buttons stay in place (they fade in on hover rather than appearing and shifting the row). Due dates carry a subtle colour cue — red when overdue, amber within 3 days, green within a fortnight.
      iii. "+ Header" inserts a section header to group tasks (e.g. by programme or workstream), and headers can contain sub-headers ("+ header" on a header); "★ This week" shows a focused, priority-sorted list of everything with a priority flag or a due date this week.
      iv. Empty tasks aren't kept — if you add a task and leave it blank, it's dropped when you switch tabs.
      v. Log "chasing" as a nested sub-task so the original task is never lost.
   d. Notes (was "Status")
      i. A general note-taking area with multiple pages — the page rail across the top switches between them, and "＋ Page" creates a new one.
      ii. Templates: Blank, Marketing plan (Vision, Problem and opportunity, Umbrella idea, How we roll this out, Sustainable ownership, What success looks like), M&E baseline framework (problem statement, core measurement question, and a baseline grid: topic / sentiment / key data points / COM-B lens / progress indicators / data collection), Stakeholder list (a spreadsheet grid: stakeholder, priority, details, opportunities, influence, interest, risks, relationship owner, next actions, engagement status), Behaviour change approach (per-behaviour insight plus a table where COM-B → Intervention functions → Policy categories → Behaviour change techniques cascade as dependent dropdowns from the Behaviour Change Wheel), and a Links database.
      iii. Each doc page is a Notion-style editor — press `/` in any block for headings, bullets, toggles (collapsible lists), callouts, tables, dividers, and inline links; pull in actions, events, contracts, POs or budget lines as clickable chips via `/link`.
      iv. The Links database page is a filterable table of the programme's key links (title, URL, category, notes) with one-click open.
3. Cross-linking
   a. Anything can link to anything: tasks ↔ contracts, PO lines, calendar events, budget lines, invoices, forecast lines (including planned spends, which carry their links through to the contract when converted).
   b. Chips are clickable everywhere and navigate to (and highlight) the target item.
   c. The ↩ badge on Overview rows and contracts lists everything linking back to them, including notes pages.
4. Exporting
   a. 📊 Excel — a multi-sheet workbook (Overview, Contracts, Variations, POs, PO Lines, Invoices, Forecast, Actions, Calendar, Links, Notes).
      i. The file is SpreadsheetML (`.xls`); Excel opens it directly and may show a one-time format prompt — click Yes.
   b. 📥 Data — a CSV round-trip of the financial data specifically, for editing in Excel and re-uploading (see 1.d).
   c. 📝 Markdown — a full programme snapshot formatted for AI ingestion.
   d. 💾 JSON — the complete raw data, also AI-readable and re-loadable.
5. Look and feel
   a. The colour palette lives in one labelled CSS variable block at the top of `index.html` ("BRAND PALETTE") — edit those hex values to match mansfield.consulting exactly.
