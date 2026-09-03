# Handover Note — Pet Brand Survey

## What this is
Cat product purchase-habit survey (凍乾 frozen-dried treats, 貓砂 litter) across 3 mainland brands: 生生不息, 城市理享, PETBAKERY. Deployed as a static GitHub Pages site with a Google Apps Script backend.

## Files
- `Pet Brand Survey.dc.html` — **source of truth**. Edit this, never `index.html` directly.
- `index.html` — standalone bundled export (~9.4MB, all images embedded as data URIs) for GitHub Pages upload. Regenerate via `super_inline_html` after any source edit.
- `google-apps-script.gs` — backend deployed at a fixed `/exec` endpoint; writes to "可讀資料 Readable" tab.
- `support.js` — DC runtime helper, do not edit.

## Current state
- All 3 brands' product images (litter + treats) are inlined as base64 data URIs in the source (they're set via JS-built CSS `background-url`, so the bundler can't auto-detect plain `<img>` tags — must manually convert to data URIs, see pattern used for `images/pet-ever/*`, `images/urbenjoy/*`, `images/pets-bakery/*`).
- Deserve brand fully removed.
- "查看結果" (view results) button links to `?admin` query param, opens in new tab, lands directly on the password gate/results view. Single-file deploy, no subfolder.
- Terminology: all instances of 中國大陸 → 內地.

## Known gotcha
If brand images 404 after upload, first suspect is stale `index.html` still live on GitHub (upload didn't actually replace it, or Pages cache ~1min delay). Only re-investigate the bundler if a *newly added* image is missing from the export.

## To re-export after edits
1. Edit `Pet Brand Survey.dc.html`.
2. `super_inline_html` → `index.html`.
3. Give user `index.html` to re-upload (single file replaces existing repo file).
