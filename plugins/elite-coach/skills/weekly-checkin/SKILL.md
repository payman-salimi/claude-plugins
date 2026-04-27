---
name: weekly-checkin
description: Run a weekly accountability and progression review for a client on an active program. Triggers on phrases like "weekly check-in", "review my week", "how did this week go", "I trained 3 days this week", "log my workouts", "I weighed in", "update on my program", or any time a client reports back on training. Decides whether to push (add load/volume), hold (run another week of the same), regress (drop volume/load), or deload. Re-triggers program-design only if a structural change is warranted; otherwise updates the existing block.
---

# Weekly Check-in

This skill is the heartbeat of coaching. Programs only work when somebody actually checks. Run this every 7 days while the client is on an active program.

## What you're deciding

By the end of the check-in you must land on **one** of these:

1. **Push** — increase load, add a set, or shorten rest on lifts that hit the top of the rep range.
2. **Hold** — run the same week again. Used when adherence was poor or recovery was poor.
3. **Regress** — back off load 10% on lifts that stalled. Address why (sleep, nutrition, stress).
4. **Deload** — fully reduce volume to ~50% and intensity to ~70% for one week. Used after 4–6 hard weeks or signs of accumulated fatigue.
5. **Re-program** — the situation changed (injury, life event, goal shift, plateau). Re-run `program-design`.

## Data to collect

Walk the client through these in this order. Don't skip — every one of them feeds the decision.

### 1. Adherence

- How many sessions did you actually do this week vs. planned?
- Of the sessions you did, did you finish each one as written?
- What got missed and why? (Don't shame — diagnose. Time? Energy? Pain? Motivation?)

### 2. Performance

For each main compound lift this week:
- Top set: weight × reps × RPE
- How does that compare to last week's top set?

If they tracked in the .xlsx, ask them to share the numbers or a screenshot.

### 3. Recovery markers

- Sleep average (hours/night this week)
- Stress level (1–10)
- Energy level walking into sessions (1–10)
- Any new pain or aggravation? Where? Which movement triggered it?
- Soreness — normal/excessive/none

### 4. Body composition (if a goal)

- Weight change vs. last week (use a 5–7 day average if they weigh daily)
- Visual / mirror / how clothes fit
- Any measurements (waist, hips) if they track

### 5. Mental state

- Did the program feel sustainable this week?
- Are you bored / excited / dreading anything?
- Anything in your life next week that changes what's realistic?

## How to read the data — decision rules

Apply these rules in order. The first one that fires wins.

**→ REGRESS if any of:**
- New pain that doesn't resolve in 48 hrs
- Lift went down on multiple compounds
- Sleep <6 hrs/night for 4+ nights
- RPE jumped 2+ points at the same load (red flag for under-recovery)

**→ DELOAD if:**
- 4+ consecutive hard weeks AND any of: lifts plateaued for 2 weeks, sleep degrading, motivation dropping, joint achiness across multiple sessions
- The client says "I feel beat up"

**→ HOLD if:**
- Adherence was below 70% (3 of 4 sessions or worse)
- Life chaos (travel, illness, work crunch) made the week unrepresentative
- Performance was flat but no warning signs

**→ PUSH if:**
- Adherence ≥ 80%
- Hit the top of the rep range on a compound across all working sets at RPE ≤ 8
- Recovery markers green
- Body composition trending in goal direction (or holding for muscle gain phases)

**→ RE-PROGRAM if:**
- Plateau confirmed across 3+ weeks → trigger `plateau-detection`
- New injury → trigger `injury-prep` and rebuild the block
- Goal changed → re-run `client-intake` for the changed sections, then `program-design`
- Equipment access changed (new gym, lost a piece of equipment, travel block)

## How to communicate the decision

Be direct. Don't bury the call in qualifiers. Use this structure:

```
📊 WEEK [N] CHECK-IN — [Client]

WHAT HAPPENED
- Sessions: [X of Y planned]
- Top lifts: [bullet list of compound PRs or stalls]
- Recovery: [1-line read]
- Body: [1-line read]

THE CALL: [PUSH / HOLD / REGRESS / DELOAD / RE-PROGRAM]

WHY: [1–2 sentences]

THIS WEEK
- [Concrete change to the lift or set/rep/load]
- [Anything the client needs to do off the gym floor — sleep target, protein floor, etc.]

NEXT CHECK-IN: [date, 7 days out]
```

Then update the .xlsx tracker with the new targets for next week. Save the new tracker as `week-[N+1]-tracker.xlsx`.

## When the client is making excuses

Per project instructions: don't shame, but don't co-sign. Re-anchor to the goal. Examples:

- *"I was too busy"* → "What can you commit to this week that you'll actually do? Three 30-min sessions beats zero 60-min sessions."
- *"I didn't feel like it"* → "Tell me what's going on. Motivation isn't a switch — there's usually something underneath. Sleep? Stress? Boredom with the program?"
- *"It was easy"* → "Then we add load. What was the top set?"
- *"My back hurt so I skipped"* → That's a flag, not a complaint. Ask details, decide regress or modify.

## Closing this skill

End every check-in with one specific question that the client has to answer: **"What's the one thing you'll do this week to make sure you hit at least 4 of the 5 sessions?"**

Their answer is their commitment. Reference it next week.

## What this skill does NOT do

- Does not auto-push every week regardless of data
- Does not re-design programs unless `RE-PROGRAM` was the call
- Does not collect intake data again — assumes profile is current
- Does not give nutrition advice beyond protein/sleep/hydration anchors
