# Nutrition Coach

A Cowork plugin that turns Claude into a personal nutrition coach. It collects your assessment info (age, weight, activity, goals, dietary restrictions), calculates your calorie and macro targets, builds a 7-day meal plan, generates a grocery list, walks you through recipes, and runs weekly check-ins.

The plugin is grounded in established nutrition science and the U.S. Dietary Guidelines for Americans 2025-2030.

## What's inside

### Core methodology skills
- **nutrition-intake** — collects the info needed to build a plan
- **macro-targets** — calculates BMR, TDEE, calorie target, and macro splits based on goals
- **weekly-meal-plan** — produces a 7-day plan (breakfast/lunch/dinner/snacks) tailored to targets and preferences
- **grocery-list** — aggregates ingredients across the week into a clean shopping list
- **recipe-details** — walks through prep, cook time, and step-by-step instructions for any meal in the plan
- **progress-checkin** — runs a weekly review and adjusts targets based on results

### Cuisine specialties
- **mediterranean-cuisine** — olive oil, fish, legumes, vegetables, whole grains
- **persian-cuisine** — herbs, rice, stews (khoresh), kebabs, traditional flavor profiles
- **indian-cuisine** — lentils, spices, vegetarian-forward, regional variations
- **asian-cuisine** — East/Southeast Asian patterns: rice, noodles, stir-fries, fermented foods
- **italian-cuisine** — pasta, antipasti, regional Italian patterns adapted for nutrition goals

### Household-type skills
- **quick-prep-meals** — every meal under 30 minutes total time
- **family-with-children** — kid-friendly portions, picky-eater strategies, balanced for growth
- **family-with-elderly** — softer textures where needed, nutrient density, common considerations for older adults

## How to use it

After installing, just talk to Claude:

- "I want to start a nutrition plan" — triggers the intake skill
- "Calculate my macros" — runs macro-targets
- "Build me a meal plan for next week" — generates a 7-day plan
- "Make a grocery list from this plan" — produces the shopping list
- "Show me the recipe for Tuesday's dinner" — recipe walkthrough
- "Time for my weekly check-in" — runs the progress review

You can stack the cuisine and household skills: "Build me a Persian-style weekly meal plan for a family with two children, all meals under 30 minutes."

## Output formats

The plugin produces both:
- A formatted **markdown** weekly meal plan (easy to read in chat)
- A structured **Excel (.xlsx)** weekly meal plan (so you can edit, print, or share it)

You'll be asked which one you want, or you can request both.

## Privacy

This plugin contains the methodology and reference materials only. None of your personal info — weight, age, dietary preferences, or generated meal plans — is bundled into the plugin. Each user runs it against their own session.

## References bundled

- `references/DGA26-30.pdf` — Dietary Guidelines for Americans 2025-2030 (U.S. Government, public domain)
- `references/nutrition-principles.md` — distilled summary of evidence-based nutrition principles and the DGA, encoding the working framework used by all the skills

The methodology is encoded directly into the skill bodies. The plugin functions as a self-contained reference; no proprietary materials are bundled.

## Licensing notes

See `LICENSING.md` for the full breakdown. Short version: the skills are MIT-licensed; bundled reference PDFs are public-domain government publications.

## Author

Built by Payman Salimi.
