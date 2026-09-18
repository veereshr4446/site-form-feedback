Here's the **final README** — copy everything in the block below and paste it into your empty `README.md` on GitHub.

---

```markdown
# 📋 Site Audit Feedback Form

> A beautiful, mobile-friendly, single-file HTML form that collects team feedback about a site-audit process — and exports the answers as a **real, styled PDF** with one click.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-veereshr4446.github.io-7e5eff?style=flat-square)](https://veereshr4446.github.io/site-form-feedback/)
[![Repo](https://img.shields.io/badge/GitHub-site--form--feedback-181717?style=flat-square&logo=github)](https://github.com/veereshr4446/site-form-feedback)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![jsPDF](https://img.shields.io/badge/jsPDF-2.5.1-7e5eff?style=flat-square)
![No Build](https://img.shields.io/badge/build-none-success?style=flat-square)

---

## ✨ Overview

This is a **zero-dependency, single-file web form** designed to gather qualitative and quantitative feedback from a team that recently switched to a new audit-submission process. It captures baseline data (old vs. new workflow), pain points, error frequency, and an honest one-liner — then produces a clean, shareable PDF on demand.

Perfect for:

- 🧑‍💼 Internal process reviews
- 📊 Post-rollout feedback collection
- 🗂️ Quick field-team surveys
- 📱 On-site data capture (mobile-first design)

---

## 🔗 Live Demo

**Try it here →** [https://veereshr4446.github.io/site-form-feedback/](https://veereshr4446.github.io/site-form-feedback/)

Open it on your phone, fill it in, hit **Download PDF** — you'll get a real, properly formatted PDF.

---

## 💡 Why I built this

Our team was moving from *"WhatsApp + paper + Excel later"* to a proper
audit form. Before rolling it out wide, I wanted honest feedback —
how long the old way took, what people lost, what annoys them now.

Rather than spin up a Google Form or a server, I wrote this as a
**single HTML file** so anyone could open it on their phone at a site,
fill it in, and export a real PDF to send back. No backend, no login,
no data leaving the browser.

---

## 🚀 Features

| Feature | Description |
|---|---|
| 🎨 **Beautiful UI** | Glassmorphism container, gradient badges, soft shadows, pastel background |
| 📱 **Mobile-first** | Single-column layout, full-width buttons, big tap targets under 640px |
| 📝 **17 structured fields** | Mix of `text`, `number`, `select`, and `textarea` inputs |
| 👥 **Multi-person questions** | Q4, Q5, Q7 collect answers from *two people* side-by-side |
| 📄 **Real PDF export** | Uses [jsPDF](https://github.com/parallax/jsPDF) — not a fake `.pdf` blob |
| 🧾 **Auto-paginated PDF** | Multi-page support with page footer (`Page X of Y`) |
| 🎨 **Styled PDF output** | Gradient header banner, colored number badges, timestamp |
| ✨ **"Show answers" preview** | Instant summary before exporting |
| 🔔 **Toast notifications** | Non-intrusive success/error feedback |
| 🌐 **No build step** | Just open the HTML file — no npm, no bundler, no server |
| 📦 **Single file** | Entire app = one `.html` file |

---

## 📁 Project Structure

```
site-form-feedback/
├── index.html      ← the entire app (HTML + CSS + JS)
└── README.md
```

Yes, really. One file.

---

## 🛠️ Tech Stack

- **HTML5** — semantic structure
- **Vanilla CSS** — grid, flexbox, custom properties, media queries
- **Vanilla JavaScript** — no framework, no jQuery
- **jsPDF 2.5.1** — loaded from CDN for real PDF generation
- **System fonts** — fast, no font downloads required

---

## 📦 Getting Started

### Option 1 — Just open it
```bash
git clone https://github.com/veereshr4446/site-form-feedback.git
cd site-form-feedback
open index.html   # macOS
# or: start index.html  (Windows)
# or: xdg-open index.html  (Linux)
```

### Option 2 — Serve locally (recommended for mobile testing)
```bash
npx serve .
# or
python3 -m http.server 8080
```
Then visit `http://localhost:8080` — and on your phone, hit `http://YOUR_LAN_IP:8080`.

