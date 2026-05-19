# MediaPipe Pose Landmarker — Integration Reference

Technical reference for the pose-analyzer.html tool. Describes the MediaPipe model used, landmark schema, angle computation, and export format.

---

## Model

**Package**: `@mediapipe/tasks-vision` v0.10.x  
**Model**: `pose_landmarker_lite` (float16) — balance of speed and accuracy; runs in browser via WASM  
**Inference mode**: `IMAGE` — each video frame processed independently  
**Running mode**: client-side only — no data leaves the browser  
**CDN**: `https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.3/vision_bundle.js`  
**WASM path**: `https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.3/wasm`  
**Model file**: `https://storage.googleapis.com/mediapipe-models/pose_landmarker/pose_landmarker_lite/float16/1/pose_landmarker_lite.task`

---

## Browser requirements

- **Chrome 90+** (recommended) — full WebAssembly + WebGL GPU support
- **Firefox 90+** — works, CPU only (no GPU delegate)
- **Safari** — may block WASM from CDN on local file:// pages; serve via `python3 -m http.server` if issues occur
- **Edge** — same as Chrome

For local file usage (double-click to open), Chrome with `--allow-file-access-from-files` flag is most reliable if CDN WASM fails to load.

---

## The 33 landmarks

MediaPipe outputs normalized coordinates (0.0–1.0 relative to frame dimensions) for 33 body points:

| Index | Name | Key use |
|---|---|---|
| 0 | nose | head position, gaze proxy |
| 1–4 | eye landmarks | head alignment |
| 5–8 | ear landmarks | head rotation |
| 9 | mouth_left | — |
| 10 | mouth_right | — |
| **11** | **left_shoulder** | spine angle, shoulder angle, push/pull analysis |
| **12** | **right_shoulder** | same |
| **13** | **left_elbow** | elbow angle |
| **14** | **right_elbow** | same |
| **15** | **left_wrist** | wrist-over-elbow alignment, bar path |
| **16** | **right_wrist** | same |
| 17 | left_pinky | hand detail |
| 18 | right_pinky | — |
| 19 | left_index | — |
| 20 | right_index | — |
| 21 | left_thumb | — |
| 22 | right_thumb | — |
| **23** | **left_hip** | hip angle, pelvis tracking |
| **24** | **right_hip** | same |
| **25** | **left_knee** | knee angle |
| **26** | **right_knee** | same |
| **27** | **left_ankle** | dorsiflexion proxy |
| **28** | **right_ankle** | same |
| 29 | left_heel | heel rise detection |
| 30 | right_heel | same |
| 31 | left_foot_index | toe position |
| 32 | right_foot_index | same |

**Bold** = landmarks used for angle computation in the analyzer.

Each landmark has:
- `x` — horizontal (0 = left edge, 1 = right edge of frame)
- `y` — vertical (0 = top, 1 = bottom of frame)  
- `z` — estimated depth (relative to hip midpoint; negative = in front of plane)
- `visibility` — confidence score 0.0–1.0 (< 0.5 = landmark likely occluded)

---

## Angle computation

### Three-point angle formula

```javascript
function angleDeg(a, b, c) {
  // Returns angle at vertex b, formed by rays b→a and b→c
  const ba = { x: a.x - b.x, y: a.y - b.y };
  const bc = { x: c.x - b.x, y: c.y - b.y };
  const dot = ba.x * bc.x + ba.y * bc.y;
  const mag = Math.sqrt(ba.x**2 + ba.y**2) * Math.sqrt(bc.x**2 + bc.y**2);
  if (mag === 0) return 0;
  return Math.acos(Math.max(-1, Math.min(1, dot / mag))) * (180 / Math.PI);
}
```

### Computed angles per frame

| Angle name | Landmark triplet (A-B-C, angle at B) |
|---|---|
| `leftKnee` | 23 (L_HIP) → 25 (L_KNEE) → 27 (L_ANKLE) |
| `rightKnee` | 24 (R_HIP) → 26 (R_KNEE) → 28 (R_ANKLE) |
| `leftHip` | 11 (L_SHOULDER) → 23 (L_HIP) → 25 (L_KNEE) |
| `rightHip` | 12 (R_SHOULDER) → 24 (R_HIP) → 26 (R_KNEE) |
| `leftElbow` | 11 (L_SHOULDER) → 13 (L_ELBOW) → 15 (L_WRIST) |
| `rightElbow` | 12 (R_SHOULDER) → 14 (R_ELBOW) → 16 (R_WRIST) |
| `leftShoulder` | 13 (L_ELBOW) → 11 (L_SHOULDER) → 23 (L_HIP) |
| `rightShoulder` | 14 (R_ELBOW) → 12 (R_SHOULDER) → 24 (R_HIP) |

