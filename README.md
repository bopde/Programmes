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
   d. Use 📥 Import to load contracts and financial data from CSV.
      i. `import-template.csv` in this folder is the template (also downloadable from the Import dialog).
      ii. One row per item, ordered contract → po → line → invoice, matched on contract/PO/line/invoice numbers — re-importing updates existing items instead of duplicating them.
      iii. A `po` row with a blank `contract_number` becomes a standalone PO; put its supplier in the `supplier` column.
   e. Data entry: Tab moves to the next field, Enter moves down the column (Excel-style), and long text fields wrap as you type.
      i. PO lines can be copied (⧉) and pasted (📋) whole — the target keeps its own line number.
      ii. Tab-separated values pasted from Excel fill across a PO line row, or across consecutive forecast periods.
      iii. Contracts, POs, PO lines and forecast lines can be reordered by dragging their ⠿ handle.
      iv. Contracts and POs fold/unfold (▼/▶) so long lists stay manageable.
2. Tabs
   a. Budget
      i. Overview — a read-only summary with one row per contract and per standalone PO: for what, where, supplier, contract #, PO #s, line count, original budget, variations, current value, end date, actuals, remaining, notes. Nothing is edited here (the "for what" / "where" live on the contract itself); → jumps to the detail, and the templated/custom views and archived filter still apply.
      ii. Contracts · POs · Lines — contracts (supplier, supplier number, total value, end date, for what, where) hold POs, which hold PO lines (line number, WBS element, spend code, GL code, value). Variations are recorded against the contract: original value + variations = current contract value, and the reconcile badge checks PO lines against that current value. POs can also be added standalone with no contract (they appear in their own section and still carry lines and invoices). Invoices (number, value, date, for, notes) attach to each PO line. Filter and view templates (Active, Ending within 90 days, Unreconciled, Archived only) can be saved as named views.
      iii. Forecast & phasing — quarters follow the July–June financial year (Q1 FY27 = Jul–Sep 2026). Rows are contracts and standalone POs; ▶ expands one to manage its forecast lines. Each forecast line picks a PO + PO line and a "for" description, several forecast lines can phase the same PO line, and they all wrap up into the contract row (Σ). "+ one per PO line" seeds a line per uncovered PO line. Type a value (`5,000`) or a percentage of remaining budget (`25%`); percentages account for what has already been spent. Invoiced actuals show per period, unphased budget is flagged, "↔" spreads the remainder evenly, and period settings + filter can be saved as named views.
      iv. Views — templated views (Full detail, Financial summary, By supplier, By location, Contract register) plus a custom view builder (choose columns, grouping, filter) with saved views.
      v. Archiving — contracts, POs, PO lines and budget lines all have an archive button (🗄) alongside delete; archived items are hidden from default views and dropdowns but keep their history and can be shown or restored (↩) at any time.
   b. Calendar
      i. Month view by default; switch to week or day.
      ii. Tags (Milestone, Meeting, Hui, Deadline — customisable in ⚙ Settings) colour and filter events; event notes are the place for hui notes.
      iii. Tasks with due dates appear automatically on the calendar, and completed actions show on their completion date (✓).
   c. Actions
      i. Endlessly nestable task list — Enter adds the next task, Tab/Shift-Tab nests/un-nests.
      ii. Each task has name, links, due date, last-actioned date (updated automatically on any edit), state (customisable in ⚙ Settings; click the pill to cycle) and notes.
      iii. Log "chasing" as a nested sub-task so the original task is never lost.
   d. Status
      i. A blank Notion-style page — press `/` in any block for headings, bullets, toggles (collapsible lists), callouts, tables, dividers, and inline links.
      ii. Pull in actions, calendar events, contracts, POs or budget lines as inline clickable chips via `/link`.
3. Cross-linking
   a. Anything can link to anything: tasks ↔ contracts, PO lines, calendar events, budget lines, invoices.
   b. Chips are clickable everywhere and navigate to (and highlight) the target item.
   c. The ↩ badge on budget lines and contracts lists everything linking back to them.
4. Exporting
   a. 📊 Excel — a multi-sheet workbook (Budget, Contracts, POs, PO Lines, Invoices, Forecast, Actions, Calendar, Status).
      i. The file is SpreadsheetML (`.xls`); Excel opens it directly and may show a one-time format prompt — click Yes.
   b. 📝 Markdown — a full programme snapshot formatted for AI ingestion.
   c. 💾 JSON — the complete raw data, also AI-readable and re-loadable.
5. Look and feel
   a. The colour palette lives in one labelled CSS variable block at the top of `index.html` ("BRAND PALETTE") — edit those hex values to match mansfield.consulting exactly.
