---
name: quick-prep-meals
description: Use this skill when the user wants every meal in the plan to come together in 30 minutes or less of total time (prep + cook). Triggers on phrases like "I don't have much time to cook", "quick meals", "under 30 minutes", "fast meal plan", "weeknight dinners", or any signal that time is the binding constraint. Layer this skill on top of weekly-meal-plan and recipe-details — it doesn't generate plans on its own, it constrains them. Bias toward sheet-pan, stir-fry, sandwich/wrap, and grain-bowl formats; rule out long-braise, stew, slow-roast, and dough-based dishes from scratch.
---

# Quick prep meals

Constrain every meal in the plan to 30 minutes or less total time. This is a layering skill — combine it with `weekly-meal-plan` and any cuisine skill the user picked.

## What "30 minutes" means

Total time = walking into the kitchen → plate on table. Not "active cooking time," not "after the oven preheats." Be honest about it. If a recipe needs a 20-minute marinade + 15 minutes of cooking, the total is 35 minutes — that's too long for this skill.

## Formats that work

These reliably hit the 30-minute target:

| Format | Why it works |
|---|---|
| Sheet-pan dinners | Single tray, one timer, hands-free 20 min |
| Stir-fries | All cooking happens in 6–10 minutes once mise is ready |
| Grain bowls (assembly) | Use pre-cooked grain (batched on Sunday or store-bought) |
| Wraps / pita / sandwich plates | No cooking past the protein |
| Skillet one-pots (chicken + greens + grain) | 20 min start to finish |
| Egg-based dinners (frittatas, fried-egg-rice) | 12–18 minutes |
| Cold protein + warm starch (canned tuna + microwaved sweet potato + salad) | 8 minutes flat |
| Pasta with quick sauce (e.g., aglio e olio, cacio e pepe) | 15 minutes |

## Formats to avoid

These break the 30-minute budget:

- Stews, braises, slow roasts (60+ minutes minimum)
- Anything with rising dough (pizza from scratch, fresh bread)
- Whole-roast proteins (whole chicken, beef roasts, turkey)
- Long-marinated kebabs and tagines
- Dishes requiring deep-frying setup
- Recipes with 4+ separate sub-components

## Quick wins for prep

Encourage the user to do a 30-minute Sunday prep that unlocks 5–10 quick meals:
- Cook 2 cups of dry grain (rice, quinoa, farro) → covers 4 meals
- Roast a sheet pan of veg (sweet potato cubes, broccoli, peppers) → covers 3 meals
- Hard-boil 8 eggs → covers snacks and breakfast
- Cook 1 kg of chicken thighs (sheet pan, 25 min) → covers 4 meals

With those four jobs done, weeknight cooking becomes assembly: warm the grain, top with the protein, add the veg, drizzle a sauce. 8–10 minutes per meal.

## Common 5-minute sauces

These sauces transform plain proteins and grains. All take under 5 minutes.

- **Tahini-lemon**: 3 tbsp tahini + juice of ½ lemon + warm water + salt + grated garlic
- **Yogurt-herb**: ½ cup plain Greek yogurt + chopped herbs + lemon + olive oil + salt
- **Chimichurri**: parsley + cilantro + garlic + red wine vinegar + olive oil + chili flake
- **Soy-ginger**: soy sauce + rice vinegar + grated ginger + sesame oil + a pinch of sugar
- **Pesto-style** (any green): basil/spinach/parsley + olive oil + nuts + parmesan + lemon

## Output cues

When generating the plan or recipes, mark every meal with `quick` and show prep + cook + total time on the same line. If a meal cannot meet the 30-minute target, swap it before publishing the plan — don't include and apologize.

## Honest constraints

Tell the user upfront what they're trading off:
- Less variety on the plate per meal (typically 3–4 ingredients vs. 6–8)
- More reliance on a Sunday prep block
- Fewer braised/stewed dishes (which is a flavor depth lost)
- More pantry staples (canned beans, frozen veg, jarred sauces) — these are not lower quality, just less romantic

A user who picks this skill is choosing weeknight reality over Instagram aesthetics. Build accordingly.