### Spine lean (trunk forward lean)

```javascript
function spineLean(landmarks) {
  const midShoulder = midpoint(landmarks[11], landmarks[12]);
  const midHip = midpoint(landmarks[23], landmarks[24]);
  // Angle from vertical (pure upright = 0°; horizontal = 90°)
  const dy = midHip.y - midShoulder.y;
  const dx = midHip.x - midShoulder.x;
  return Math.abs(Math.atan2(Math.abs(dx), Math.abs(dy)) * (180 / Math.PI));
}
```

Note: Because y increases downward in image coordinates, `midHip.y > midShoulder.y` normally. A positive `dx` means the torso is leaning forward (toward the camera side for a side-view). Lean angle increases as the athlete bends more forward.

---

## Key frame selection

The analyzer selects 6–8 frames to export:

| Label | Selection logic |
|---|---|
| `bottom` | Frame with the minimum average knee angle (L+R)/2 |
| `top` / `lockout` | Frame with the maximum average knee angle |
| `mid_ascending` | Frame at ~50% of the ascending phase between bottom and top |
| `worst_spine` | Frame with the maximum spine lean value |
| `start` | First frame with visibility > 0.7 on key landmarks |
| `end` | Last frame with visibility > 0.7 on key landmarks |
| `asymmetry_peak` | Frame with the largest L/R knee or hip delta |

---

## Export JSON schema

```json
{
  "exercise": "string — user-selected or typed",
  "cameraAngle": "side | front | diagonal | unknown",
  "videoInfo": {
    "filename": "string",
    "duration_s": "number",
    "framesAnalyzed": "integer",
    "sampledFps": 5
  },
  "summary": {
    "minKneeAngle": { "left": 0, "right": 0 },
    "maxKneeAngle": { "left": 0, "right": 0 },
    "minHipAngle": { "left": 0, "right": 0 },
    "maxHipAngle": { "left": 0, "right": 0 },
    "avgSpineLean_deg": 0,
    "maxSpineLean_deg": 0,
    "asymmetry": {
      "knee_deg": 0,
      "hip_deg": 0,
      "shoulder_deg": 0
    }
  },
  "keyFrames": [
    {
      "label": "bottom",
      "timestamp_s": 0,
      "screenshotIndex": 1,
      "angles": {
        "leftKnee": 0, "rightKnee": 0,
        "leftHip": 0, "rightHip": 0,
        "leftElbow": 0, "rightElbow": 0,
        "leftShoulder": 0, "rightShoulder": 0,
        "spineLean": 0
      },
      "landmarks": [
        { "x": 0.0, "y": 0.0, "z": 0.0, "visibility": 0.0 }
      ]
    }
  ]
}
```

The `landmarks` array in each key frame contains all 33 points. `screenshotIndex` corresponds to the numbered screenshots the user captures from the tool's canvas (Screenshot 1, 2, 3…).

---

## Limitations and known issues

**Occlusion**: When a body part is hidden (e.g., far-side knee in a side-view squat), visibility drops below 0.5. The tool flags low-visibility landmarks in the UI and excludes them from angle computation. Claude should note when angles are from a low-visibility landmark.

**2D projection**: All angles are computed in the image plane. Depth (z) is estimated, not measured. A squat filmed from a slight angle will show apparent asymmetry even if the athlete is symmetric. Always cross-reference with the camera angle field.

**Single-person**: The tool uses `numPoses: 1`. If two people are in frame, only the closest/most prominent person is analyzed.

**Frame rate**: The tool samples at 5 fps. Fast explosive movements (Olympic lifts, jumps) may miss peak positions between samples. For plyometric analysis, use slow-motion video (120+ fps original) — the tool will still sample at 5 fps but the source video will have captured the peak.

**Model accuracy**: `pose_landmarker_lite` trades some accuracy for speed. For wrist and foot landmarks especially, visibility and position can drift under occlusion or extreme angles. Use `pose_landmarker_full` if the lite model shows unreliable results — swap the model URL in the HTML tool.

**Full model URL**: `https://storage.googleapis.com/mediapipe-models/pose_landmarker/pose_landmarker_full/float16/1/pose_landmarker_full.task`
