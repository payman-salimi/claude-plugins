---
name: form-correction
description: Analyze exercise form from video or photos and return prioritized corrections with coaching cues and drills. Use this whenever a client shares footage or stills of themselves lifting, pastes pose-analyzer JSON, or asks anything about their technique — "can you check my form", "how does my squat look", "correct my deadlift", "review my lift", "my form feels off", "is my back rounding", "why does my knee cave" — even if they haven't run the pose-analyzer tool yet (guide them to it, or coach from the images). The bundled tools/pose-analyzer.html extracts MediaPipe joint angles in the browser; the client uploads the exported JSON plus key-frame screenshots. Layer with injury-prep whenever pain is mentioned.
---

# Form Correction

Turn video into coaching. The client runs their footage through the pose-analyzer tool, which extracts 33 body landmarks and computes joint angles per frame. They hand that data to Claude — Claude does the coaching interpretation.

## The two-step workflow

### Step 1 — Client runs the pose analyzer

The tool lives at `tools/pose-analyzer.html` inside this skill's folder. Give the client the full path (resolve it from wherever this SKILL.md was loaded; offer to open it for them if you have a browser or `open` command available). It runs entirely in the browser — no video leaves their machine. Steps:

1. Open `pose-analyzer.html` in Chrome (recommended; Safari may block the WASM download on `file://` pages — if so, serve the folder with `python3 -m http.server` and open it via `localhost`)
2. Upload their exercise video (MP4, MOV, WebM — under 5 min)
3. Select the exercise type and camera angle (side / front / diagonal)
4. Click **Analyze** — the tool samples 5 frames per second and overlays landmarks on each
5. Review the key frames it highlights (start, bottom, mid, top, worst spine lean, worst asymmetry, end)
6. Click **Export JSON + Instructions** — downloads `form-analysis-<exercise>-<timestamp>.json`
7. Screenshot 2–4 of the highlighted key frames directly from the tool (the thumbnails are numbered; those numbers match `screenshotIndex` in the JSON)

### Step 2 — Client uploads to Claude

Client pastes the `form-analysis.json` contents and uploads the screenshots into the conversation. This skill takes it from there.

---

## What Claude receives — reading the JSON

The JSON has five sections (this mirrors what the tool actually emits; the full schema is in `references/mediapipe-integration.md`):

```
{
  "exercise": "squat",
  "cameraAngle": "side" | "front" | "diagonal",
  "videoInfo": { filename, duration_s, framesAnalyzed, sampledFps, resolution },
  "summary": {
    "minKneeAngle": { left, right },        // degrees — bottom of rep
    "maxKneeAngle": { left, right },        // degrees — lockout
    "minHipAngle":  { left, right },        // hip crease angle at depth
    "maxHipAngle":  { left, right },
    "avgSpineLean_deg": number,             // trunk lean from vertical, averaged over all frames
    "maxSpineLean_deg": number,             // worst single-frame lean
    "asymmetry": { knee_deg, hip_deg, shoulder_deg }  // max L vs R delta seen
  },
  "keyFrames": [                            // up to 7 frames at diagnostic moments
    {
      "label": "start" | "bottom" | "mid" | "top" | "worst_spine" | "worst_asym" | "end",
      "timestamp_s": number,
      "screenshotIndex": number,            // matches the numbered thumbnail the client screenshots
      "angles": { leftKnee, rightKnee, leftHip, rightHip, leftElbow, rightElbow, leftShoulder, rightShoulder, spineLean },
      "landmarks": [ { x, y, z, visibility } × 33 ]
    }
  ]
}
```

Angles are in degrees, computed from normalized (x, y) coordinates. `spineLean` is 0° upright and 90° horizontal — it is the trunk forward lean referred to throughout this skill. Z is estimated depth (unreliable without a stereo camera — treat as a supporting signal only). Any angle where a contributing landmark has `visibility < 0.5` is `null`; when a key angle is null, say so rather than guessing. Landmarks follow MediaPipe's 33-point schema — the index map is in `references/mediapipe-integration.md`.

If the client's camera angle is `front`, sagittal angles (spine lean, hip angle) are unreliable but valgus and asymmetry are trustworthy; from a `side` view it's the reverse. Weight your read accordingly (details in `references/joint-angle-standards.md`, "Camera angle quality notes").

---

## How to analyze — exercise by exercise

### Squat (back squat, front squat, goblet, box)

Read in this order at the **bottom frame**:

