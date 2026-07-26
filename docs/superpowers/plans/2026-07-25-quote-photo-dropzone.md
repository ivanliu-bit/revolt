# Quote-Section Photo Dropzone Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Move the existing photo-upload dropzone out of the sell flow's step 1 and into the home-page quote form, gate the "Sell my phone →" button on having ≥2 photos, and collapse the sell flow from 3 steps to 2.

**Architecture:** Single-file static site (`index.html`, vanilla HTML/CSS/JS, no build step, no test framework). All existing dropzone CSS (`.dropzone`, `.thumbs`, `.thumb`, `.photo-tips`) and JS (`addPhotos`, `updatePhotoUI`, `photoCount`) are reused as-is — only their DOM location and which button they gate change. This is one coherent, atomically-applied change: moving the dropzone's IDs (`#photo-input`, `#thumbs`, `#photo-tips`, `#tip-1..3`) without simultaneously deleting the old copy would create duplicate-ID conflicts that break the page, so the move and the sell-flow renumbering happen together, not as separable increments.

**Tech Stack:** Plain HTML/CSS/JS. Verified by opening `index.html` directly in a browser (per the repo's own README: "no install, no build step").

## Global Constraints

- Single file touched: `index.html` only (per spec `docs/superpowers/specs/2026-07-25-quote-photo-dropzone-design.md`).
- No backend, no AI/vision analysis — photos remain purely a front-end preview and never feed into the `quote()` price calculation.
- No test framework exists in this repo — verification is manual, via browser interaction, not automated test runs.
- Reuse existing dropzone markup/CSS/JS verbatim; do not rewrite working code.

---

### Task 1: Merge photo dropzone into quote form, gate the Sell button, collapse sell flow to 2 steps

**Files:**
- Modify: `index.html` (CSS in `<style>`, markup in `#page-home` and `#page-sell`, script in `<script>`)

**Interfaces:**
- Consumes: existing `addPhotos(files)`, `photoCount` (global, starts at `0`), `go(page)`, `goQuote()` — all already defined elsewhere in the file and untouched by this task.
- Produces: `#sell-btn` (id on the quote section's "Sell my phone" button, replaces the removed `#next-1`), renumbered `#panel-1`/`#panel-2` (was `#panel-2`/`#panel-3`) and `#st1`/`#st2` (was `#st2`/`#st3`) for the sell flow's `setStep(n)` to target.

- [ ] **Step 1: Add CSS for the relocated dropzone and the disabled Sell button**

  Find this block (around line 340):
  ```css
  .quote-result button:hover { background: var(--green-dark); transform: translateY(-3px); box-shadow: 0 12px 30px rgba(22,163,74,.42); }
  ```
  Add immediately after it:
  ```css
  .quote-result button:disabled { background: #b9cfc1; box-shadow: none; cursor: not-allowed; transform: none; }
  ```

  Find this block (around line 474, inside the `/* ===== SELL FLOW ===== */` section):
  ```css
  .dropzone:hover { border-color: var(--green); background: var(--green-soft); transform: translateY(-2px); }
  .dropzone .dzico { font-size: 2.4rem; margin-bottom: 8px; }
  ```
  Add immediately after it:
  ```css
  .qform .dropzone { padding: 28px 20px; margin-bottom: 6px; }
  .qform .dzico { font-size: 2rem; margin-bottom: 6px; }
  ```

- [ ] **Step 2: Move the dropzone markup into the quote form**

  In `#page-home`, find (around line 634-637):
  ```html
      <div class="quote-grid">
        <div class="qform">
          <label>Phone brand</label>
          <select id="brand" onchange="quote()">
  ```
  Replace with:
  ```html
      <div class="quote-grid">
        <div class="qform">
          <label>Photos</label>
          <div class="dropzone" onclick="document.getElementById('photo-input').click()">
            <div class="dzico">📸</div>
            <h3>Add photos of your phone</h3>
            <p>Click to browse (or drag &amp; drop) — front, back, and any damage. This confirms your quote so there are no surprises.</p>
          </div>
          <input type="file" id="photo-input" accept="image/*" multiple style="display:none" onchange="addPhotos(this.files)">
          <div class="photo-tips" id="photo-tips">
            <span id="tip-1">1️⃣ Front of phone</span>
            <span id="tip-2">2️⃣ Back of phone</span>
            <span id="tip-3">3️⃣ Close-up of any damage</span>
          </div>
          <div class="thumbs" id="thumbs"></div>

          <label>Phone brand</label>
          <select id="brand" onchange="quote()">
  ```

- [ ] **Step 3: Gate the "Sell my phone" button on photo count**

  Find (around line 672):
  ```html
          <button onclick="goSell()">Sell my phone →</button>
  ```
  Replace with:
  ```html
          <button id="sell-btn" disabled onclick="goSell()">Sell my phone → (add at least 2 photos)</button>
  ```

- [ ] **Step 4: Remove the old photos step and renumber the sell-flow stepper**

  In `#page-sell`, find (around line 1026-1097):
  ```html
  <div class="stepper">
    <div class="st active" id="st1"><div class="dot">1</div><div class="lbl">Photos</div><div class="bar2"></div></div>
    <div class="st" id="st2"><div class="dot">2</div><div class="lbl">Your details</div><div class="bar2"></div></div>
    <div class="st" id="st3"><div class="dot">3</div><div class="lbl">Shipping label</div></div>
  </div>

  <section style="padding-top: 36px;">

    <div class="qsummary">
      <span>Your quote</span>
      <span class="amt" id="sell-amount">$35</span>
      <span style="font-weight:600; font-size:.88rem; opacity:.85;" id="sell-path">full harvest</span>
    </div>

    <!-- STEP 1: PHOTOS -->
    <div class="sell-panel active" id="panel-1">
      <div class="dropzone" onclick="document.getElementById('photo-input').click()">
        <div class="dzico">📸</div>
        <h3>Add photos of your phone</h3>
        <p>Click to browse (or drag &amp; drop) — front, back, and any damage. This confirms your quote so there are no surprises.</p>
      </div>
      <input type="file" id="photo-input" accept="image/*" multiple style="display:none" onchange="addPhotos(this.files)">
      <div class="photo-tips" id="photo-tips">
        <span id="tip-1">1️⃣ Front of phone</span>
        <span id="tip-2">2️⃣ Back of phone</span>
        <span id="tip-3">3️⃣ Close-up of any damage</span>
      </div>
      <div class="thumbs" id="thumbs"></div>
      <div class="flow-btns">
        <button class="fbtn next" id="next-1" disabled onclick="setStep(2)">Continue → (add at least 2 photos)</button>
      </div>
    </div>

    <!-- STEP 2: DETAILS -->
    <div class="sell-panel" id="panel-2">
      <div class="sform">
        <div class="row">
          <div><label>Full name</label><input id="f-name" placeholder="Alex Green" oninput="checkForm()"></div>
          <div><label>Email</label><input id="f-email" type="email" placeholder="alex@email.com" oninput="checkForm()"></div>
        </div>
        <label>Street address</label><input id="f-addr" placeholder="123 Whyte Ave NW" oninput="checkForm()">
        <div class="row">
          <div><label>City</label><input id="f-city" placeholder="Edmonton" oninput="checkForm()"></div>
          <div><label>Postal code</label><input id="f-postal" placeholder="T6G 2R3" oninput="checkForm()"></div>
        </div>
        <label>How should we pay you?</label>
        <div class="chips payx" id="payx">
          <button class="chip active" onclick="pickPay(this)">💸 E-transfer</button>
          <button class="chip" onclick="pickPay(this)">🎁 Store credit (+10%)</button>
        </div>
      </div>
      <div class="flow-btns">
        <button class="fbtn back2" onclick="setStep(1)">← Back</button>
        <button class="fbtn next" id="next-2" disabled onclick="makeLabel()">Generate my shipping label →</button>
      </div>
    </div>

    <!-- STEP 3: LABEL -->
    <div class="sell-panel" id="panel-3">
  ```
  Replace with:
  ```html
  <div class="stepper">
    <div class="st active" id="st1"><div class="dot">1</div><div class="lbl">Your details</div><div class="bar2"></div></div>
    <div class="st" id="st2"><div class="dot">2</div><div class="lbl">Shipping label</div></div>
  </div>

  <section style="padding-top: 36px;">

    <div class="qsummary">
      <span>Your quote</span>
      <span class="amt" id="sell-amount">$35</span>
      <span style="font-weight:600; font-size:.88rem; opacity:.85;" id="sell-path">full harvest</span>
    </div>

    <!-- STEP 1: DETAILS -->
    <div class="sell-panel active" id="panel-1">
      <div class="sform">
        <div class="row">
          <div><label>Full name</label><input id="f-name" placeholder="Alex Green" oninput="checkForm()"></div>
          <div><label>Email</label><input id="f-email" type="email" placeholder="alex@email.com" oninput="checkForm()"></div>
        </div>
        <label>Street address</label><input id="f-addr" placeholder="123 Whyte Ave NW" oninput="checkForm()">
        <div class="row">
          <div><label>City</label><input id="f-city" placeholder="Edmonton" oninput="checkForm()"></div>
          <div><label>Postal code</label><input id="f-postal" placeholder="T6G 2R3" oninput="checkForm()"></div>
        </div>
        <label>How should we pay you?</label>
        <div class="chips payx" id="payx">
          <button class="chip active" onclick="pickPay(this)">💸 E-transfer</button>
          <button class="chip" onclick="pickPay(this)">🎁 Store credit (+10%)</button>
        </div>
      </div>
      <div class="flow-btns">
        <button class="fbtn back2" onclick="goQuote()">← Back to quote</button>
        <button class="fbtn next" id="next-2" disabled onclick="makeLabel()">Generate my shipping label →</button>
      </div>
    </div>

    <!-- STEP 2: LABEL -->
    <div class="sell-panel" id="panel-2">
  ```

  Note: this replaces the panel wrapper's opening tag only (`id="panel-3"` → `id="panel-2"`); the label-step markup that follows (`.label-card` etc.) is unchanged and stays exactly where it is.

- [ ] **Step 5: Retarget `updatePhotoUI()` to the Sell button**

  Find (in `<script>`):
  ```js
    function updatePhotoUI() {
      for (let i = 1; i <= 3; i++)
        document.getElementById('tip-' + i).classList.toggle('got', photoCount >= i);
      const btn = document.getElementById('next-1');
      btn.disabled = photoCount < 2;
      btn.textContent = photoCount < 2 ? 'Continue → (add at least 2 photos)' : 'Continue →';
    }
  ```
  Replace with:
  ```js
    function updatePhotoUI() {
      for (let i = 1; i <= 3; i++)
        document.getElementById('tip-' + i).classList.toggle('got', photoCount >= i);
      const btn = document.getElementById('sell-btn');
      btn.disabled = photoCount < 2;
      btn.textContent = photoCount < 2 ? 'Sell my phone → (add at least 2 photos)' : 'Sell my phone →';
    }
  ```

- [ ] **Step 6: Shrink `setStep()`'s loop to 2 panels**

  Find:
  ```js
    function setStep(n) {
      for (let i = 1; i <= 3; i++) {
        document.getElementById('panel-' + i).classList.toggle('active', i === n);
        const st = document.getElementById('st' + i);
        st.classList.toggle('active', i === n);
        st.classList.toggle('done', i < n);
      }
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  ```
  Replace with:
  ```js
    function setStep(n) {
      for (let i = 1; i <= 2; i++) {
        document.getElementById('panel-' + i).classList.toggle('active', i === n);
        const st = document.getElementById('st' + i);
        st.classList.toggle('active', i === n);
        st.classList.toggle('done', i < n);
      }
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  ```

- [ ] **Step 7: Point `makeLabel()` at the new step 2**

  Find:
  ```js
    function makeLabel() {
      const name = document.getElementById('f-name').value.trim();
      const addr = document.getElementById('f-addr').value.trim();
      const city = document.getElementById('f-city').value.trim();
      const postal = document.getElementById('f-postal').value.trim().toUpperCase();
      document.getElementById('lbl-from').innerHTML =
        name + '<br>' + addr + '<br>' + city + ', AB ' + postal;
      document.getElementById('lbl-track').textContent =
        'REV-2026-' + String(Math.floor(100000 + Math.random() * 900000));
      setStep(3);
    }
  ```
  Replace with:
  ```js
    function makeLabel() {
      const name = document.getElementById('f-name').value.trim();
      const addr = document.getElementById('f-addr').value.trim();
      const city = document.getElementById('f-city').value.trim();
      const postal = document.getElementById('f-postal').value.trim().toUpperCase();
      document.getElementById('lbl-from').innerHTML =
        name + '<br>' + addr + '<br>' + city + ', AB ' + postal;
      document.getElementById('lbl-track').textContent =
        'REV-2026-' + String(Math.floor(100000 + Math.random() * 900000));
      setStep(2);
    }
  ```

- [ ] **Step 8: Manual verification — quote section**

  Open `index.html` directly in a browser (double-click, or `start index.html` from the repo root). Verify:
  - The quote form's first field is now "Photos" with a dropzone, above "Phone brand".
  - "Sell my phone →" is disabled and reads "Sell my phone → (add at least 2 photos)".
  - Click the dropzone, select 1 image file → button stays disabled, tip 1 gets a green "got" highlight.
  - Select a 2nd image file (click dropzone again, or select 2 files at once) → button becomes enabled and text changes to "Sell my phone →". Thumbnails for both photos appear with working ✕ remove buttons.
  - Remove a photo down to 1 → button becomes disabled again.
  - Add photos back to ≥2, change brand/age/power/screen chips → the quoted `$amount` still updates live exactly as before (confirms photos don't affect pricing).

- [ ] **Step 9: Manual verification — sell flow**

  With ≥2 photos added, click "Sell my phone →". Verify:
  - Stepper now shows only 2 dots: "Your details" (active) and "Shipping label".
  - You land directly on the details form (no photos step).
  - "← Back to quote" returns to the home page's quote section (scrolled to it).
  - Fill all 5 fields (name/email/address/city/postal) → "Generate my shipping label →" becomes enabled.
  - Click it → stepper advances to "Shipping label" (step 2 of 2), label card shows the entered name/address and the quoted amount.
  - Click "Done — back home" → returns to the home page.

- [ ] **Step 10: Commit**

  ```bash
  git add index.html
  git commit -m "$(cat <<'EOF'
  Move photo dropzone into quote form, collapse sell flow to 2 steps

  Photos are now collected alongside the condition questionnaire instead
  of as a separate first step after "Sell my phone" — the Sell button is
  gated on 2+ photos instead of the old step's Continue button, and the
  sell-flow stepper drops from 3 steps to 2.
  EOF
  )"
  ```
