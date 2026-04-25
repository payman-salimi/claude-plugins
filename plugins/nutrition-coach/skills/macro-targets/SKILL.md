---
name: macro-targets
description: Use this skill to calculate the user's BMR, TDEE, daily calorie target, and macronutrient split (protein, carbs, fats) based on their intake profile and goals. Triggers on phrases like "calculate my macros", "what are my calorie targets", "how many calories should I eat", "set my protein target", "give me my numbers", or any request that requires turning intake data into specific daily targets. Use this skill after nutrition-intake confirms the profile, and before weekly-meal-plan. Recalculate whenever a user's weight, activity, or goal changes by more than ~5%.
---

# Macro targets

Turn the intake profile into concrete daily targets: total calories, protein grams, carbohydrate grams, and fat grams. These targets feed directly into the weekly meal plan.

## Calculation steps

Run these in order. Show your work to the user — the transparency builds trust and lets them sanity-check the math.

### Step 1: BMR (basal metabolic rate)

Use **Mifflin-St Jeor** by default:
- Male:   BMR = (10 × weight_kg) + (6.25 × height_cm) − (5 × age) + 5
- Female: BMR = (10 × weight_kg) + (6.25 × height_cm) − (5 × age) − 161

Use **Katch-McArdle** when body fat % is known (more accurate for lean/athletic users):
- BMR = 370 + (21.6 × lean_body_mass_kg)
- where lean_body_mass_kg = weight_kg × (1 − bodyfat_decimal)

### Step 2: TDEE (total daily energy expenditure)

TDEE = BMR × activity multiplier

| Activity level | Multiplier | Description |
|---|---|---|
| Sedentary | 1.2 | Desk job, no exercise |
| Lightly active | 1.375 | Light exercise 1–3 days/week |
| Moderately active | 1.55 | Moderate exercise 3–5 days/week |
| Very active | 1.725 | Hard exercise 6–7 days/week |
| Athlete | 1.9 | Twice-daily training or physical job + training |

If the user is between two levels, pick the lower one — most people overestimate their activity.

### Step 3: Calorie target based on goal

| Goal | Adjustment from TDEE |
|---|---|
| Aggressive fat loss | −20% to −25% (only for short blocks, max 8 weeks) |
| Moderate fat loss | −15% to −20% |
| Slow fat loss / recomposition | −10% |
| Maintenance | 0% |
| Slow lean gain | +5% to +10% |
| Moderate lean gain | +10% to +15% |

Sanity-check the result against the rate of change:
- Fat loss: aim for 0.5–1% of bodyweight per week
- Lean gain: aim for 0.25–0.5% of bodyweight per week
- Faster than this → muscle loss (cutting) or excess fat gain (bulking)

If the user requested an unrealistic timeframe ("lose 30 lbs in 6 weeks"), explain the math: at a sustainable 1% per week, that's a ~170-180 lb starting weight and 4-6 months. Offer the realistic timeline.

### Step 4: Protein

Protein is calculated first because it's the most important and most non-negotiable macro.

| Goal | Protein (g per kg of bodyweight) | Protein (g per lb) |
|---|---|---|
| Sedentary general health | 1.2–1.6 | 0.55–0.73 |
| Active / strength training | 1.6–2.2 | 0.73–1.0 |
| Fat loss (preserve lean mass) | 2.0–2.4 | 0.91–1.1 |
| Older adults (60+) | 1.6–2.0 | 0.73–0.91 |
| Lean gain | 1.6–2.0 | 0.73–0.91 |

For users carrying significant body fat, calculate protein from goal weight or lean mass, not total weight, to avoid inflating the number.

Multiply protein grams × 4 to get protein calories.

### Step 5: Fats

Set fats based on percentage of total calories:
- Minimum: 20% of calories (below this, hormone production suffers)
- Default: 25–30% of calories
- Higher fat / low carb preference: up to 40%

Fat grams = (calorie_target × fat_percent) / 9

### Step 6: Carbs (the remainder)

Carb_calories = total_calories − protein_calories − fat_calories
Carb_grams = carb_calories / 4

If the carb target comes out absurdly low (under ~50 g) for someone who isn't doing keto on purpose, raise the calorie target or lower fats — that result usually means the inputs are off.

### Step 7: Fiber

Aim for 14 g per 1000 kcal, or:
- Adult women: 25 g/day minimum
- Adult men: 38 g/day minimum

This is a target, not a strict cap — going higher is fine.

### Step 8: Water

Baseline: 30–35 ml per kg of bodyweight, plus 500–750 ml per hour of intense exercise.

## Output format

Present targets in this exact block:

```
Daily targets
-------------
Calories:  [X] kcal
Protein:   [X] g  ([Y]% of calories)
Carbs:     [X] g  ([Y]% of calories)
Fats:      [X] g  ([Y]% of calories)
Fiber:     [X] g
Water:     [X] L

Math
----
BMR (formula):     [X] kcal
TDEE (× [Y]):      [X] kcal
Goal adjustment:   [+/−Z]%  →  [X] kcal/day
Expected rate:     [X] lb/kg per week
Estimated arrival: [date / week count] at goal
```

Then add a one-line note: "If your weight isn't moving as expected after 2 weeks, we'll recalculate."

## What to do for couples

If the user is planning for two people (themselves and a spouse), produce two separate target blocks side by side. Their meals will overlap but their portion sizes will differ.

## Handing off

After targets are set and the user accepts them, say: "Now I'll build your weekly meal plan around these targets." Then invoke the `weekly-meal-plan` skill.

## Reference

For detailed formulas, edge cases, and adjustment logic, see `references/macro-formulas.md`.
