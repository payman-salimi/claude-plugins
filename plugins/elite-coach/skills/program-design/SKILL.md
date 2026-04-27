---
name: program-design
description: Master programming skill. Takes a completed intake plus the relevant specialty lenses and produces a concrete, periodized weekly program — split, exercises, sets/reps/RPE, rest, cardio prescription, deload schedule. Trigger phrases include "build my program", "give me a plan", "design my week", "what should I do at the gym", "make my training plan", "weekly program", or any request for actual programming after intake is on file. Always run client-intake first if profile data is missing. Layer in specialty skills (injury-prep, hypertrophy, fat-loss, beginner-foundations, prenatal-postpartum, post-knee-surgery, older-adults, elite-athlete, body-recomp, maintenance, functional-training, coach-development) as the client's situation dictates. Output both a markdown plan in chat AND an Excel tracker workbook.
---

# Program Design

This is the engine. Intake produced the picture of the client; this skill produces the program they will actually do.

## When to trigger

- After `client-intake` has been completed and confirmed.
- When the client has a profile on file and asks for a new block (e.g., "rebuild my plan for the next 4 weeks").
- After `weekly-checkin` decided a major change is needed.
- Never run this without the intake fields filled. If anything critical is missing, hand back to `client-intake`.

## Layering specialty skills

The 13 specialties are not standalone — they're modifiers on top of this engine. Read the client's situation and pull the right ones:

| Client situation | Layer in |
|---|---|
| Back / knee / shoulder pain (no surgery) | `injury-prep` |
| Currently pregnant or postpartum | `prenatal-postpartum` |
| Post-surgical knee (ACL, meniscus, TKR) | `post-knee-surgery` |
| 60+ years old | `older-adults` |
| Brand new to lifting | `beginner-foundations` |
| Elite athlete / advanced lifter | `elite-athlete` |
| Certified trainer / coach themselves | `coach-development` |
| Goal: muscle gain | `hypertrophy` |
| Goal: fat loss | `fat-loss` |
| Goal: maintenance | `maintenance` |
| Goal: simultaneous gain + lose | `body-recomp` |
| Goal: functional / movement only | `functional-training` |
| Stalled progress diagnosed | `plateau-detection` |

You can layer multiple — e.g., a postpartum client with a low-back issue who wants to lose fat: `prenatal-postpartum` + `injury-prep` + `fat-loss` all apply.

## The decision tree

Before writing the program, lock these decisions in order:

### 1. Training frequency

Use the lower of (a) what they said they could realistically do and (b) what their recovery capacity supports.

- Beginner: 2–4 days/week full body or upper/lower
- Intermediate: 3–5 days/week upper/lower or push/pull/legs
- Advanced: 4–6 days/week PPL, body part split, or specialized
- Older adult / postpartum / post-surgical: start lower, build up

### 2. Cardio vs. weight balance

Decide the ratio explicitly. Common defaults:

| Goal | Resistance / Cardio split |
|---|---|
| Pure hypertrophy | 80 / 20 — minimum cardio for health (2x 20–30 min Z2/wk) |
| Body recomp | 65 / 35 — strength priority, modest cardio for deficit |
| Fat loss | 55 / 45 — strength preserves muscle, cardio drives deficit |
| Maintenance | 60 / 40 |
| Endurance / sport | 30 / 70 — strength is supportive |
| Functional / health | 50 / 50 |

Cardio modalities to mix in: Zone 2 (steady, conversational pace), Zone 4–5 intervals, sport-specific, walking. Default mix: 1–2 Z2 sessions + 1 interval session per week unless contraindicated.

### 3. The split

Pick based on frequency and goal. Examples:

- 3-day full body (beginner, time-crunched, body recomp)
- 4-day upper/lower (intermediate, hypertrophy, fat loss)
- 5-day PPL+UL or body part (advanced hypertrophy)
- 6-day PPL twice (advanced, high volume)
- 2-day full body (true novice, busy parent, postpartum return)

### 4. Exercise selection rules

For each session, in order:
1. **One main compound** (squat, deadlift, press, row, hinge variant) — 3–5 sets, lower reps (3–8), longer rest (2–4 min)
2. **One secondary compound** — 3–4 sets, 6–12 reps
3. **2–4 accessories** for muscle groups undertrained by 1+2 — 3 sets, 8–15 reps
4. **Optional finisher** — metabolic/conditioning, 5–15 min

