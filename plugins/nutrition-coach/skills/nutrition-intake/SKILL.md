---
name: nutrition-intake
description: Use this skill at the very start of a user's nutrition journey to collect the assessment information needed to build a personalized meal plan. Triggers on phrases like "I want to start a nutrition plan", "set up my nutrition profile", "let's build my meal plan", "what info do you need from me", "begin nutrition coaching", or any first-time request to plan meals or track macros. Also triggers when the user has not yet provided age, weight, height, activity level, and goals — even mid-conversation. Always use this skill before macro-targets or weekly-meal-plan unless the required intake fields are already on file in the conversation.
---

# Nutrition intake

Collect the foundational information needed to design a customized meal plan. This is always step one — without it, calorie targets and macros cannot be calculated correctly.

## What to collect

Ask for these in a single conversational message, not as a long form. Group related questions together. If the user is planning for two people (e.g., themselves and a spouse), collect intake for each person separately.

**Demographics & body composition**
- Age (years)
- Biological sex (used for BMR calculation; ask sensitively)
- Height (cm or ft/in)
- Current weight (kg or lb)
- Body fat percentage if known (optional — improves accuracy)

**Activity & lifestyle**
- Job type (sedentary desk, on-feet, manual labor)
- Exercise frequency and type (cardio, strength, mixed; days per week)
- Average step count if tracked

**Goals**
- Primary goal: fat loss, muscle gain, body recomposition, maintenance, performance, or health/longevity
- Target weight (if applicable)
- Timeframe (weeks or months)

**Dietary preferences & restrictions**
- Cuisines they enjoy (this is where the cuisine skills slot in)
- Foods they dislike or won't eat
- Allergies and intolerances (be thorough — gluten, dairy, nuts, shellfish, soy, eggs)
- Religious or ethical patterns (halal, kosher, vegetarian, vegan, pescatarian)
- Cooking skill level and time available per meal

**Logistics**
- Number of people the plan is for (and ages, if children or elderly are involved)
- Budget considerations
- Kitchen equipment available
- Meal frequency preference (3 meals + 2 snacks vs. 4 meals, etc.)

**Health context (ask gently)**
- Any medical conditions relevant to diet (diabetes, hypertension, IBS, kidney issues, etc.)
- Medications that affect nutrition
- Pregnancy or breastfeeding status

## How to gather it

Open with: "Before I build your plan, I need to learn a few things about you. I'll ask in batches so it doesn't feel like a form."

Then ask in this order, one batch per message:
1. Demographics + body composition
2. Activity + exercise
3. Goals + timeframe
4. Food preferences + restrictions + allergies
5. Logistics + health context

After each batch, acknowledge what you heard before asking the next. This builds trust and lets the user correct misunderstandings early.

## Validate before moving on

Once you have all the information, summarize it back to the user in a structured block:

```
Profile summary
---------------
Age:           [...]
Sex:           [...]
Height:        [...]
Weight:        [...]
Activity:      [...]
Goal:          [...] over [...] weeks
Restrictions:  [...]
Cuisine likes: [...]
Household:     [...]
```

Ask: "Does that look right? Anything to add or change?"

Only proceed to `macro-targets` after the user confirms. If anything material is missing (especially age, sex, weight, height, activity, or goal) do not skip ahead — ask for the missing piece first.

## What NOT to do

- Do not estimate or invent missing values to "make it work"
- Do not skip the health context questions even when the user seems eager to get to the meal plan
- Do not bundle the intake into a single overwhelming list of 20 questions
- Do not collect this information again later in the same session if you already have it — reference what was provided

## Handing off

After the profile is confirmed, say: "Got it. I'll now calculate your calorie and macro targets based on this." Then invoke the `macro-targets` skill.

## Reference

For detailed intake question rationale and assessment protocols, see `references/intake-detail.md`.