### Option 3 — Use the hosted version
👉 [https://veereshr4446.github.io/site-form-feedback/](https://veereshr4446.github.io/site-form-feedback/)

---

## 📄 The 17 Fields

| # | Question | Type |
|---|---|---|
| 1 | Roughly how many people on the team are using the form? | `number` |
| 2 | How many audit entries submitted this week? (`=COUNTA()`) | `text` |
| 3a | Errors / stuck while submitting — how often? | `select` |
| 3b | Error details (optional) | `text` |
| 4 | Before this form, how did you usually record a site audit? *(first + second person)* | `text × 2` |
| 5 | Old way: time per site *(first + second person)* | `text × 2` |
| 6 | How long does it take now, using the form? | `text` |
| 7 | Lost / forgot details with old method? *(first + second person)* | `text × 2` |
| 8 | Easier to fill on phone at the site? | `text` |
| 9 | Anything annoying or you'd want changed? | `textarea` |
| 10a | Would you say: saves time / no difference / slower? | `select` |
| 10b | Time-impact comment (optional) | `text` |
| 11 | One honest sentence about how it's working | `textarea` |
| + | Additional thoughts | `textarea` |

---

## 🧠 How the PDF Works

The PDF export is done entirely client-side:

1. On click, values are collected from the form via `form.elements`.
2. `jsPDF` creates an A4 document.
3. A gradient header is drawn with two overlapping `rect()` fills.
4. Each field is rendered with:
   - a **filled circle badge** (question number),
   - **bold label** (auto-wrapped with `splitTextToSize`),
   - **value** below it (auto-wrapped).
5. When `y` approaches the page bottom, `doc.addPage()` is called and `y` resets.
6. After all fields, a loop adds `Page X of Y` footers to every page.
7. `doc.save('site_audit_feedback_YYYY-MM-DD.pdf')` triggers the download.

No server, no uploads, no data leaves the browser. 🔒

---

## 🔧 Customization

All customization happens inside the single `index.html`.

### Add / remove / reorder fields

1. Add the HTML input inside the `.grid`:
   ```html
   <div class="card">
     <div class="label-row">
       <span class="q-num">12</span>
       <span class="q-text">Your new question?</span>
     </div>
     <input type="text" name="yourFieldName" placeholder="…" />
   </div>
   ```

2. Register it in the `FIELDS` array in the script:
   ```js
   const FIELDS = [
     // …
     { key: 'yourFieldName', label: '12. Your new question' }
   ];
   ```

That's it — it will now appear in **Show answers** and in the **PDF**.

### Multiline values
Set `isMultiline: true` in the field definition to hint larger text blocks:
```js
{ key: 'annoyances', label: '9. Annoying / would change', isMultiline: true }
```

### Change the PDF colors
Look for these hex values in the script:
```js
doc.setFillColor(126, 94, 255);  // purple banner
doc.setFillColor(79, 140, 255);  // blue banner overlay
doc.setFillColor(126, 94, 255);  // number badge
```

### Change the theme (web UI)
Edit the gradients in `<style>`:
```css
body { background: linear-gradient(145deg, #f9f0ff 0%, #e5f4ff 100%); }
.btn-primary { background: linear-gradient(135deg, #7e5eff, #4f8cff); }
```

---

## 🌐 Browser Support

| Browser | Supported |
|---|---|
| Chrome / Edge (latest) | ✅ |
| Firefox (latest) | ✅ |
| Safari (iOS 14+) | ✅ |
| Samsung Internet | ✅ |
| IE 11 | ❌ (uses modern JS + CSS) |

> ⚠️ **Requires internet on first load** to fetch jsPDF from the CDN.
> To go fully offline, download `jspdf.umd.min.js` and point the script tag to your local copy.

---

## 🔒 Privacy

- All processing is **client-side**.
- No data is sent to any server.
- No analytics, no cookies, no tracking.
- The only external request is the jsPDF CDN script.

---

## 🗺️ Roadmap

- [ ] Optional `localStorage` autosave (draft recovery)
- [ ] Dark mode toggle
- [ ] CSV / JSON export alongside PDF
- [ ] Form validation with inline errors
- [ ] Offline jsPDF bundling

PRs welcome!

---

## 🤝 Contributing

1. Fork the repo
2. Create your branch: `git checkout -b feature/amazing-idea`
3. Commit: `git commit -m "Add amazing idea"`
4. Push: `git push origin feature/amazing-idea`
5. Open a Pull Request

Please keep it **single-file friendly** — no build step.

---

## 👤 Author

**Viresh Ranjanagi**
- GitHub: [@veereshr4446](https://github.com/veereshr4446)
- Live Demo: [veereshr4446.github.io/site-form-feedback](https://veereshr4446.github.io/site-form-feedback/)
- Built this form from scratch for our team's audit workflow.

---

## 📜 License

[MIT](LICENSE) © Viresh Ranjanagi

Free to use, modify, and share. Attribution appreciated but not required.

---

## 🙏 Acknowledgements

- [jsPDF](https://github.com/parallax/jsPDF) — the real-PDF engine
- Emoji icons via [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html)

---

## ⭐ Show your support

If this saved you time, drop a ⭐ on the repo — it helps more teams find it!

👉 [https://github.com/veereshr4446/site-form-feedback](https://github.com/veereshr4446/site-form-feedback)
```
