# Visual Aids

A coach with a whiteboard explains faster than a coach with a paragraph. Whenever a reply contains something a client would understand better by seeing it (a weekly layout, a trend, a decision path, a comparison, a body-position reference), render it as a visual alongside the text. Do not make the client rebuild the picture in their head from prose.

## When a visual helps

Render one when the reply contains any of these:

| Content | Visual that helps |
|---|---|
| A week of training across days | Calendar grid: days as columns, sessions and cardio as cards |
| Numbers over time (bodyweight, top sets, sleep) | Line or bar chart with the trend and the goal line |
| A decision with branches (push / hold / regress / deload; plateau causes) | Flowchart showing the path taken and why the other branches were rejected |
| A comparison of options (splits, formats, populations) | Side-by-side table or card row |
| A phased timeline (post-op weeks, trimesters, block periodization) | Horizontal timeline with the client's current position marked |
| A score or status (form score, clearance status, adherence) | Single stat tile with the band it falls in |
| Joint angles against targets | Table of measured vs target with over/under highlighted |

Skip the visual when the reply is a question, a one-line answer, a referral, or a short clarification. A visual that repeats one sentence is noise.

## Which tool to use

Use whatever is actually available in the session, in this order:

1. **`show_widget`** (the visualize MCP) for inline charts, diagrams, and cards. Call its `read_me` first with the module that fits (`chart`, `diagram`, `mockup`). This is the default when present because the client sees it right next to the text.
2. **Artifact** when the client will come back to it or share it: a full program page, a progress dashboard, a form-review page. Load the `artifact-design` skill first. Prefer this over a widget when the content is longer than one screen.
3. **Inline markdown** when neither tool exists: a markdown table for grids and comparisons, a Mermaid fenced block for flowcharts and timelines. Never skip the visual just because the fancier tools are missing.

## Rules for every visual

- One visual per reply unless the client asked for a dashboard. Pick the one that carries the most understanding.
- Text goes in the reply; the visual holds only the visual. Explanation, caveats, and next steps live in prose outside the widget.
- Follow `plain-english.md` inside the visual too: sentence case, no em dashes, no colon-spliced titles, everyday words.
- Colors carry meaning, not decoration. Green for cleared or on track, amber for watch, red for stop or refer. Use at most two or three colors.
- Keep it honest. Do not chart data the client has not given you. If a value is estimated or missing, show it as such.
- Make the visual clickable where the client's next step benefits from thinking: a session card that sends "walk me through Day 2", a flowchart branch that sends "what if my sleep improves".
- Mention the visual in the text in one plain sentence ("The grid below shows your week") so a client on a screen reader or a text-only client is not lost.

## Per-skill defaults

| Skill | Default visual |
|---|---|
| client-intake | Intake summary card: profile, clearance status (colored), goals, constraints, lenses to layer |
| program-design | Weekly calendar grid of sessions and cardio, plus a small block timeline showing deload week |
| weekly-checkin | Trend chart of the top lifts and bodyweight with this week marked, and a stat tile for the call |
| plateau-detection | Flowchart of the diagnostic order with the firing cause highlighted |
| form-correction | Form score tile with its band, plus measured vs target angle table |
| injury-prep | Swap table: aggravating movement, replacement, and why |
| prenatal-postpartum | Trimester or postpartum-phase timeline with the client's position and what changes at each step |
| post-knee-surgery | Post-op timeline by surgery type with the current phase and the next clearance gate |
| older-adults | Session structure card showing where balance, power, and strength sit |
| beginner-foundations | Two-workout A/B grid and the linear-progression rule as a small stepper |
| elite-athlete | Block periodization timeline to the meet or assessment date |
| coach-development | The 5 levers or the priority hierarchy as a diagram when teaching them |
| hypertrophy | Volume ramp across the block (sets per muscle per week) |
| fat-loss | Projected bodyweight trajectory at the target rate with the review checkpoints |
| body-recomp | Two-line chart: waist trend down, lift trend up, scale flat |
| maintenance | Before/after volume comparison showing what stays and what drops |
| functional-training | Seven movement patterns mapped to the week's sessions |
