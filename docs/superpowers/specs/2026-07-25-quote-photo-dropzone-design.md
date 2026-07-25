# Quote-section photo dropzone — design

## Context

`index.html` is a single-file static demo (no backend). The founder wants a way for users to submit phone photos alongside the existing condition questionnaire, to support (eventually) human review of device condition. Per discussion:

- No AI/vision analysis — photos are for manual/human review only, and this is explicitly a demo, not a working submission pipeline (no backend exists or is being added in this iteration).
- The estimate must stay a **price range** (already true in the current quote logic's intent, not literally rendered as a range yet — out of scope here, not part of this change).
- Photos should live where the user already enters condition info, not as a separate later step that duplicates the ask.

## Current state

- `#quote` section (home page) — `.qform` contains: brand `<select>`, age `<select>`, "does it turn on?" chips, "screen condition" chips, optional comments `<textarea>`. Submitting isn't a submit action — every change recomputes `quote()` live, showing an amount in `.quote-result`.
- `#page-sell` (reached via "Sell my phone →") is a 3-step stepper: **Photos** (dropzone, requires ≥2 photos to continue) → **Your details** (contact form) → **Shipping label**. The photo dropzone markup/CSS (`.dropzone`, `.thumbs`, `.thumb`, `.photo-tips`) and JS (`addPhotos`, `updatePhotoUI`, `photoCount`) already exist and are reused, not rebuilt.

## Design

**1. Move, don't duplicate.** The photo dropzone relocates from sell-flow step 1 into the `#quote` section's `.qform`, placed above the "Phone brand" label. Resulting field order: **photos → brand → age → power → screen → comments**.

**2. Photos stay non-functional to pricing.** `quote()`'s math is untouched — photos are collected for future human review, not read by any calculation. This matches the earlier no-AI decision and the rest of the site's demo-level honesty (nothing here claims to analyze the images).

**3. The ≥2-photo gate moves with the dropzone.** Previously "Continue" in sell-flow step 1 was disabled until 2 photos were added. That gate now applies to the **"Sell my phone →"** button in `.quote-result`: disabled (with the same "add at least 2 photos" style messaging) until `photoCount >= 2`.

**4. Sell flow collapses from 3 steps to 2.** Step 1 (Photos) is removed entirely. The stepper shows **Your details → Shipping label**. `goSell()` now lands directly on the details form instead of the photo step. Step numbering, the progress dots, and `setStep()`'s loop bound (currently `1..3`) update accordingly.

**5. Unchanged:** the quote pricing formula, the shipping-label generator, the "Demo mode" alerts, all other pages/sections.

## Out of scope (explicitly, per discussion)

- No backend, no real photo delivery/storage — this stays a front-end-only preview, same trust level as the rest of the demo.
- No AI/vision-based price adjustment.
- No change to how the price amount itself is displayed (still a single number, not a range) — raised in conversation as a possible future change but not part of this task.

## Implementation notes

- Reuse existing CSS classes (`.dropzone`, `.dzico`, `.thumbs`, `.thumb`, `.photo-tips`) and JS (`addPhotos`, `updatePhotoUI`) as-is; only their DOM location and the element(s) they toggle change.
- `updatePhotoUI()` currently toggles `#next-1` (sell-flow step 1's continue button); it needs to instead toggle the "Sell my phone →" button in the quote section.
- Sell-flow panel IDs (`panel-1`/`panel-2`/`panel-3`) and stepper IDs (`st1`/`st2`/`st3`) renumber down to two panels/steps; `goSell()` and `setStep()` update to match.
- The dropzone was originally sized for the ~760px-wide sell-flow panel. Inside `.qform` (one column of the `.quote-grid`, narrower on desktop, full-width once the grid stacks under 780px) it may need minor padding/sizing tweaks so it doesn't feel cramped — a CSS-only adjustment, not a structural one.
- Single file change: `index.html` only.
