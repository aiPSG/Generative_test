# Metaball Type

Generate **letters and numbers from 2D metaball blobs** — right in the browser.

Type any text and the app draws each glyph from a **hand-made 5×7 grid font**
(no system fonts), turns every filled cell into a metaball, and lets the blobs
merge into smooth, gooey, connected letters. Tune the blobs, the iso-threshold,
colors, and motion, then export a PNG.

## Why a grid font?

The chunky 5×7 grid style metaballizes *perfectly* because:

- Every glyph has a **uniform 1-cell stroke width**, so one blob per filled
  cell gives evenly-spaced metaballs that fuse into smooth necks.
- Neighbouring cells (orthogonal **and** diagonal) sit close enough to connect,
  so strokes stay continuous.
- **Counters** (the holes in O, A, B, 8, …) are 2+ cells from any blob, so they
  stay open instead of filling in — the letters remain legible even when very
  gooey.

## Live demo

Once GitHub Pages is enabled for this repo, the app is served at:

```
https://<owner>.github.io/<repo>/
```

## Features

- **Text input** — A–Z, 0–9 and `. , ! ? - : '`, multiple lines.
- **Grid attributes**
  - *Cell size* — pixels per grid cell (overall letter scale).
  - *Letter spacing* — gap between glyphs, in cells. Glyphs use **proportional
    kerning** (narrow glyphs like `I !  . 1` only advance by the columns they use).
  - *Show underlying grid* — overlay the 5×7 lattice each glyph is built on.
- **Metaball attributes**
  - *Blob radius (× cell)* — blob size as a multiple of the cell, so letters
    keep merging at any scale; bigger = thicker necks.
  - *Cell size variation* — randomly varies each cell's blob size (0 = uniform)
    for a more organic, hand-made look.
  - *Field strength* — how strongly each blob contributes to the field.
  - *Threshold (iso-level)* — fatter/merged vs. thin/separated blobs.
  - *Edge smoothing* — anti-aliasing of the iso-surface.
- **Motion** — animate the blobs into "living goo" with adjustable wobble and speed.
- **Color** — two-color gradient fill, background (or transparent), optional outline.
- **Randomize** and **download PNG**.

## How it works

1. Each character is looked up in a built-in **5×7 bitmap font** and every
   filled cell becomes a **blob center**.
2. Each blob adds a smooth Wyvill falloff `(1 − d²/R²)²` to an unclamped
   floating-point scalar **field** — the classic 2D metaball construction.
   Because two nearby blobs' fields add in the gap between them, that gap
   crosses the threshold and a smooth **connecting neck** forms.
3. Pixels whose field value crosses the **threshold** are filled — with a
   smoothstep band for anti-aliasing — producing the gooey, connected glyphs.

Everything is a single self-contained `index.html` with no dependencies, so it
works perfectly as a static GitHub Pages site.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server
# open http://localhost:8000
```
