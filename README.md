# Decision Tree Builder

Decision Tree Builder is an interactive decision-tree and option-comparison tool delivered as a single, self-contained HTML file (`index.html`). You build one tree of options per workstream, note the pros, cons, outcome and cost of each option, flag blockers, tick the deliverables each option provides, and mark the path you actually chose. Press **Complete** to get a summary table with cost totals and deliverable coverage. You can then export everything, including a picture of the tree, to an Excel workbook and import it again later to carry on.

## Features

- Any number of root workstreams, each with its own tree of options nested to any width and up to 200 levels deep.
- Per block: title, pros, cons, outcome, cost (a plain number) and a blocker flag.
- One chosen path per workstream, highlighted on the diagram.
- Session-wide deliverables, ticked on blocks, with a coverage strip in the results.
- Final goals that one or more workstreams feed, with inherited pros, cons and cost total.
- Rearrange blocks by drag and drop, with a one-step Undo / Redo for moves and deletes.
- Collapse and expand branches, top-down or left-right layout, zoom, pan and fit.
- Light and dark themes.
- Keyboard navigation and shortcuts.
- Export to an xlsx workbook (summary, picture of the tree, raw data) and import from it again.
- Runs entirely in the browser: no libraries, no external resources, no network traffic.

## Quick start

1. Download `index.html`.
2. Open it in any modern browser.

That is all. There is nothing to install, no build step and no server. The page makes no network requests. Every time it opens it shows the built-in dinner example, so you can try every feature straight away.

## Core concepts

### Workstreams (roots)

A **root** is a workstream: one decision you need to make. Roots are listed in the **Roots** section of the left rail; add one with **+ Root**. Each root is the top of its own tree.

### Options, blocks and nesting

Every item in a tree is a **block** (also called a node). Any block, including a root, can have as many children as you like: select it and press **+ Child**. Children usually represent the options, or refinements of an option, under their parent. A tree may be at most 200 levels deep, counting the root as level 1. There is no limit on width.

### Cost and totals

- **Cost** is a plain number with no currency symbol and no unit. Anything that is not a number is refused and the stored cost is left unchanged.
- An **empty** cost means "no cost", which is deliberately different from a cost of zero.
- A cost may have at most 6 decimal places and a magnitude of at most 9007199254.740991. Values outside these limits are refused rather than rounded.
- **Path total:** for each workstream, the summary adds up the costs of the blocks on its chosen path. Blocks with no cost are not counted. The row reads "Path total over N blocks with a cost" and appears only when at least one block on the path has a cost.
- **Goal cost total:** a goal has no cost of its own. Its total is derived (read only): the sum of the costs of every block on the chosen path or paths that feed it.
- Totals are added exactly. If a total ever leaves the supported range, the tool says so in words instead of printing a wrong number.

### Pros, cons and outcome

Free-text fields on each block, edited in the **Details** panel. Once a field has text, the block shows a coloured dot: green for pros, amber for cons, blue for outcome and black for cost. Click a dot to expand the text in place; click again to collapse it.

### The blocker flag

The small padlock on a block, or the **Blocker: off** / on button in the Details panel, toggles the blocker flag. A blocked block gets a translucent red wash on the diagram and is highlighted in the summary table and the exported workbook.

### The chosen path (one per workstream)

Each workstream stores exactly one chosen path. Select a block and press **Choose path**: that block becomes the end of the path, and every ancestor up to the root is included automatically. The path is highlighted with a green border and tint, and the end block has a thicker border. Choosing a different block in the same tree moves the end point. **Clear path** removes the choice for that workstream. Only blocks on chosen paths appear in the summary table; a workstream with no chosen path is still listed, with a note saying so.

### Deliverables

A **deliverable** is something the work has to produce. Deliverables are session-wide: there is one list, shared by every workstream.

- Manage the list in the **Deliverables** section of the left rail: **+ Deliverable** adds one, and each row has **Rename** and **Delete** buttons. The number beside each row shows how many blocks tick it.
- In a block's Details panel, tick the deliverables that block delivers. Any number of blocks may deliver the same deliverable.
- Deleting a deliverable removes it from every block that ticked it.
- On the diagram, a badge shows children and deliverables together, for example `+2 (3)` for two children and three deliverables, `(3)` for no children and three deliverables, or `+2` for children only.
- **Coverage:** after **Complete**, the results open with a strip of one rectangle per deliverable. Green means at least one block on any chosen path delivers it; grey means none does. A headline gives the count, for example "3 of 4 deliverables covered". Goals never contribute to coverage.

### Final goals

