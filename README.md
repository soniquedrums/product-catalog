# Sonique Product Catalog

A browser-based digital flipbook for viewing Sonique product catalogs by year. Built with [PageFlip.js](https://github.com/Nodlik/StPageFlip) and hosted on GitHub Pages.

---

## How It Works

Each catalog year is stored as individual PNG page images under `/assets/page-images/{year}/`. The viewer loads the correct year from a URL query parameter:

```
https://soniquedrums.github.io/product-catalog/?year=2026
```

Pages can be navigated using the slider at the bottom. The full PDF can be downloaded from the same control bar.

---

## File Structure

```
assets/
  page-images/
    2024/   page_1.png … page_16.png
    2025/   page_1.png … page_24.png
    2026/   page_1.png … page_24.png
  2024_catalog.pdf
  2025_catalog.pdf
  2026_catalog.pdf
index.html
```

---

## Adding a New Year

1. Place the PDF in `/assets/` as `{year}_catalog.pdf`.
2. Export the PDF pages as PNGs at 200 DPI using poppler (see [Exporting Page Images](#exporting-page-images) below).
3. Update `pageCountMapping` in `index.html`:

   ```javascript
   const pageCountMapping = {
     '2026': 24,
     '2025': 24,
     '2024': 16,
   };
   ```

4. Commit and push to `main`. GitHub Actions deploys automatically.

---

## Exporting Page Images

Page images must be exported from the source PDF at **150 DPI** to balance sharpness on Retina/HiDPI displays with reasonable load times. This produces 1275×1650px PNGs. Do not use lower-resolution exports — they will appear blurry in the flipbook viewer.

**Install poppler** (one-time):

```bash
brew install poppler
```

**Export a catalog year:**

```bash
pdftoppm -png -r 150 assets/{year}_catalog.pdf assets/page-images/{year}/page
```

This creates files named `page-01.png`, `page-02.png`, etc. Rename them to the `page_N.png` convention the viewer expects:

```bash
for f in assets/page-images/{year}/page-*.png; do
  num=$(basename "$f" | grep -o '[0-9]*' | sed 's/^0*//')
  mv "$f" "assets/page-images/{year}/page_${num}.png"
done
```

Replace `{year}` with the actual year in both commands.

---

## Dependencies

- [PageFlip.js](https://github.com/Nodlik/StPageFlip) — loaded via CDN, no build step required.
- [poppler](https://poppler.freedesktop.org/) — used locally to export PDFs to PNG; install via `brew install poppler`.

---

## License

MIT — see [LICENSE](LICENSE).
