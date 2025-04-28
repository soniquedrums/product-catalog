# 🥁 Product Catalog Flipbook

![License](https://img.shields.io/badge/License-MIT-blue.svg) ![Made with PageFlip](https://img.shields.io/badge/Made%20with-PageFlip.js-orange) ![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)

This project is a simple and responsive **digital flipbook viewer** for product catalogs, using [PageFlip.js](https://github.com/Nodlik/StPageFlip).

It dynamically loads PNG pages from a GitHub Pages repository based on the selected year (passed via the URL), and allows smooth navigation through the catalog with **page sliders** and **zoom controls**.

---

## 📚 Table of Contents

- 🎯 [Features](#-features)
- 🗂️ [File Structure](#-file-structure)
- 🚀 [How to Use](#-how-to-use)
- ⚙️ [Configuration Details](#-configuration-details)
- 🧰 [Dependencies](#-dependencies)
- 📋 [To-Do / Future Improvements](#-to-do--future-improvements)
- 🏗️ [Example Usage](#-example-usage)
- 📜 [License](#-license)

---

## ✨ Features

- 📖 Realistic page-flip animations
- 📱 Mobile and desktop responsive
- 🖼️ Dynamic image loading based on the selected year
- 🎚️ Page slider for easy navigation
- 💨 Optimized loading for better performance
- 🛠️ No build tools needed — pure HTML, CSS, and JavaScript

---

## 🗂️ File Structure

```plaintext
/assets/page-images/{year}/page_{n}.png
index.html
README.md
```

- Images for each catalog year are organized in folders named after the year.
- The main flipbook functionality is handled inside `index.html`.

---

## 🚀 How to Use

1. **Host the files** using GitHub Pages or any static hosting service.
2. **Upload catalog images** to `/assets/page-images/{year}/` folders.
   
   Example:
   ```plaintext
   /assets/page-images/2025/page_1.png
   /assets/page-images/2025/page_2.png
   ```
3. **Access the flipbook** by visiting a URL with a `year` query parameter:

   Example:
   ```
   https://your-domain.com/index.html?year=2025
   ```
4. **Navigate between pages** using the page slider.
5. **Use the zoom buttons** to zoom in and out.

---

## ⚙️ Configuration Details

- The total page count for each year is manually set in the JavaScript:

  ```javascript
  const pageCountMapping = {
    '2025': 24,
    '2024': 16,
  };
  ```

- Update the `pageCountMapping` whenever you add a new catalog.

- Images are dynamically loaded based on the year specified in the URL.

---

## 🧰 Dependencies

- [PageFlip.js](https://github.com/Nodlik/StPageFlip) (via CDN)

No additional libraries or frameworks are needed.

---

## 📋 To-Do / Future Improvements

- [ ] Add swipe gesture support for better mobile experience
- [ ] Add zoom in and out buttons
- [ ] Add a "Reset Zoom" button
- [ ] Display "Page X of Y" counter
- [ ] Preload pages for faster flipping
- [ ] Add a loading spinner while pages are loading

---

## 🏗️ Example Usage

Visit:

```
https://soniquedrums.github.io/product-catalog/index.html?year=2025
```

To view the 2025 catalog.

---

## 📜 License

This project uses [PageFlip.js](https://github.com/Nodlik/StPageFlip) under its respective open-source license.