1. **Knee angle** — target ≥ 90° parallel (thigh parallel to floor). Below 70° = deep squat, check intentionality. Above 100° = not reaching depth.
2. **Knee tracking** — visually from screenshots, does the knee track over the second toe? JSON `asymmetry.knee_deg` > 10° = one knee caving (most reliable from a front camera angle).
3. **Hip angle** — target 90–110° at depth for upright torso squat. Higher number = more forward lean.
4. **Spine lean (trunk forward lean)** — target < 45° from vertical for back squat; < 30° for front/goblet. Above 60° = "good morning" — bar path is compromised.
5. **Depth consistency** — compare min knee angle across reps. > 15° variation = inconsistent depth.
6. **Asymmetry** — L/R knee or hip delta > 10° = lateral imbalance, possible mobility restriction or weakness.

**Common squat errors and coaching cues:**

| Error | Landmark signature | Cue |
|---|---|---|
| Knee cave (valgus) | asymmetry.knee > 10°, knee x-coordinate moves medial | "Spread the floor with your feet. Push your knees out into your elbows on the way up." |
| Forward lean | spineLean > 55° at the bottom frame | "Chest up. Imagine a string pulling the top of your head to the ceiling." |
| Butt wink | spine inflects at bottom (Z-landmarks shift) | "Stop the descent 5° before your pelvis tucks. Work ankle mobility — couch stretch daily." |
| Heels rising | ankle landmarks shift anterior | "Elevate heels 1–2 cm with plates and work calf/ankle mobility." |
| Not reaching depth | minKneeAngle > 100° | "Box squat to a target depth. Hip flexor and ankle mobility are likely the limiters." |
| Lateral shift | midpoint hip x-coordinates asymmetric | "Likely weak glute on the shift side. Add single-leg work: step-ups, single-leg RDL." |

### Deadlift (conventional, sumo, Romanian)

Read at **start of pull** (bar leaves floor) and **lockout**:

1. **Hip hinge angle** — at setup: hip angle 45–70° (conventional), 30–50° (sumo). Shallower = squat-morning hybrid.
2. **Spine lean** — should stay neutral through pull. spineLean sudden jump mid-pull = early hip rise, "stiff-leg" pattern.
3. **Bar path** — landmark for wrist/hand x-coordinate should stay close to mid-foot. Drifting forward = lat engagement missing.
4. **Lockout** — at top frame: knee and hip fully extended (angles ~175–180°), no hyperextension of lumbar.
5. **Head/neck position** — nose landmark should track a neutral cervical spine: looking slightly down at setup, not cranked up.

**Common deadlift errors:**

| Error | Signature | Cue |
|---|---|---|
| Hips rise first (early hip rise) | hip angle increases faster than knee angle in first frames | "Push the floor away — think leg press at the start, not a pull." |
| Rounded lower back | lumbar inflection visible in screenshots | "Brace: big breath in, 360° pressure into belt/waistband before you pull." |
| Bar drifts forward | wrist landmark drifts anterior | "Scrape your shins. Lat pulldown cue: pack your armpits." |
| Hyperextending at lockout | hip angle > 185°, lumbar goes into extension | "Lock out with glutes, not by leaning back. Squeeze glutes hard at the top." |
| Head cranked back | nose y-coordinate elevated | "Eyes neutral — look at a spot 3–4 feet in front of you on the floor." |

### Bench press

Read at **bottom of press** (bar touches chest) and **lockout**:

1. **Elbow flare** — at bottom: shoulder angle (elbow-shoulder-hip) should be 45–75°. > 90° = too flared, shoulder stress.
2. **Wrist alignment** — wrist landmark should be stacked over elbow (x close). Forward = wrist strain.
3. **Shoulder retraction** — scap retracted: shoulder blades should be pinched. Hard to read from landmarks alone — use screenshots.
4. **Back arch** — note trunk lean and hip elevation. Excessive arch (spine ≥ 10 cm off bench) = powerlifting arch, note intentionality.
5. **Bar path** — should touch lower chest (nipple line), not neck.

### Pull-up / Row

Read at **top of pull** (chin over bar / elbows at 90°):

1. **Elbow angle** — target ≤ 90° at top. > 110° = partial rep.
2. **Shoulder elevation** — at top: no shoulder shrug. Shrug = traps dominating, lats not engaged.
3. **Body swing** — consistency of torso angle frame-to-frame. Large variance = kipping / momentum.

### Overhead press

