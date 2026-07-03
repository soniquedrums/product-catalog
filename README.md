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

1. Export each catalog page as a PNG and place it in `/assets/page-images/{year}/`, named `page_1.png`, `page_2.png`, etc.
2. Place the full PDF in `/assets/` as `{year}_catalog.pdf`.
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

## Dependencies

- [PageFlip.js](https://github.com/Nodlik/StPageFlip) — loaded via CDN, no build step required.

---

## License

MIT — see [LICENSE](LICENSE).
