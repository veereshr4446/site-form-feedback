
# Site Audit Feedback Form

A single-file, browser-based feedback form for collecting structured input from field teams about a site audit submission process. Responses can be exported as a formatted PDF — no backend, no login, no setup required.

**Live demo:** https://veereshr4446.github.io/site-form-feedback/
**Repository:** https://github.com/veereshr4446/site-form-feedback

---

## Overview

This project provides a lightweight, self-contained web form designed to gather qualitative and quantitative feedback about an internal audit workflow. It captures baseline comparison data (old process vs. new process), operational pain points, error frequency, and free-form commentary.

The form requires no server, no database, and no third-party form service. It runs entirely in the browser and exports responses on demand as a PDF document.

### Use cases

- Internal process reviews
- Post-rollout feedback collection
- Field-team surveys
- On-site data capture from mobile devices

---

## Features

- Single-file implementation — `index.html` contains the full application
- Responsive layout optimized for both desktop and mobile browsers
- Seventeen structured input fields (text, number, select, textarea)
- Multi-person response support for comparison questions
- Client-side PDF generation using jsPDF
- Auto-paginated PDF output with page footers
- In-form progress indicator
- Answer preview before export
- Toast notifications for user feedback
- No build step, no local dependencies

---

## Technology

| Layer | Choice |
|---|---|
| Markup | HTML5 |
| Styling | Vanilla CSS (custom properties, grid, flexbox) |
| Behavior | Vanilla JavaScript (ES5-compatible syntax) |
| PDF engine | jsPDF 2.5.1 (loaded from CDN) |
| Fonts | System font stack |

No frameworks, no bundlers, no package manager required.

---

## Project structure

```
site-form-feedback/
├── index.html      Application source (HTML + CSS + JS)
├── README.md       This document
└── LICENSE         MIT license
```

---

## Getting started

### Option 1 — Open directly

```bash
git clone https://github.com/veereshr4446/site-form-feedback.git
cd site-form-feedback
```

Open `index.html` in any modern browser.

### Option 2 — Serve locally

For mobile testing on the same network:

```bash
npx serve .
```

or

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080` on your computer, or `http://<your-lan-ip>:8080` on your phone.

### Option 3 — Hosted version

The form is deployed via GitHub Pages:

https://veereshr4446.github.io/site-form-feedback/

---

## Form fields

| # | Question | Input type |
|---|---|---|
| 1 | Team members using the form | number |
| 2 | Audit entries submitted this week | text |
| 3a | Error/stuck frequency | select |
| 3b | Error details | text |
| 4 | Previous recording method (two respondents) | text × 2 |
| 5 | Previous time per site (two respondents) | text × 2 |
| 6 | Current time per site | text |
| 7 | Details lost with old method (two respondents) | text × 2 |
| 8 | Mobile usability comparison | text |
| 9 | Issues or suggestions | textarea |
| 10a | Time impact verdict | select |
| 10b | Time impact comment | text |
| 11 | One-sentence summary | textarea |
| + | Additional thoughts | textarea |

---

## How the PDF export works

The export runs entirely in the browser:

1. On click, values are read from `form.elements` and normalized.
2. A new A4 document is created with jsPDF.
3. A header block renders the title and a generation timestamp.
4. Each field is rendered with a labeled section; long values wrap automatically using `splitTextToSize`.
5. When the vertical cursor approaches the page margin, `doc.addPage()` is called and the cursor resets.
6. A footer with page numbers is applied to every page after all content is written.
7. The file is saved as `site-audit-feedback-YYYY-MM-DD.pdf`.

No network requests occur during export. The PDF is generated locally and saved directly to the user's device.

---

## Customization

### Adding or removing a field

1. Add the input inside the `.form-card__body` section:

```html
<div class="field-group">
  <div class="field-group__head">
    <span class="field-num">12</span>
    <label class="field-label" for="newField">Your question</label>
  </div>
  <div class="input-wrap">
    <input type="text" id="newField" name="newField" placeholder="…" />
  </div>
</div>
```

2. Register the field in the `FIELDS` array in the script:

```js
const FIELDS = [
  // …
  { key: 'newField', label: '12. Your question' }
];
```

The field will automatically appear in the preview and the PDF export.

### Multiline values

Set `multiline: true` in the field definition for textareas:

```js
{ key: 'annoyances', label: '9. Issues / suggestions', multiline: true }
```

### Theming

The palette is defined in the `:root` block:

```css
:root {
  --accent: #2563eb;
  --text:   #0f172a;
  --bg:     #f6f8fb;
  --border: #e5e9f0;
  /* … */
}
```

Changing these values updates the entire UI consistently.

---

## Browser support

| Browser | Status |
|---|---|
| Chrome / Edge (current) | Supported |
| Firefox (current) | Supported |
| Safari (iOS 14+) | Supported |
| Samsung Internet | Supported |
| Internet Explorer 11 | Not supported |

The form requires JavaScript enabled and internet access on first load for the jsPDF dependency.

---

## Accessibility

- All inputs have associated `<label>` elements.
- Focus states are visible (blue ring).
- Color contrast meets WCAG AA for body text.
- Buttons are keyboard-navigable.
- The toast uses `role="status"` and `aria-live="polite"`.

---

## Roadmap

- [ ] Optional draft autosave via `localStorage`
- [ ] Light/dark theme toggle
- [ ] CSV and JSON export alongside PDF
- [ ] Inline validation messages
- [ ] Bundled offline jsPDF

Pull requests are welcome.

---

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes: `git commit -m "Add your feature"`.
4. Push to the branch: `git push origin feature/your-feature`.
5. Open a pull request.

Keep the project single-file. Do not introduce a build step.

---

## Author

**Viresh Ranjanagi**
- GitHub: https://github.com/veereshr4446
- Live demo: https://veereshr4446.github.io/site-form-feedback/

---

## License

Released under the [MIT License](LICENSE).

---

## Acknowledgements

- [jsPDF](https://github.com/parallax/jsPDF) — client-side PDF generation
- Icons rendered inline as SVG
```

---

## 📋 Final steps

1. **Open your repo:** https://github.com/veereshr4446/site-form-feedback
2. **Click `README.md`** → ✏️ pencil icon
3. **Ctrl + A** → **Delete** (clear the empty file)
4. **Paste the block above** (everything between the ``` fences — do **not** copy the fences themselves)
5. **Commit** with message: `Add professional README`
6. **Add a LICENSE file** (optional but recommended):
   - Repo → **Add file** → **Create new file**
   - Name it: `LICENSE`
   - Click **"Choose a license template"** → pick **MIT** → fill in "Viresh Ranjanagi" → **Review and submit**

That's it — your repo now looks complete and professional. 🎯

---

## 🎁 Bonus — Repo description & topics

While you're on the repo page, click the ⚙️ gear icon next to **"About"** on the right side, and fill in:

**Description:**
```
Browser-based feedback form for collecting structured site audit input and exporting responses as PDF. Single-file, no backend.
```

**Topics (tags):**
```
html, css, javascript, jspdf, feedback-form, audit-form, pdf-export, single-file, no-backend, github-pages
```

**Website:** `https://veereshr4446.github.io/site-form-feedback/`
