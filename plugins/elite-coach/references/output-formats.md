# Output Formats

Clients use programs in different places: a phone at the squat rack, a shared spreadsheet, a Slack channel with their coach, a document they print. The plugin's job is to deliver the outcome where it will actually get used. Produce the default in chat first, then offer the formats that fit the question. Never make the client ask "can I get this as a spreadsheet?" when a spreadsheet was the obvious home for it.

## The format menu

Offer only formats whose tools exist in the current session. Check what is available before offering; an option that fails when picked is worse than no option.

| Format | Best for | Needs |
|---|---|---|
| Markdown in chat | Everything, always the first delivery | Nothing |
| Excel workbook (.xlsx) | Trackers the client fills in weekly; anything with per-set cells | `program-design/scripts/build_tracker.py` (openpyxl) or an `xlsx` skill |
| Google Sheet | Same as Excel, when the client already works in Google or wants to share with a coach or partner | A Google Drive or Sheets connector |
| Artifact (web page) | Programs, dashboards, and form reviews the client will reopen on a phone; anything with charts | The Artifact tool |
| Word or Google Doc | Intake summaries, clearance letters, a program the client wants to print or send to a physician or PT | A `docx` skill or a Google Docs connector |
| Slack message | Check-in summaries, the weekly call, a reminder, anything short that a coach or accountability partner should see | A Slack connector |
| Notion page | Clients who keep their training log in Notion | A Notion connector |
| PDF | A finished block the client wants to file or hand to a PT | A `pdf` skill |

## Which options to offer, by deliverable

Pick two or three options that genuinely fit. Do not list the whole menu.

| Deliverable | Offer |
|---|---|
| A weekly program (program-design) | Excel tracker (default), Google Sheet, Artifact page. Doc or PDF if they mention printing or a physician. |
| Weekly check-in call (weekly-checkin) | Chat summary (default), Slack message to their channel, tracker update for next week. |
| Intake summary (client-intake) | Chat summary (default), Doc for their records or to bring to a doctor, Notion page if they keep a log there. |
| Plateau diagnostic (plateau-detection) | Chat (default), Doc if they want to share with a coach, updated tracker if the fix changes the plan. |
| Form review (form-correction) | Chat (default), Artifact page with the annotated key frames and score for re-filming comparison. |
| Phase timeline (prenatal-postpartum, post-knee-surgery) | Chat (default), Doc or PDF to share with the OB, midwife, or PT. |
| Coaching frameworks (coach-development) | Chat (default), Doc or Notion page the coach can keep and reuse. |

## How to offer

1. Deliver the default in chat so the client has something immediately.
2. Close with one plain sentence listing the options, for example: "I can also put this in a Google Sheet you can share with your coach, or on a page you can open on your phone at the gym. Want either?"
3. When the choice changes the work substantially (a Sheet vs a printed Doc changes how the tracker is built), ask before building, using the question tool if one is available, with the recommended option first.
4. Remember the answer. Once a client picks Google Sheets, deliver every later tracker there without asking again. Ask again only if the situation changes (new coach, travel, they mention printing).

## Format rules

- The same content goes into every format. A Slack summary is shorter, not different.
- `plain-english.md` applies inside every format: sheet headers, doc headings, Slack text, artifact titles.
- A tracker always keeps the same structure (one tab per day, Weekly Cardio, Progress Log) whether it is Excel or Google Sheets, so `weekly-checkin` can read it back.
- Sending to Slack, Notion, Google, or any external service publishes the content. Confirm the destination (which channel, which folder) before sending, and never send a client's medical details anywhere they have not named.
- When a connector is not available, say so in one sentence and offer the nearest alternative (an .xlsx file instead of a Google Sheet, a markdown file instead of a Doc).
