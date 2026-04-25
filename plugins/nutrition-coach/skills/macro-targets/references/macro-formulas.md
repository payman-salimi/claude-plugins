# Macro formulas — detailed reference

## BMR equations

### Mifflin-St Jeor (1990) — default
The most widely validated BMR equation for the general population.
- Male:   BMR = (10 × kg) + (6.25 × cm) − (5 × age) + 5
- Female: BMR = (10 × kg) + (6.25 × cm) − (5 × age) − 161

Accuracy: ±10% for ~80% of healthy adults.

### Katch-McArdle (1996) — for known body fat
Better for lean or muscular individuals because it bases BMR on lean mass.
- BMR = 370 + (21.6 × LBM_kg)
- LBM_kg = weight_kg × (1 − body_fat_decimal)

### Harris-Benedict (revised 1984) — fallback
Older and slightly less accurate than Mifflin-St Jeor; included for cross-checking.
- Male:   BMR = 88.362 + (13.397 × kg) + (4.799 × cm) − (5.677 × age)
- Female: BMR = 447.593 + (9.247 × kg) + (3.098 × cm) − (4.330 × age)

## Activity multipliers (PAL — physical activity level)

| Level | Multiplier | Real-world example |
|---|---|---|
| 1.2 | Sedentary | Desk job, mostly sitting, no formal exercise |
| 1.375 | Lightly active | Light walking + 1–2 short workouts/week |
| 1.55 | Moderately active | Active job OR 3–5 structured workouts |
| 1.725 | Very active | Hard daily training, 6+ sessions/week |
| 1.9 | Extra active | Twice-daily training, manual labor + training |

When in doubt, drop one level. Self-reported activity is consistently overestimated by 15–25%.

## Calorie adjustments by goal

| Goal | Adjustment | Notes |
|---|---|---|
| Aggressive cut | −25% | Cap at 8 weeks; refeed weekly |
| Moderate cut | −20% | Sustainable for 12+ weeks |
| Slow cut / recomp | −10% to −15% | Best for body recomposition |
| Maintenance | 0 | Use during stress, sleep deprivation, or to consolidate after a cut/bulk |
| Slow lean bulk | +5% to +10% | ~0.25% bodyweight gain per week |
| Moderate bulk | +10% to +15% | ~0.5% bodyweight gain per week |

Hard floor: never drop below ~1200 kcal/day for women or ~1500 kcal/day for men without medical supervision.

## Protein targets — evidence-based ranges

| Population | g/kg | g/lb |
|---|---|---|
| Sedentary adult, general health | 1.2–1.6 | 0.55–0.73 |
| Recreational exerciser | 1.4–1.8 | 0.64–0.82 |
| Strength athlete (gain) | 1.6–2.0 | 0.73–0.91 |
| Strength athlete (cut) | 2.0–2.4 | 0.91–1.1 |
| Endurance athlete | 1.4–1.7 | 0.64–0.77 |
| Older adults (60+) | 1.6–2.0 | 0.73–0.91 |
| Pregnancy (2nd/3rd trimester) | +25 g over baseline | — |

For overweight users (BMI > 30), calculate from goal weight or lean body mass to avoid inflating the target.

## Fat targets

Fats provide essential fatty acids and support hormone production. The minimum is non-negotiable.

| Approach | % of calories | Notes |
|---|---|---|
| Floor | 20% | Below this, testosterone/estrogen suffer |
| Standard | 25–30% | Default for most users |
| Higher-fat | 35–40% | If user prefers fewer carbs |
| Ketogenic | 70–75% | Specialty case — only if user requests it explicitly |

Within fats, aim for:
- Saturated fat: under ~10% of total calories (DGA guideline)
- Omega-3 (EPA/DHA): 250–500 mg/day from fish or supplements
- Trans fats: avoid (industrial trans fats are out of the food supply but check labels)

## Carbohydrate quality

Targets for carb grams come from the calorie remainder. Within that bucket:
- Whole grains, legumes, vegetables, fruit → priority
- Refined grains and added sugars → minimize (DGA: under 10% of calories from added sugar)
- Fiber: 14 g per 1000 kcal as a rule of thumb

## Hydration

| Activity | Water target |
|---|---|
| Baseline | 30–35 ml/kg/day |
| Light exercise | + 500 ml |
| Moderate exercise (1 hr) | + 750 ml |
| Heavy/hot exercise | + 1000 ml + electrolytes |

Caffeine and tea count toward hydration. Alcohol does not.

## Recalculation cadence

Recalculate targets when:
- Weight changes by more than 5%
- Activity level shifts (new job, new training program, injury)
- Goal changes
- Two consecutive weeks of zero progress (stall) — usually means TDEE has adapted downward by 5–15%

When stalled in a fat-loss block, reduce calories by another 5–10% OR increase activity by 1500–2500 kcal/week (e.g., daily 30-min walks). Don't do both simultaneously.
