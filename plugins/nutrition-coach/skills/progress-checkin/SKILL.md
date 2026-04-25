---
name: progress-checkin
description: Use this skill to run a weekly progress review and decide whether to adjust the user's calorie/macro targets or meal plan. Triggers on phrases like "weekly check-in", "let's review my progress", "I weighed in today", "I'm not losing weight", "review my week", "time for an update", "I'm stalled", or any request to evaluate how the plan is going. Use the actual progress data the user shares (weight changes, energy, hunger, adherence, sleep) and decide one of: hold steady, tighten the deficit, ease the deficit, switch to maintenance, or recalculate from scratch. Re-run macro-targets when changes are warranted.
---

# Progress check-in

Run a structured review of the past week and decide how to adjust. The decision logic matters more than the conversation — be specific about what's changing and why.

## Inputs to gather

Ask for these in a single message:

1. **Weight** (current, vs. last check-in)
2. **Adherence** — what % of meals/days did the user actually hit? (be honest, not optimistic)
3. **Energy levels** — 1–10 scale, average across the week
4. **Hunger** — was it manageable, or fighting all day?
5. **Sleep** — average hours, quality
6. **Training** — did all sessions happen? How did they feel?
7. **Anything notable** — travel, sickness, social meals, period for women (which can move scale weight ±2 kg)

Always normalize over 2-week trends, never single-week noise. A single weigh-in is data; two weigh-ins is a trend.

## Decision logic

### For fat loss goals

| Trend (2 weeks) | Adherence | Action |
|---|---|---|
| Losing 0.5–1% per week | High | Hold steady. The plan is working. |
| Losing >1% per week | High | Either ease the deficit by 5–10% OR add a refeed day. Faster than 1%/week starts costing muscle. |
| Losing <0.3% per week | High | Recalculate. TDEE may have adapted. Drop calories ~5–10% or add ~1500 kcal/week of cardio. |
| Not losing | Low (under 70%) | Don't change targets. Address adherence first. Ask: what's the friction point? |
| Not losing | High (>85%) | Recalculate from scratch — body composition or activity changed. |
| Energy/hunger crashing | Any | Ease the deficit or schedule a maintenance week. Sustainability beats speed. |
| Weight gain | Mixed | Audit liquid calories, weekend meals, hidden fats. Run a 2-week strict tracking experiment before adjusting numbers. |

### For lean gain goals

| Trend (2 weeks) | Adherence | Action |
|---|---|---|
| Gaining 0.25–0.5% per week | High | Hold steady. |
| Gaining >0.5% per week | High | Reduce calories by 5%. Faster gain is fat, not muscle. |
| Gaining <0.1% per week | High | Add 100–150 kcal/day. Often easiest from carbs around training. |
| Not gaining | Low | Address adherence. Are you missing meals? Eating slow? |
| Stalled with high adherence | High | Recalculate. May need 200–300 kcal more if NEAT compensated. |

### For maintenance / recomposition

Watch body composition cues, not just scale: clothes fit, photos, strength in the gym, energy. Adjust slowly — ±100 kcal at a time.

## What to say back

After the user shares their numbers, do this in order:

1. **Acknowledge** what worked. Specifically, not generically. "Hitting protein on 6 of 7 days is solid."
2. **Name the trend** in one sentence. "Two-week average: down 0.6% per week. That's right in the target range."
3. **State the decision clearly**. "We're holding targets where they are this week."
4. **Or, if changing**: "I'm dropping daily calories by 100 — from 1850 to 1750 — by reducing carbs to 175g. Protein and fats stay where they are." Then re-run `macro-targets` to recompute and update the meal plan.
5. **Surface one friction point** to address next week. "Your Friday adherence dropped — let's pre-plan that day specifically. Want me to lock in two simple Friday meals you can default to?"
6. **Ask one focused question** for the coming week. Not five. One.

## When to recommend a deload or break

Recommend a 1–2 week diet break (eat at maintenance, no deficit) when any of these are true:
- 8+ continuous weeks in a deficit
- Sleep quality has dropped meaningfully
- Training performance has plateaued or regressed for 2+ weeks
- Persistent hunger that's making adherence hard
- Mood/irritability noticeably worse

Frame it positively: this is a strategic move, not failure. Diet breaks improve hormonal markers and adherence.

## When to refer out

If the user mentions any of these, recommend they consult a registered dietitian or physician:
- Disordered relationship with food (obsessive tracking, food fear, binge episodes)
- Significant unintended weight changes
- Symptoms of nutrient deficiency (fatigue beyond expected, hair loss, missed periods, frequent illness)
- A medical condition that should be co-managed (diabetes, thyroid, kidney issues)

Be direct but kind: "What you're describing is outside what a meal plan should solve on its own. Worth talking to a registered dietitian — they can take the calorie/macro framework here and adjust for your specific situation."

## Format

End every check-in with this block:

```
This week's call
----------------
Direction:    [hold / tighten / ease / break / recalculate]
New targets:  [unchanged] OR [new numbers]
One focus:    [the single friction point we're addressing]
Next check:   [date, 7 or 14 days out]
```
