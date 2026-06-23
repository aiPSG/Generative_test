# Metaball Type

Generate **letters and numbers from 2D metaball blobs** — right in the browser.

Type any text and the app renders each glyph as a field of soft, gooey
metaballs that merge into the letter shapes. Tune the blobs, the iso-threshold,
colors, and motion, then export a PNG.

## Live demo

Once GitHub Pages is enabled for this repo, the app is served at:

```
https://<owner>.github.io/<repo>/
```

## Features

- **Text input** — letters, numbers, symbols, multiple lines.
- **Font** picker and **font size**.
- **Metaball attributes**
  - *Blob spacing* — distance between blob centers sampled along each glyph.
  - *Blob radius* — size of each blob's influence.
  - *Field strength* — how strongly each blob contributes to the field.
  - *Threshold (iso-level)* — fatter/merged vs. thin/separated blobs.
  - *Edge smoothing* — anti-aliasing of the iso-surface.
- **Motion** — animate the blobs into "living goo" with adjustable wobble and speed.
- **Color** — two-color gradient fill, background (or transparent), optional outline.
- **Randomize** and **download PNG**.

## How it works

1. The text is rendered to an offscreen canvas and the filled pixels are
   sampled on a grid to produce a set of **blob centers**.
2. Each center adds a soft radial falloff to a scalar **field** (additive
   blending), which is the classic 2D metaball construction.
3. Pixels whose field value crosses the **threshold** are filled — with a
   smoothstep band for anti-aliasing — producing the gooey glyphs.

Everything is a single self-contained `index.html` with no dependencies, so it
works perfectly as a static GitHub Pages site.

## Run locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server
# open http://localhost:8000
```
