# Programme Manager

A single-file, locally hosted budgeting and programme management app — a "Notion-light database tool with a budgeting addition". No installation, no server, no dependencies: open `index.html` in a desktop browser (Chrome or Edge recommended).

1. Getting started
   a. Open `index.html` in your browser (double-click the file).
   b. Enter a programme name on the start screen — each programme is a separate instance.
      i. Data autosaves to the browser as you type (see the "Saved" stamp in the header).
      ii. Every programme created on this computer is listed on the start screen.
   c. Use 💾 Save to write a portable `.programme.json` file, and 📂 Open to load one.
      i. The `.json` file is plain structured text — drop it (or the 📝 Markdown snapshot) straight into an AI model for analysis and interrogation.
      ii. Ctrl/Cmd-S also saves.
   d. Use 📥 Data for a spreadsheet round-trip of contracts and financial data.
      i. Download current data (opens in Excel), edit or add rows, save as CSV, and re-upload — this replaces the old fixed import template. `import-template.csv` remains a worked example of the format.
      ii. One row per item, ordered contract → po → line → invoice, matched on contract/PO/line/invoice numbers — re-uploading updates existing items instead of duplicating them.
      iii. A `po` row with a blank `contract_number` becomes a standalone PO; put its supplier in the `supplier` column. Contracts also carry `what` and `where` columns.
      iv. If a file has no recognised `type` column (e.g. a report exported from elsewhere), the importer now says so clearly instead of silently doing nothing.
   e. Data entry: Tab moves to the next field, Enter moves down the column (Excel-style), and long text fields wrap as you type.
      i. PO lines can be copied (⧉) and pasted (📋) whole — the target keeps its own line number.
      ii. Tab-separated values pasted from Excel fill across a PO line row, or across consecutive forecast periods.
      iii. Contracts, POs, PO lines, forecast lines, tasks and links can be reordered by dragging their ⠿ handle (within their own group).
      iv. Contracts and POs fold/unfold (▼/▶) so long lists stay manageable.
   f. Customise in ⚙ Settings: the label for the "Where" field (e.g. Site, Region, Workstream), task states, task priorities, task tags, calendar tags and forecast statuses.
2. Tabs
   a. Budget
      i. Overview — a read-only summary with one row per contract and per standalone PO (no double-counting): for what, supplier, contract #, PO #s, line count, original budget, variations, current value, end date, actuals, remaining. The "For what" column shows the contract's name (its "for what", falling back to the contract number so a row is always identifiable). Nothing is edited here; → jumps to the detail, and the templated/custom views and archived filter still apply.
      ii. Contracts · POs · Lines — contracts (supplier, supplier number, total value, end date, for what, where) hold POs, which hold PO lines (line number, WBS element, spend code, GL code, value). Variations are recorded against the contract: original value + variations = current contract value, and the reconcile badge checks PO lines against that current value. POs can also be added standalone with no contract (they appear in their own section and still carry lines and invoices). Invoices (number, value, date, for, notes) attach to each PO line. Filter and view templates (Active, Ending within 90 days, Unreconciled, Archived only) can be saved as named views.
      iii. Forecast & phasing — quarters follow the July–June financial year (Q1 FY27 = Jul–Sep 2026), and a "Financial year…" picker jumps straight to a whole FY. Rows are contracts and standalone POs; ▶ expands one to manage its forecast lines. You phase on the forecast lines only — the contract/PO row above is the read-only sum of its lines. Each forecast line carries a "what for" description, a Status, and Start/End dates, and picks a PO + PO line (its supplier and reference show automatically); several forecast lines can phase the same PO line. "+ one per PO line" seeds a line per uncovered PO line. Type a value (`5,000`) or a percentage of remaining budget (`25%`); percentages account for what has already been spent. Forecast lines can be archived (🗄) and hidden with the "show archived" toggle. Invoiced actuals show per period, unphased budget is flagged, "↔" spreads the remainder evenly, and period settings + filter can be saved as named views.
      iv. Views — templated views (Full detail, Financial summary, By supplier, By location, Contract register) plus a custom view builder (choose columns, grouping, filter) with saved views.
      v. Archiving — contracts, POs, PO lines and budget lines all have an archive button (🗄) alongside delete; archived items are hidden from default views and dropdowns but keep their history and can be shown or restored (↩) at any time.
   b. Calendar
      i. Month view by default; switch to week or day.
      ii. Tags (Milestone, Meeting, Hui, Activation/Activity, Deadline — customisable in ⚙ Settings) colour and filter events; each event also has an Organiser field, and event notes are the place for hui notes.
      iii. Tasks with due dates appear automatically on the calendar, and completed actions show on their completion date (✓).
   c. Actions
      i. Endlessly nestable task list — Enter adds the next task, Tab/Shift-Tab nests/un-nests; all top-level items sit tight against the left edge and children indent under a guide.
      ii. Each task has name, a priority flag (click to cycle), owner/person, tags, links, due date, last-actioned date, completion date, state (click the pill to cycle) and notes. Notes stay hidden under the task — a 🗒 indicator appears when a note exists, and clicking it expands/collapses the note.
      iii. "+ Header" inserts a section header to group tasks (e.g. by programme or workstream), and headers can contain sub-headers ("+ header" on a header); "★ This week" shows a focused, priority-sorted list of everything with a priority flag or a due date this week.
      iv. Log "chasing" as a nested sub-task so the original task is never lost.
   d. Notes (was "Status")
      i. A general note-taking area with multiple pages — the page rail across the top switches between them, and "＋ Page" creates a new one.
      ii. Templates: Blank, Stakeholder list, Marketing plan, Behaviour change approach, M&E baseline, and a Links database.
      iii. Each doc page is a Notion-style editor — press `/` in any block for headings, bullets, toggles (collapsible lists), callouts, tables, dividers, and inline links; pull in actions, events, contracts, POs or budget lines as clickable chips via `/link`.
      iv. The Links database page is a filterable table of the programme's key links (title, URL, category, notes) with one-click open.
3. Cross-linking
   a. Anything can link to anything: tasks ↔ contracts, PO lines, calendar events, budget lines, invoices.
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
