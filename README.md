# GreenVolt Demo Website

Team Green · Shad Design Entrepreneurship 2026

A demo website for GreenVolt: we buy old and dead phones, disassemble them, and sell every component to whoever values it most.

## Run it

Everything is in one file. Just open `index.html` in any browser: no install, no build step, works offline (fonts fall back if there's no internet).

## Put it on GitHub

1. Create a free account at github.com (if you don't have one)
2. Click **New repository** → name it `GreenVolt-website` → Create
3. Click **uploading an existing file** → drag in `index.html` and `README.md` → Commit

### Make it a live website (GitHub Pages, free)

1. In your repo, go to **Settings → Pages**
2. Under "Branch", pick `main`, folder `/ (root)` → Save
3. Wait ~1 minute, then your site is live at `https://YOUR-USERNAME.github.io/GreenVolt-website/`

Now you have a real URL to show on Demo Day.

## How to edit

Open `index.html` in any text editor (VS Code recommended). The file has three parts:

| Where               | What's there                                                                                                                |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `<style>` (top)     | All the design. Colors are defined once in `:root` at the very top. Change `--green`, `--accent`, etc. to rebrand instantly |
| HTML (middle)       | The 5 pages, each wrapped in `<div class="page" id="page-...">`: `home`, `how`, `journey`, `about`, `sell`                  |
| `<script>` (bottom) | Quote calculator math, page switching, photo upload, shipping label generator                                               |

### Common edits

- **Team names**: search for `[Name]` (About page team section)
- **Company name**: search-and-replace `GreenVolt`
- **Payout prices**: in the script, find `function quote()`. The math is `recoverable value × power × payout share`, and each phone model's recoverable value is set in the `MODELS` table
- **Colors**: `:root` block at the top of `<style>`
- **Hero stat facts**: search for `data-target`

## Pages

- **Home**: hero, 3-step how it works, instant quote calculator with photo upload, where phones go, why us vs trade-ins
- **How it works**: full 5-step process + FAQ
- **Where phones go**: reuse waterfall, component breakdown table, environmental math
- **About us**: mission, story, values, team
- **Sell flow**: details form → demo shipping label (reached via "Sell my phone")

---

Demo prototype, not a real service yet.
