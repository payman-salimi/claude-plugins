---
name: recipe-details
description: Use this skill to walk a user through how to actually cook a specific meal from their plan — ingredients, prep time, cook time, equipment, step-by-step instructions, and serving notes. Triggers on phrases like "how do I make Tuesday's dinner", "give me the recipe for", "show me how to cook this", "what's the recipe", "walk me through this dish", or any request for detailed prep instructions on a specific meal. Use this when the user has a meal plan and wants to actually cook a particular dish; pull cuisine-specific technique notes from the matching cuisine skill (mediterranean-cuisine, persian-cuisine, etc.) when applicable.
---

# Recipe details

Provide complete, foolproof recipe instructions for any meal in the plan. The output should be confident enough that a cook with average skill can follow it without Googling anything.

## What every recipe must include

1. **Title**
2. **Yield** (number of servings)
3. **Time breakdown**: prep time | cook time | total time
4. **Equipment needed** (assume a basic kitchen: stove, oven, knife, board, sheet pan, sauce pan, sauté pan, mixing bowls)
5. **Ingredients with measurements**, grouped if there are sub-components (e.g., "For the marinade", "For the sauce")
6. **Steps**, numbered, in chef-logical order
7. **Macros per serving** (calories, protein, carbs, fats)
8. **Serving suggestions** — what to plate alongside, garnish ideas
9. **Storage** — how long it keeps, how to reheat, whether it freezes

## Step-writing rules

- Each step does one logical thing. "Heat oil and add garlic" is one step. "Heat oil, add garlic, add onions, deglaze, simmer 20 min" is five steps.
- Lead with the verb: "Heat", "Whisk", "Slice", "Roast"
- Include the why when it's non-obvious: "Sear without moving for 3 minutes — this is what builds the crust"
- Specify temperatures and times: "medium-high heat" with a target indicator like "until shimmering" or "until edges turn translucent"
- Include doneness cues, not just times: "until the chicken is 74°C / 165°F at the thickest point" or "until the rice has absorbed all the liquid"
- Note typical mistakes in a one-line aside: "Don't crowd the pan — work in two batches if needed"

## Time budgeting

Be honest about time. If a chef-level cook can do it in 25 minutes, a home cook needs 35–40. Pad for:
- Reading the recipe (5 min)
- Mise en place / prep (10–15 min for most dinners)
- Cleaning between steps

Total time = prep + active cooking + passive cooking. Show all three.

## Cuisine-specific technique notes

Pull from the matching cuisine skill:
- **Persian**: rice technique (tahdig), saffron blooming, herb prep
- **Indian**: tempering spices (tadka), bhuna stage, balancing acid/heat/sweetness
- **Asian**: wok technique, oil flavoring, sauce ratios
- **Italian**: pasta water as a sauce ingredient, soffritto base, restraint with garlic
- **Mediterranean**: olive oil quality, finishing acid, herb timing

Note these where relevant — they're what separate a good version from a great one.

## Format

```
# [Dish name]
Yield: [n] servings · Prep: [x] min · Cook: [y] min · Total: [z] min

## Equipment
- [list]

## Ingredients
- [item] [quantity]
- [item] [quantity]
...

## Steps
1. ...
2. ...
3. ...

## Per serving
[X] kcal · P [X]g · C [X]g · F [X]g

## Serving
[plating + garnish notes]

## Storage
[fridge/freezer life + reheat method]

## Tip
[one helpful aside, optional]
```

## Multiple-recipe walkthroughs

When the user asks "give me all this week's recipes," produce them as a single document — one dish per page or section, with a table of contents at the top. Save as both markdown and a printable .docx if requested (use `anthropic-skills:docx`).

## What NOT to do

- Do not approximate macros per serving when ingredient quantities are precise. Compute them honestly.
- Do not write 17-step recipes when 8 steps would do. Combine trivial sub-steps.
- Do not skip doneness cues. "Cook for 10 minutes" without an indicator is a recipe that fails.
- Do not use vague qualifiers ("a bit of", "some", "to taste") on first-pass measurements. Give a specific starting amount, then say "adjust to taste at the end."