A **final goal** is the destination that chosen paths arrive at. Add one with **+ Goal** in the left rail, then select any block in a workstream and press **Goal...** to choose which goal that workstream feeds (or to release it).

- A workstream feeds at most one goal; a goal can be fed by any number of workstreams, or none.
- A goal's own fields are its title, outcome and blocker flag.
- Its pros and cons are inherited from the blocks on the chosen paths that feed it, and are read only.
- Its cost is the derived total described above. It has no editable cost and no deliverables.
- A goal is drawn past the deepest level of the workstreams it serves. It shows as "not linked" with a dashed border until you press **Complete**, which links the end of each feeding chosen path to it with a dashed green connector. The links are removed if the relevant chosen path changes, and **Complete** links them again.
- Goals cannot be dragged or made a child of anything.

## The built-in example: dinner

Every page load starts with a small dinner plan that exercises every feature.

| Workstream | Option | Choices (cost) |
|---|---|---|
| Main course | Meat | Roast chicken (24), Beef steak (40) |
| Main course | Fish | Baked salmon (30), flagged as a **blocker** (check guests for allergies) |
| Main course | Vegetarian | Mushroom risotto (12) |
| Drinks | Hot drinks | Tea (3), Coffee (5) |
| Drinks | Juices | Orange juice (4), Apple juice (4) |
| Drinks | Alcoholic drinks | Wine (15), Beer (10) |

Four deliverables are seeded: **Everyone fed**, **Dietary needs covered**, **Drinks for every guest** and **Within budget**. Both workstreams feed one final goal, **Dinner for 6 guests**. No chosen path is set at the start.

A short walk-through:

1. In the Main course tree, select **Roast chicken** and press **Choose path**. The path Main course > Meat > Roast chicken is highlighted.
2. In the Drinks tree, select **Wine** and press **Choose path**.
3. Press **Complete**. The summary shows a path total of 24 for Main course and 15 for Drinks, the goal "Dinner for 6 guests" shows a cost total of 39, and the coverage strip reports 2 of 4 deliverables covered (Everyone fed and Within budget, both from Roast chicken).
4. Now select **Mushroom risotto** and press **Choose path**, then select **Tea** and press **Choose path**, and press **Complete** again. The totals become 12 and 3 (goal total 15), and coverage rises to 4 of 4.
5. Try choosing **Baked salmon** to see how a blocked step is highlighted in the summary.

## Using the interface

### Adding and editing blocks

- **+ Root** (left rail) adds a workstream. **+ Child** (toolbar) adds a child to the selected block.
- **Rename** renames the selected block. **Delete** removes it and its whole subtree after a confirmation.
- **Details** opens the **Node details** panel to edit the title, pros, cons, outcome, cost, blocker flag and deliverable ticks. **Close** hides it.
- Drag a block to move it: drop it onto another block to make it that block's last child, between two blocks to reorder it as a sibling, or onto empty canvas to make it a new root. The whole subtree moves with it. Moves that would create a cycle, exceed the maximum depth or change nothing are refused. Press Escape while dragging to cancel.

### Collapse and expand

Every block with children has a small round `-` control on the connector below it (or to its right in the left-right layout). Click it to collapse that branch; it becomes `+` and a blue badge shows how many descendants are hidden. **Expand all** and **Collapse all** in the toolbar act on every branch. Collapsing is a view only: it never changes the data or the chosen path, and the summary still reports hidden steps.

### Orientation

The **Layout** button switches between **top-down** (suits deep, narrow trees) and **left-right** (suits wide, shallow trees). The layout recalculates automatically and blocks shrink as the diagram gets busier.

### Zoom and pan

- **Zoom -** and **Zoom +** magnify between 25 and 300 percent. **100%** resets the zoom; **Fit** fits the whole tree into view.
- Ctrl (or Cmd) plus the mouse wheel zooms around the pointer.
- Drag empty canvas to pan. Hold Space, or use the middle mouse button, to pan from anywhere.

### Theme

Light is the default theme for a first-time visitor. Once you pick a theme, it is remembered in the browser and restored on later visits. The **Dark theme** / **Light theme** button in the top bar switches between them.

### The results panel

**Complete** builds the **Complete summary** under the diagram, stamped with the time it was generated. It contains the deliverable coverage strip, one table per workstream (with Cost and Deliverables columns and a path total row) and a single **Final goals** table listing every goal once with the workstreams it serves, its inherited pros and cons, outcome, blocker state and cost total. **Hide results** dismisses the table but leaves goal links on the diagram. Pressing **Complete** again always rebuilds from the current tree.

### Undo