1. **Elbow position at start** — shoulder angle at rack position: elbows slightly in front of bar, not flared back.
2. **Lockout** — arms fully extended overhead, biceps by ears (check shoulder x-landmark alignment with wrist).
3. **Lower back extension** — no lumbar hyperextension to push bar overhead.

### Hinge / RDL / Hip thrust

1. **Hip angle** — RDL: hip angle at bottom 30–60°; hip thrust: full extension at top, hip angle ~175°.
2. **Knee tracking** — minimal during RDL. Large knee bend = turning it into a squat.
3. **Spine neutral** — no rounding at bottom of RDL. Shoulders should track slightly in front of hips.

---

## Scoring

Before writing the output, compute a **Form Score** from 0–100.

Start at 100 and deduct points per issue found:

| Issue | Deduction |
|---|---|
| Each major alignment error (spine rounding, knee cave, early hip rise) | −15 |
| Each moderate error (forward lean over target, partial ROM, elbow flare) | −10 |
| L/R asymmetry > 10° at a key joint | −8 |
| Minor technical fault (heel rise, head position, grip width) | −5 |
| Low landmark visibility on a key joint (< 0.5 confidence) | −3 (uncertainty penalty) |

Cap deductions at 0 — score never goes below 0. Round to nearest integer.

**Score bands:**

| Score | Label | Action |
|---|---|---|
| 90–100 | Excellent | Acknowledge and move on. No corrective plan needed. |
| 75–89 | Good | 1 fix. One coaching cue, one drill. |
| 55–74 | Needs work | 2–3 fixes. Prioritized cues + corrective drills. |
| < 55 | Rebuild first | Flag the top issue clearly. Reduce load and drill the movement pattern before adding weight. |

---

## Output format

```
📹 [Exercise] Form Score: [N]/100 — [Excellent / Good / Needs Work / Rebuild First]

[If score ≥ 90]
Your form is on point. [1 sentence on what's working well.] Keep training — re-film in 4 weeks.

[If score < 90]
[1 sentence on what's working — always acknowledge something.]

FOCUS FOR NEXT SESSION
[The single highest-impact fix, in plain language. One sentence max.]
Cue: "[10 words or less — tactile, physical, something they can feel]"
Drill: [Exercise] — [sets × reps]

[If score < 75, add a second fix:]
ALSO WATCH
[Second issue in one sentence.]
Cue: "[10 words or less]"
Drill: [Exercise] — [sets × reps]

[If score < 55, replace the above with:]
BEFORE ADDING WEIGHT
[Explain the core problem in 2 sentences max. Be direct, not alarming.]
Step 1: [Specific load or volume reduction — e.g., "Drop to 60% of current load"]
Step 2: [The foundational drill to rebuild the pattern — sets × reps × frequency]
Re-film when this feels automatic.
```

Cap it at 2 fixes per session: motor learning research and every coach's experience agree that a lifter can hold one or two cues in their head under load, not five. Always name something that's working — a client who only hears faults stops sending video. Keep the entire response under 150 words so it fits on a phone screen at the gym.

---

## When screenshots alone are submitted (no JSON)

If the client uploads images without running the pose analyzer, still help — but note the limitation:

- Analyze from the visual frame only (joint angles estimated, not measured)
- Ask what the exercise and goal are
- Still use the same output format
- Note at the bottom: *"Run the pose analyzer tool for precise joint angle measurements — this analysis is based on visual estimation only."*

---

## Layering with other skills

| Client situation | Layer in |
|---|---|
| Client reports pain in the movement | `injury-prep` — check if the form error is causing or caused by pain |
| Beginner, first time filming | `beginner-foundations` — form errors are expected; keep the fix list to 2 items max |
| Elite athlete drilling competition lift | `elite-athlete` — higher tolerance for aggressive technique choices (e.g., bar arc in snatch) |
| Post-surgical client | `post-knee-surgery` or relevant skill — form errors may be compensatory, don't over-correct |

---

## Disclaimer — always include once

> "This is coaching feedback based on landmark data from your video — not a medical diagnosis. If you experience sharp, radiating, or worsening pain during any lift, stop and see a physician or physical therapist before continuing."

---

## What this skill does NOT do

- Does not diagnose injury from form
- Does not replace a trained eye watching live — video angle matters, and bad camera angles produce bad data
- Does not require a perfect camera setup — but front-facing or side-facing 90° views produce the most reliable landmark data. Diagonal is acceptable. Behind-the-client is worst.
- Does not analyze more than one exercise per session — pick the priority lift and analyze that one
