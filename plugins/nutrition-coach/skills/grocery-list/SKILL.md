---
name: grocery-list
description: Use this skill to aggregate a weekly meal plan into a single, organized grocery list. Triggers on phrases like "make my grocery list", "shopping list", "what do I need from the store", "aggregate the ingredients", or any request for a consolidated shopping list from a meal plan. Run this after weekly-meal-plan has produced a plan. Group by store section (produce, protein, dairy, pantry, frozen) and consolidate duplicate ingredients across meals into single line items with total quantities.
---

# Grocery list

Turn a 7-day meal plan into one organized shopping trip. The user should be able to walk into a store with this list and not have to think.

## Steps

### 1. Pull every ingredient from the plan

Walk through each meal in the plan and list every ingredient with its quantity per serving × number of servings.

Example:
- Sunday breakfast (×2 people): Greek yogurt 200g × 2 = 400g
- Monday breakfast (×2 people): Greek yogurt 200g × 2 = 400g
- Wednesday snack (×2 people): Greek yogurt 150g × 2 = 300g
- → Total Greek yogurt: 1100g (round up to 1200g / one large container)

### 2. Consolidate duplicates

Add up the same ingredient across all meals. Round up to realistic package sizes:
- Olive oil → "1 bottle (500ml)" not "73 ml"
- Garlic → "1 head" not "8 cloves"
- Spices → "small jar if not on hand" with a note

### 3. Group by store section

Reorder so the user shops in one pass through the store. Use these sections in this order:

```
PRODUCE
  Vegetables: ...
  Fruit: ...
  Fresh herbs: ...

PROTEIN
  Meat & poultry: ...
  Fish & seafood: ...
  Eggs: ...

DAIRY & ALTERNATIVES
  Milk, yogurt, cheese: ...
  Plant-based: ...

PANTRY
  Grains: ...
  Legumes: ...
  Oils, vinegars, condiments: ...
  Spices: ...
  Nuts & seeds: ...
  Canned goods: ...

FROZEN
  ...

BAKERY
  ...

OTHER
  ...
```

### 4. Subtract what's already on hand

Always ask: "Do you want me to skip anything you already have? Spices, oils, nuts, and pantry staples are often half-stocked."

### 5. Estimate budget if asked

When the user asks for a budget estimate, give a rough total based on regional grocery prices, with a ±15% caveat. Don't pretend to know exact prices — that varies too much by store and city.

## Output format

```
Grocery list — week of [date]
For: [n] people
Estimated trip: ~[X] minutes, ~$[Y] (approx)

PRODUCE
  - Spinach, 1 bag (200g)
  - Cucumber, 2 medium
  - Lemons, 4
  - Fresh dill, 1 bunch
  ...

PROTEIN
  - Chicken thighs, boneless skinless, 1.5 kg
  - Salmon fillets, 600g
  - Eggs, 1 dozen
  ...
```

End the list with a "verify before checkout" reminder: "Quick scan — did I miss anything you wanted to add this week (snacks, treats, drinks)?"

## Excel version

When the meal plan was produced as .xlsx, populate the "Grocery list" sheet of that same workbook. Use formulas where possible so changing a meal in the plan auto-updates the grocery quantity.

## What NOT to do

- Do not list ingredients in the order they appeared in the plan — group by store section
- Do not output quantities at meal-level (200g + 200g + 200g) — always sum and round
- Do not include obviously-already-on-hand items (water, salt, pepper) without asking
- Do not skip the "anything else this week?" prompt