**Undo** in the toolbar (or Ctrl+Z / Cmd+Z) reverses the last block **move or delete**, and nothing else. It holds one step only; after use the button reads **Redo**. Any other change (adding, renaming, editing details, ticking a deliverable, changing a path, collapsing a branch, importing, Clear all) clears the step. Selecting a different block does not.

### Clear all

**Clear all** in the left rail deletes every root, block and goal after a confirmation. The deliverable list is kept, because it is session-wide. It cannot be undone and the tree is not saved anywhere, so export first if you need it.

### Keyboard shortcuts

| Key | Action |
|---|---|
| Tab / Shift+Tab | Move between blocks and controls |
| Enter or Space on a block | Select it |
| Up / Down / Left / Right | Parent / first child / previous and next sibling |
| Shift+Enter | Open the Details panel for the selected block |
| Insert | Add a child to the selected block |
| Delete | Delete the selected block (after confirmation) |
| Ctrl+Z / Cmd+Z | Undo or redo the last move or delete |
| + / - | Zoom in / out |
| 0 | Reset zoom to 100% |
| f | Fit the tree to the screen |
| d / l | Dark / light theme |
| Space (held) | Pan by dragging from anywhere |
| Escape | Close help, the Details panel or an expanded attribute; cancel a drag |

Single-letter shortcuts and Ctrl+Z are ignored while you are typing in a field.

### Picture export

There is no separate image download. A PNG picture of the whole diagram is embedded in the **Decision tree** sheet of the exported workbook (see below). It is rendered from its own layout pass at a fixed width, so it is unaffected by zoom or scroll position, and it follows the current orientation and collapsed branches.

## Saving and resuming work

**The tree is never stored in the browser.** Every page load starts from the dinner example. Use **Export xlsx** and **Import xlsx** to save and resume.

**Export xlsx** downloads `decision-tree-summary.xlsx`, generated entirely in the browser, with three sheets:

| Sheet | Contents |
|---|---|
| Summary | One section per workstream with the chosen path's pros, cons, outcomes, costs, deliverables and path total, blocked steps in red, then the Final goals table and the deliverable coverage strip with its headline count. |
| Decision tree | A PNG picture of the whole diagram, goals included. |
| Raw data for Import | The machine-readable save format, a complete description of the tree. |

**Import xlsx** reads a workbook exported earlier (including one re-saved in Excel) and rebuilds the whole tree: every block and attribute, costs, deliverables and ticks, chosen paths, goals, goal assignments and collapsed branches.

- Each part of the file is checked against the checksum recorded in the workbook; a corrupted file is refused.
- Import is all or nothing: the file is fully validated before anything changes, and if anything fails while drawing the new tree, the previous tree is restored.
- If the current tree differs from the untouched example, you are asked to confirm: "Importing replaces the current tree completely." The message gives the number of workstreams, blocks and goals that would be lost. Cancelling changes nothing.

## Import file format

The importer reads only the sheet named exactly **`Raw data for Import`**. The easiest and safest way to get a valid file is to **export one from the tool and edit it**, rather than writing one from scratch.

### Layout

| Row | Contents |
|---|---|
| 1 | A1 = `Schema`, B1 = `decisionTreeBuilder.rawImport`, C1 = `Version`, D1 = `4` |
| 2 | Column headings |
| 3 onwards | One record per row |

Only schema version **4** is accepted. Other versions are refused with a message saying whether the file is older, newer or not a version number at all.

Headings are matched by name, so columns may be reordered, but **every** heading below must be present. Rows where both RecordKind and Identifier are empty are skipped.

### Record kinds and identifiers

| RecordKind | Identifier format | Meaning |
|---|---|---|
| `node` | `node-` followed by a positive whole number, e.g. `node-1` | A block (root or child) |
| `goal` | `goal-` followed by a positive whole number | A final goal |
| `deliverable` | `deliverable-` followed by a positive whole number | A deliverable definition |

Numbers must have no leading zeros and must not be zero. Every identifier must be unique in the sheet, and its prefix must match its RecordKind. Parent/child links work by each node naming its parent in **ParentIdentifier**; a node with no parent is a root. Order among siblings (and among roots, goals and deliverables) comes from **SiblingIndex**, with ties broken by identifier.

### Columns

Yes/no columns accept `1`, `true`, `yes` (yes) or `0`, `false`, `no`, empty (no), case-insensitive. Anything else is refused.

