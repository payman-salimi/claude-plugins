# Elite Coach

A complete personal training plugin. Claude becomes a credentialed coach who runs proper intake, builds tailored programs, and adapts to every common population — beginners, elite athletes, older adults, pregnancy/postpartum, post-surgical, injured, and certified trainers wanting to level up.

## What it does

1. **Onboards a client properly** — runs a thorough intake (PAR-Q+ style screening, health history, lifestyle, training history, dietary log, equipment access).
2. **Diagnoses the situation** — picks the right specialty lens (injury, hypertrophy, fat loss, recomp, return-to-training, etc.).
3. **Builds a real program** — weekly split, sets, reps, RPE/percentages, rest, cardio prescription, deloads — output as both a chat-ready markdown plan and an Excel tracker.
4. **Holds the client accountable** — runs weekly check-ins, detects plateaus, decides whether to push harder, hold, or regress.

## Skills included

### Core orchestration
- **client-intake** — collects everything needed before programming.
- **program-design** — the master planner. Composes specialty skills into a real program.
- **weekly-checkin** — accountability + progressive overload decisions.

### Population specialties
- **injury-prep** — back pain, knee pain, common joint issues.
- **prenatal-postpartum** — pregnant clients and postpartum return.
- **post-knee-surgery** — ACL, meniscus, TKR return-to-training.
- **older-adults** — 60+ training (strength, balance, longevity).
- **beginner-foundations** — first-time lifters / true novices.
- **elite-athlete** — high-level conditioned individuals.
- **coach-development** — for certified trainers who want to level up their own programming.

### Goal specialties
- **hypertrophy** — muscle gain.
- **fat-loss** — fat loss with muscle preservation.
- **maintenance** — hold the line on strength, body comp, conditioning.
- **body-recomp** — simultaneous fat loss + muscle gain.
- **functional-training** — pure functional / movement-quality work.

### Adjustment
- **plateau-detection** — diagnoses why progress stalled and modifies the plan.

## How to use

Just ask. Claude will pick the right skill(s) automatically based on what you say:

- *"I want to start lifting"* → triggers **client-intake**, then **beginner-foundations** + **program-design**.
- *"I'm 32 weeks pregnant and want to keep training"* → triggers **prenatal-postpartum**.
- *"My squat hasn't moved in 6 weeks"* → triggers **plateau-detection**.
- *"I want to lose 15 lbs in 12 weeks"* → triggers **fat-loss** + **program-design**.

## Outputs

Every program comes out two ways:

1. **Markdown in chat** — the format from your project instructions: warm-up, main block, finisher, cool-down, coaching note.
2. **Excel tracker** — a `.xlsx` to log sets, reps, weights, and RPE week-over-week.

## Source material

Skills draw on widely accepted exercise science principles in personal training, hypertrophy, strength and conditioning, plus evidence-based behavior change frameworks and published research on training adherence.
