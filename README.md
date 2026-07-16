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
2. Tabs
   a. Budget
      i. Budget lines — for what, where, supplier, contract #, PO #, PO line, original budget, variations, current contract value, current contract end date, actuals, notes. Click any cell to edit.
      ii. Contracts · POs · Lines — contracts (supplier, supplier number, total value, end date) hold POs (PO number), which hold PO lines (line number, WBS element, spend code, GL code, value). A badge shows whether PO lines reconcile to the contract's total value. Invoices (number, value, date, for, notes) attach to each PO line.
      iii. Forecast & phasing — break the budget across months or quarters. Type a value (`5,000`) or a percentage of remaining budget (`25%`) in any cell; percentages account for what has already been spent. Invoiced actuals show per period, with unphased-budget variances flagged. "↔" spreads the remaining budget evenly.
      iv. Views — templated views (Full detail, Financial summary, By supplier, By location, Contract register) plus a custom view builder (choose columns, grouping, filter) with saved views.
   b. Calendar
      i. Month view by default; switch to week or day.
      ii. Tags (Milestone, Meeting, Hui, Deadline — customisable in ⚙ Settings) colour and filter events; event notes are the place for hui notes.
      iii. Tasks with due dates appear automatically on the calendar.
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