If the client has injuries or restrictions, the specialty skill replaces banned movements with regressions before this skill writes the workout.

### 5. Loading (sets x reps x intensity)

Default rep ranges by goal:

| Goal | Compound rep range | Accessory rep range | Intensity (RPE / %1RM) |
|---|---|---|---|
| Strength | 3–5 | 5–8 | RPE 7–9 / 75–90% |
| Hypertrophy | 6–10 | 8–15 | RPE 7–9 / 65–80% |
| Endurance / functional | 12–20 | 15–25 | RPE 6–8 / 50–70% |
| Beginner / older adult | 8–12 | 10–15 | RPE 6–7 (always 2–3 reps in reserve) |

### 6. Progressive overload model

Pick one and tell the client which:

- **Linear progression** (beginners): add 5 lb to compounds each session, 2.5 lb to upper-body accessories. Stall 2 sessions in a row → deload that lift 10% and ramp back.
- **Double progression** (intermediates): hit top of rep range across all sets → add weight, drop to bottom of rep range, build back up.
- **Wave / undulating** (advanced): vary intensity day-to-day or week-to-week. Heavy/light/medium structure.
- **% based block** (very advanced): 4–8 week blocks at prescribed % of 1RM, peaking at the end.

### 7. Deload schedule

- Beginner: every 8–12 weeks or as needed
- Intermediate: every 4–6 weeks, 1 deload week (50–60% volume, ~70% intensity)
- Advanced: every 3–5 weeks, planned

## The output — TWO formats every time

### Format 1: Markdown in chat

Use the exact format from the project instructions for each session you prescribe. Don't deviate from this layout — the client expects it.

```
🏋️ [WORKOUT NAME] — Week [N], Day [N]

GOAL OF TODAY'S SESSION: [1 sentence — e.g., "Build squat strength + posterior chain volume"]

WARM-UP (X min)
- Exercise | sets x reps or duration

MAIN BLOCK
A1. Exercise | sets x reps | rest | notes (e.g., "RPE 8, controlled eccentric")
A2. ...
B1. ...
B2. ...

FINISHER / CARDIO BLOCK (if applicable)
- Type | Duration | Target HR or Pace

COOL-DOWN
- Stretching/mobility work

COACHING NOTE: [1–2 sentences on what to focus on mentally or physically today]
```

Show the full week (every training day). Show the cardio days separately if they don't share a session with lifting.

### Format 2: Excel tracker

Generate an `.xlsx` workbook with one tab per training day plus a "Weekly Cardio" tab plus a "Progress Log" tab. Use the `xlsx` skill to build it. Required columns per training day tab:

| Exercise | Set 1 reps | Set 1 wt | Set 1 RPE | Set 2 reps | Set 2 wt | Set 2 RPE | Set 3 reps | Set 3 wt | Set 3 RPE | Set 4 reps | Set 4 wt | Set 4 RPE | Notes |

Pre-fill the Exercise column and target reps. Leave the rest empty for the client to fill as they train.

Save the file to `/Users/paymansalimi/Documents/Claude/Projects/Personal Trainer/programs/[client-name]/week-[N]-tracker.xlsx` and share the `computer://` link.

## Ordering rules

Within a session: **strength before cardio**, unless the goal is sport-specific endurance. Compound lifts before accessories. Heavy multi-joint work before isolation. If two sessions share a day, separate by 4+ hours.

## Recovery prescription

Always include — even if the client doesn't ask:
- **Sleep target**: 7–9 hours, prioritize consistency over total
- **Protein**: 1.6–2.2 g/kg/day for hypertrophy & body recomp, 1.4–1.8 for general
- **Hydration**: ~35 mL/kg/day baseline + 500 mL per hour of training
- **Stress management**: 1+ low-intensity activity/week (walk, mobility, yoga)

## Closing this skill

After writing the program:
1. Post the markdown plan
2. Post the link to the .xlsx tracker
3. End with: **"Run this for [N] weeks. We'll check in [date] to review progression and decide whether to push, hold, or deload. Anything in this plan you want to adjust before you start?"**

Never deliver a program and disappear. Always pin the next check-in.

## What this skill does NOT do

- Does not skip layered specialty skills (an injured client gets `injury-prep` rules baked in, not generic programming)
- Does not invent client data — if intake is missing fields, hand back to `client-intake`
- Does not re-program every week. Programs run in 3–6 week blocks; weekly tweaks come from `weekly-checkin`
