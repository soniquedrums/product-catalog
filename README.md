# Sonique Product Catalog

A browser-based digital flipbook for viewing Sonique product catalogs by year. Built with [Turn.js](https://github.com/blasten/turn.js) and hosted on GitHub Pages.

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
    2024/   page_1.webp … page_16.webp
    2025/   page_1.webp … page_24.webp
    2026/   page_1.webp … page_24.webp
  2024_catalog.pdf
  2025_catalog.pdf
  2026_catalog.pdf
index.html
```

---

## Adding a New Year

1. Place the PDF in `/assets/` as `{year}_catalog.pdf`.
2. Export the PDF pages as WebP images at 150 DPI using poppler + cwebp (see [Exporting Page Images](#exporting-page-images) below).
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

Page images are stored as WebP at **150 DPI** (1275×1650px). WebP provides 70-75% smaller files than PNG at the same quality, which significantly reduces load time. Use the **print-quality** PDF as the source when extracting — the web-quality PDF uses lossy compression that will degrade image quality if re-extracted.

**Install dependencies** (one-time):

```bash
brew install poppler webp
```

**Export and convert a catalog year:**

```bash
# Extract pages as PNG (150 DPI = 1275×1650px)
pdftoppm -png -r 150 assets/{year}_catalog.pdf /tmp/{year}_pages/page

# Convert each PNG to WebP at high quality
for f in /tmp/{year}_pages/page-*.png; do
  num=$(basename "$f" .png | grep -oE '[0-9]+' | sed 's/^0*//')
  cwebp -q 90 -sharp_yuv "$f" -o "assets/page-images/{year}/page_${num}.webp"
done
```

Replace `{year}` with the actual year. The `cwebp -q 90 -sharp_yuv` flags preserve text sharpness at high quality.

---

## Dependencies

- [Turn.js](https://github.com/blasten/turn.js) + jQuery 2.x — CSS 3D flip renderer; loaded via CDN, no build step required. Uses CSS `rotateY` on `<img>` elements so the browser renders pages at native Retina resolution (unlike canvas-based flipbook libraries).
- [poppler](https://poppler.freedesktop.org/) — used locally to export PDFs to intermediate PNG; install via `brew install poppler`.
- [libwebp](https://developers.google.com/speed/webp) — `cwebp` converts the extracted PNGs to WebP; install via `brew install webp`.

---

## License

MIT — see [LICENSE](LICENSE).
