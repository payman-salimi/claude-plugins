---
name: plateau-detection
description: Diagnose why a client has stalled and prescribe specific modifications to break the plateau. Triggers when the client mentions "stuck", "plateau", "stopped progressing", "lifts haven't moved", "weight isn't changing", "I'm stalled", "no progress in weeks", "hit a wall", "lifts aren't going up", or any indication that the program has stopped working. Layer on top of program-design — this skill does NOT auto-rebuild the entire program; it identifies the cause, recommends targeted changes, and only escalates to a full re-program if the cause requires it.
---

# Plateau Detection

A plateau is a signal, not a sentence. Progress in training is non-linear, and stalling is part of the loop — but stalls have causes, and the causes are diagnosable.

The job here is to ask the right questions, find the actual cause, and prescribe the smallest effective change. Don't blow up a program because of a 2-week stall when the cause is just under-sleeping.

## What counts as a plateau

Define it before diagnosing. A plateau is:

- **Strength**: a compound lift hasn't progressed (weight or reps) in 3+ consecutive weeks despite intent to progress
- **Hypertrophy**: measurements (and/or photos) haven't changed in 4–6 weeks despite training in a building phase
- **Fat loss**: bodyweight (5–7 day average) hasn't moved in 2+ weeks despite an intended deficit

Single-week stalls aren't plateaus. Don't react to noise.

## The diagnostic order

Walk through these in order. The first one that fires is your answer.

### 1. Adherence

Most "plateaus" are missed sessions in disguise.
- How many sessions actually happened in the last 4 weeks?
- Were they completed as written, or shortened?
- Were the working weights and rep prescriptions actually hit?

If adherence < 80%: that's the plateau. The fix is adherence, not programming.

### 2. Recovery

- Sleep average over last 4 weeks?
- Stress level changes?
- Big life events (move, work crunch, illness)?
- Soreness duration after sessions?
- Energy level walking into the gym (1–10)?

Recovery debt looks like a plateau but isn't. Sleep <6 hrs avg = plateau. Fix the sleep before fixing the program.

### 3. Nutrition

- Goal-aligned calorie target — actually being hit?
- Protein at the prescribed floor (1.6+ g/kg for hypertrophy, 2.0+ for fat loss/recomp)?
- Recent change in eating patterns (travel, holidays, meal-prep collapse)?

Most clients underestimate intake by 20–30%. If the math doesn't add up to progress, the math is wrong.

### 4. Training stimulus

If 1–3 are clean, the program may be the issue. Check:

**Volume drift**: has total weekly volume slowly decreased without notice? Working sets not actually pushed?

**Intensity drift**: are top sets actually at RPE 8, or has it slid to RPE 6?

**Variation staleness**: same exercises for 8+ weeks at the same volume? Body has fully adapted to the stimulus.

**Volume too high**: counterintuitively, sometimes the issue is *too much* volume — recovery is the limiter, not stimulus.

### 5. Goal mismatch

Is the client running the right program for the goal? Common mismatches:
- Running a hypertrophy block while in a heavy fat-loss deficit (read `body-recomp`)
- Running a beginner program when they're now an intermediate
- Running a high-volume program when life chaos is high (volume should drop)

### 6. Genuine plateau (rare)

If the above are all clean, you may have hit an actual training plateau — programming has stopped producing adaptation. This is the only case that warrants a structural change to the program.

## The fixes — by cause

### If adherence is the issue

- Reduce program scope: 4 days → 3 days if 4 isn't happening
- Move sessions earlier in the day (mornings have higher adherence)
- Reduce session length
- Build in flexibility (1 of 4 sessions can be a "minimum effective dose" version on bad days)
- Re-anchor to the goal: "Why does this matter to you?"

### If recovery is the issue

- Add a deload week immediately (50% volume, 70% intensity)
- Drop one session if running 5–6 days
- Address sleep: sleep target, no caffeine after noon, screen cutoff, sleep hygiene
- Address stress: low-intensity work (walks, yoga), reduce gym intensity for 2–3 weeks
- Re-evaluate after 2–3 weeks

### If nutrition is the issue

- Have them log everything for 5 days — actual intake, not estimated
- Adjust calories or protein based on what's actually happening
- For fat loss stalls: NEAT may have dropped — push step count back up
- Refer to RD or nutrition-coach skill for precision

### If training stimulus is the issue

Pick **one** of these — don't change everything at once:

**Add load via different rep range**: client stuck at 5x5 squats? Run 4x8 for 4 weeks, then back to 3x5. New stimulus.

**Add volume in measured doses**: add 2–3 hard sets per stuck muscle per week. Re-evaluate in 3 weeks.

**Reduce volume strategically**: counterintuitively, sometimes cutting volume by 30% breaks a plateau. Recovery becomes possible, performance jumps.

**Change exercise variation**: swap conventional deadlift for trap bar, back squat for front squat. New movement = re-set adaptation curve.

**Tempo manipulation**: add a 3-sec eccentric and 1-sec pause for 4 weeks. New stimulus, same lift.

**Frequency adjustment**: take a stuck lift from 1x/week to 2x/week (one heavy day, one volume day). Or the reverse if recovery is the issue.

**Deload, then push**: a 1-week deload often unlocks a stalled lift more than any other change. Try this first.

### If goal-program mismatch

Re-run `program-design` with the layered specialty skills aligned to the actual goal. Don't try to patch a wrong program — replace it.

### If true plateau (rare)

Major structural change:
- Switch periodization model (linear → undulating, undulating → block)
- Run a "specialization cycle" — one block focused on bringing up the stuck lift, holding everything else
- Take a strategic 1-week off (full rest), then reintroduce

## The diagnostic conversation

Don't just throw fixes at the client. Walk them through the diagnostic out loud — they need to see the reasoning so they understand the why.

```
🔍 PLATEAU DIAGNOSTIC — [Client name]

WHAT'S STALLED
- [Lift/metric] hasn't moved since [date]
- Specifics: [last 4 weeks of data]

WHAT WE CHECKED (in order)
1. Adherence: [findings]
2. Recovery: [findings]
3. Nutrition: [findings]
4. Training stimulus: [findings]
5. Goal alignment: [findings]

THE LIKELY CAUSE: [1 sentence]

THE FIX (one change, not five):
- [Specific change]
- Run for [N] weeks
- Re-evaluate at [date]

WHAT WE'RE NOT CHANGING (and why):
- [...]
```

Keeping changes small lets you isolate what worked.

## When the client is impatient

> "I know this is frustrating. The temptation right now is to throw out the program and start over. We're not going to do that. Here's what I see, here's the one thing we're changing, and here's when we're checking back in. Trust the process. If this doesn't move it in 3 weeks, we go bigger."

## Special plateaus

### Strength plateau on a single lift while others progress

Usually a technical issue or weak point. Address with:
- Pause variations to overcome the sticking point
- Deficit work to build position strength
- Increased frequency on that lift specifically

### Plateau in fat loss after 8+ weeks of cutting

Often metabolic adaptation. Use a diet break (1 week at maintenance) to reset. Read `fat-loss`.

### Plateau in hypertrophy after a long building phase

Time for a deload, possibly a maintenance block, then back to building. Read `maintenance` and `hypertrophy`.

### Plateau in body recomp

Slowest progress curve in fitness. 4 weeks of no visible change is normal. Don't react to it. Read `body-recomp`.

## What this skill does NOT do

- Does not auto-rebuild the program at the first stall
- Does not make multiple changes at once (one variable at a time)
- Does not assume genetic limit until adherence, recovery, and nutrition are confirmed clean
- Does not work without honest data — if the client won't track, diagnostics are guesses