| Column | node | goal | deliverable |
|---|---|---|---|
| RecordKind | Required: `node` | Required: `goal` | Required: `deliverable` |
| Identifier | Required, `node-N` | Required, `goal-N` | Required, `deliverable-N` |
| ParentIdentifier | Empty for a root; otherwise the `node-N` of an existing node | Not read | Not read |
| RootIdentifier | Optional. If filled, must be the `node-N` of the root that the parent links actually lead to | Not read | Not read |
| SiblingIndex | Whole number, 0 or more, digits only (no sign, no decimal point, no leading zeros: `0` is the only value that may start with 0, so `01` is refused), at most 9007199254740991; empty is treated as 0 | Same (order of goals) | Same (order of deliverables) |
| IsRoot | Yes/no; must be yes exactly when ParentIdentifier is empty | Not read | Not read |
| Title | Block title | Goal title | Deliverable name |
| Pros | Free text | Not read (derived; written for reading only) | Not read |
| Cons | Free text | Not read (derived; written for reading only) | Not read |
| Outcome | Free text | Free text | Not read |
| Cost | Empty (no cost) or a plain number within the supported precision and range | Must be empty | Not read |
| DeliverableIdentifiers | Space-separated `deliverable-N` values, each defined in the sheet; may be empty | Must be empty | Not read |
| Blocker | Yes/no | Yes/no | Not read |
| Collapsed | Yes/no: branch is collapsed | Not read | Not read |
| OnChosenPath | Yes/no; must match the chosen path rebuilt from IsChosenPathEnd | Not read | Not read |
| IsChosenPathEnd | Yes/no; at most one per workstream | Not read | Not read |
| GoalIdentifier | Written by the exporter on roots; not read by the importer (goal assignment comes from GoalServedRootIdentifiers) | Not read | Not read |
| GoalServedRootIdentifiers | Not read | Space-separated `node-N` values of the roots this goal serves; may be empty | Not read |
| IsActiveBlock | Yes/no: the block selected after import | Yes/no | Not read |

If no row is marked as the active block, the first root is selected.

### Main validation errors

An import is refused, with a message naming the row where possible, if:

- the `Raw data for Import` sheet is missing, does not start with the schema marker, or declares a version other than 4;
- any required column heading is missing;
- a RecordKind is not `node`, `goal` or `deliverable`, or an Identifier is missing, malformed or duplicated;
- a ParentIdentifier, RootIdentifier, DeliverableIdentifiers entry or GoalServedRootIdentifiers entry is malformed;
- SiblingIndex is not a plain whole number, or a yes/no cell holds another value;
- IsRoot disagrees with ParentIdentifier;
- a cost is not a number or is outside the supported precision or range;
- a goal row carries a cost or deliverables;
- a block ticks a deliverable that the sheet does not define;
- a parent named in ParentIdentifier is not in the sheet, or the parent links form a loop;
- there are no node rows, or no root workstreams;
- a workstream has more than one chosen path end;
- the tree is deeper than 200 levels;
- a RootIdentifier disagrees with the root the parent links lead to;
- an OnChosenPath value disagrees with the rebuilt chosen path;
- a goal claims to serve something that is not a root, or a root is claimed by more than one goal;
- the file is corrupt (checksum mismatch) or cannot be read as a workbook.

## Privacy and storage

Your tree is never stored and never sent anywhere. T[text](README.md) [text](index.html)here is no server: the page has no external dependencies and makes no network requests. It also declares a Content Security Policy in a meta element (for example `default-src 'self'`, `object-src 'none'`, `form-action 'none'`).

Only these view preferences are kept in the browser's localStorage, under keys beginning `decisionTreeBuilder.`:

- theme;
- orientation (layout);
- zoom level;
- whether the results panel was hidden.

None of them describes a tree. Collapsed branches last only while the page is open. The results themselves are never remembered: after a reload the panel stays empty until you press **Complete**.

## Limitations

- One chosen path per workstream, and each workstream feeds at most one goal.
- Maximum tree depth of 200 levels (the root is level 1).
- Undo covers only the most recent block move or delete.
- Single user, single browser tab. There is no collaboration, sharing or sync; share the exported workbook instead.
- Nothing is saved automatically. Export before closing the page if you want to keep your work.

## Contributing

The whole tool is one HTML file with inline CSS and JavaScript, no dependencies and no build step. To contribute, edit `index.html`, open it in a browser to test, and submit your change. Please keep it self-contained, with no external resources, and keep the in-page Help text in step with any behaviour you change.

## Licence

This project is source-available.

Commercial use is NOT permitted without a separate commercial licence.

If you wish to use this software in a business, commercial product, SaaS platform, consultancy, or revenue-generating service, please contact:

https://www.linkedin.com/in/aleksandr-sukhov/

Copyright (c) 2026 Aleksandr Sukhov
All rights reserved.