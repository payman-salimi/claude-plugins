# Intake question rationale

## Why each field matters

**Age** — affects BMR (older adults have lower resting metabolism) and influences guidance on protein needs, bone-supporting nutrients, and hydration.

**Biological sex** — the Mifflin-St Jeor BMR formula has separate constants for male and female; without it the calorie target will be off by ~150-300 kcal/day. Phrase the question respectfully: "For the BMR formula I need to ask about biological sex — male or female?"

**Height + weight** — both are direct inputs to BMR. Always confirm units (cm vs ft/in, kg vs lb) and convert silently for consistency.

**Body fat %** — when known, lets you use the Katch-McArdle formula instead, which is more accurate for lean or athletic individuals because it bases BMR on lean mass. Use Katch-McArdle when bf% is provided; fall back to Mifflin-St Jeor when it isn't.

**Activity level** — converts BMR to TDEE via an activity multiplier (1.2 sedentary, 1.375 lightly active, 1.55 moderately active, 1.725 very active, 1.9 athlete). Ask about both job type and structured exercise — an office worker who lifts 5x/week is "moderately active," not "very active."

**Goal & timeframe** — determines the calorie surplus/deficit. Evidence-based guidance: aim for 0.5–1% of body weight per week for fat loss; 0.25–0.5% per week for lean muscle gain. More aggressive targets are unsustainable and trigger lean-mass loss.

**Allergies and intolerances** — distinguish allergy (immune response, can be life-threatening) from intolerance (digestive discomfort) from dislike (preference). All three matter for the meal plan but the framing differs.

**Religious/ethical patterns** — these are non-negotiable. Treat them with the same firmness as allergies.

**Cooking skill + time** — determines recipe complexity. Pair with the `quick-prep-meals` skill if time is a constraint.

**Household composition** — if children are present, pair with `family-with-children`. If elderly, pair with `family-with-elderly`. Adjust portions and texture accordingly.

**Health context** — flag conditions that require professional oversight. The plugin must always recommend consulting a registered dietitian or physician for: diabetes, kidney disease, eating disorder history, pregnancy, breastfeeding, or any condition with prescribed dietary restrictions.

## Red flags that pause intake

If the user mentions any of the following, gently note that the meal plan output will be general guidance and they should review it with a healthcare provider before following it:
- A history of disordered eating
- Recent unintentional weight loss or gain
- Medications with known nutrient interactions (warfarin, MAOIs, lithium, certain diabetes meds)
- Pregnancy or active breastfeeding
- Diagnosed eating disorder, kidney disease, liver disease, or uncontrolled diabetes

The plugin still helps in these cases — it just frames its output as a starting draft for the healthcare provider, not a finished plan.
