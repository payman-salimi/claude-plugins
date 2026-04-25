---
name: weekly-meal-plan
description: Use this skill to generate a customized 7-day meal plan once intake and macro targets are set. Triggers on phrases like "build my meal plan", "create the weekly plan", "give me 7 days of meals", "plan my meals for next week", "make me a meal plan", or any request to produce a multi-day meal schedule. Always run nutrition-intake and macro-targets first if those are missing. Output both a markdown plan and an Excel (.xlsx) plan unless the user specifies a single format. Layer in the cuisine and household-type skills (mediterranean-cuisine, persian-cuisine, indian-cuisine, asian-cuisine, italian-cuisine, quick-prep-meals, family-with-children, family-with-elderly) when the user has specified those preferences.
---

# Weekly meal plan

Build a 7-day meal plan that hits the user's calorie and macro targets, respects their preferences and restrictions, and reads like something a thoughtful coach would hand them — not a generic template.

## Inputs required

Before generating, confirm you have:
- Daily targets (calories, protein, carbs, fats) from `macro-targets`
- Dietary restrictions and allergies from `nutrition-intake`
- Number of people the plan serves (if more than one, capture each person's targets)
- Cuisine preferences (slot in the relevant cuisine skill)
- Household type (slot in `family-with-children` and/or `family-with-elderly` if applicable)
- Time/skill constraints (slot in `quick-prep-meals` if needed)

If any of these are missing, ask before building. Do not invent.

## Plan structure

A complete week contains:
- 7 days × (breakfast + lunch + dinner + 1–2 snacks)
- Each meal lists: name, ingredients with quantities, calories, protein, carbs, fats
- Daily totals row showing how the day stacks up against targets
- A "swap" column with one easy substitution for each meal

Aim for daily totals within ±5% of each macro target. Hitting protein exactly is the highest priority — overshoot calories slightly rather than underdeliver protein.

## Design principles

**Repetition is a feature, not a bug.** Real-world adherence is higher when the same ingredients show up 3–4 times per week. Plan a "core grocery list" of ~15–20 ingredients and recombine them across meals. Avoid the rookie mistake of designing 21 unique meals — that produces a beautiful PDF and a $400 grocery bill.

**Anchor each day on a protein source.** Pick the protein first (chicken, fish, eggs, lentils, tofu, etc.), then build carbs and vegetables around it. Most amateur plans fail because they design the carb first and the protein gets squeezed.

**Prep convergence.** Plan at least 2–3 days where one cook session covers multiple meals (e.g., Sunday: roast chicken + grain + veg → Monday lunch + Tuesday dinner). Mark these clearly.

**Variety over the week, simplicity within the day.** Same breakfast 3–4 days a week is fine. Different dinners is where variety matters — that's the meal people savor.

**Plate composition (DGA-aligned)**
- ½ plate vegetables and fruit
- ¼ plate lean protein
- ¼ plate whole grain or starchy vegetable
- 1 thumb of healthy fat (olive oil, avocado, nuts)

**Hydration cues.** End each day's row with the water target as a reminder.

## Output: markdown version

Render as a single document with a top-of-page summary and 7 day blocks. For couples, show two columns of portions.

```
# Weekly meal plan — [date range]
For: [name(s)]
Targets: [X] kcal · P [X]g · C [X]g · F [X]g per person

## Sunday
| Meal       | Dish                              | Cal  | P  | C  | F  | Notes |
|------------|-----------------------------------|------|----|----|-----|-------|
| Breakfast  | Greek yogurt bowl with berries    | 350  | 28 | 38 | 8   |       |
| Lunch      | Chicken & quinoa Mediterranean    | 520  | 42 | 55 | 16  | prep |
| Dinner     | Salmon, roasted veg, sweet potato | 620  | 40 | 50 | 28  | core |
| Snack      | Apple + 2 tbsp almond butter      | 250  | 7  | 28 | 14  |       |
|            | Daily total                       | 1740 | 117| 171| 66  |       |
```

Repeat for each day. Mark prep-ahead meals with `prep`, leftover meals with `→Mon` notation.

## Output: Excel (.xlsx) version

Always also produce a workbook saved to the project folder. Structure:
- **Sheet 1: Summary** — targets, weekly totals, grocery preview
- **Sheet 2: Plan** — 7 columns (Sun–Sat), rows for each meal, with formulas computing daily totals
- **Sheet 3: Grocery list** — auto-aggregated from Sheet 2 (ingredient × total quantity needed)
- **Sheet 4: Recipes** — link/anchor to each unique meal name with prep steps

Use the `anthropic-skills:xlsx` skill to write the workbook. Save it to `/Users/[user]/Documents/Claude/Projects/[project]/Weekly_Meal_Plan_[date].xlsx` so it persists.

After writing the file, share a `computer://` link.

## Tailoring to cuisines and households

When the user has specified cuisines, source meal ideas from the matching cuisine skills. For example, if the user picked Persian + Indian, alternate days between the two — don't blend them within a single meal unless the user explicitly enjoys fusion. Read the appropriate cuisine skill's reference for ingredient lists and traditional dishes.

For families with children, follow `family-with-children` portion guidance. For elderly household members, follow `family-with-elderly` for texture and nutrient density.

## What NOT to do

- Do not invent calorie or macro values for foods. Use the FoodData Central / standard nutrition values; if you're not sure, say so and round.
- Do not design 21 unique meals. Repetition is realistic.
- Do not skip protein anchoring. A meal under 25 g protein at lunch or dinner is a flag.
- Do not include foods the user listed as disliked or restricted, even "just to add variety."
- Do not produce only the markdown plan when the user asked for both formats — always produce the xlsx too.

## Reference

For meal templates, common protein sources by cuisine, and prep-convergence patterns, see `references/meal-templates.md`.
