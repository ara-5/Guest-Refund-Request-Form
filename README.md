# GuestStay — Guest Refund Request Form

> A production-ready internal tool built as part of a take-home engineering assessment. Demonstrates full-stack thinking in a zero-dependency, single-file frontend: cloud persistence, conditional UX logic, security hardening, and a polished UI — deployed and live.

**[→ Live Demo](https://celadon-churros-e0523d.netlify.app/)** &nbsp;|&nbsp; Built with: HTML · CSS · Vanilla JS · JSONBin.io

---

## What This Is

A web form where guests can submit a refund request for a property booking. It was built to a specific product spec — matching real-world criteria around field validation, conditional logic, data persistence, and mobile responsiveness — and goes beyond the requirements with several production-grade additions.

The entire app ships as a **single `index.html` file** with no build step, no npm, no framework. This was a deliberate choice: it deploys anywhere (Netlify, Vercel, GitHub Pages) in under a minute, and keeps the codebase readable without toolchain overhead.

---

## Features

**Required spec:**
- All 7 fields: Full Name, Email, Booking Reference, Booking Date, Refund Reason (dropdown), Additional Details, File Upload
- Conditional 90-day warning banner — appears and hides dynamically as the user changes the date
- Full client-side validation with per-field inline error messages
- Detailed submission summary — shows every field back to the user, not just "success"
- Cloud persistence via JSONBin.io with localStorage as an automatic offline fallback
- Mobile responsive — two-column layout collapses gracefully at 560px

**Beyond the spec:**
- Dark mode with saved preference
- CSV export of the submission (Excel-compatible with UTF-8 BOM)
- Print / Save as PDF with a clean print stylesheet
- Loading spinner during cloud save
- Character counter on the textarea (warns at 700 chars, errors at 900+)
- Drag & drop file upload with MIME-type validation and 10MB size limit
- Client-side rate limiting (max 3 submissions per 60 seconds)
- Future booking date guard
- Dropdown value allowlist validated in JavaScript (not just HTML)
- All user input HTML-escaped before DOM insertion — no XSS vectors
- CSP meta tag + security response headers via `netlify.toml` / `vercel.json`
- Scoped JSONBin Access Key (read + update only — not the master key)

---

## Technical Decisions Worth Noting

**Why JSONBin instead of a spreadsheet or database?**
For a take-home with no backend, JSONBin gives genuinely retrievable, persistent cloud storage accessible via a REST API — not just `console.log` or ephemeral memory. The data is viewable, exportable, and queryable. localStorage alone wouldn't pass a "retrievable" bar.

**Why a scoped Access Key instead of the Master Key?**
The key lives in client-side code, visible to anyone who opens DevTools. Using the Master Key there would expose every bin in the account. The Access Key is restricted to read + update on this specific bin only — minimum viable permissions for the job.

**Why validate the dropdown value in JS?**
HTML `<select>` elements can be trivially manipulated via DevTools. Checking the submitted value against `ALLOWED_REASONS` in JavaScript mirrors how you'd validate an enum on a backend — it prevents arbitrary strings from being written to the database.

**Why a single file?**
Deliberate tradeoff for this context. A component-based structure (React, Vue) adds real value at scale. For a form this size, a single well-commented file is more readable to a reviewer than a project with 15 files and a build pipeline. Code organisation lives in clear section comments instead of file boundaries.

---

## Running Locally

No install needed:

```bash
git clone https://github.com/ara-5/Guest-Refund-Request-Form.git
cd Guest-Refund-Request-Form
open index.html   # or double-click in Finder / Explorer
```

Or with a static server:

```bash
npx serve .
# → http://localhost:3000
```

---

## Deploying Your Own Copy

### Netlify (recommended — security headers included)
1. Fork this repo
2. [netlify.com](https://netlify.com) → **Add new site** → **Import from Git** → select fork → **Deploy**

Security headers in `netlify.toml` are applied automatically.

### Vercel
1. Fork this repo
2. [vercel.com](https://vercel.com) → **Add New Project** → import fork → Framework: **Other** → **Deploy**

### GitHub Pages
1. Fork this repo
2. **Settings** → **Pages** → Source: `main` branch, `/ (root)` → **Save**

---

## Using Your Own JSONBin

1. Sign up at [jsonbin.io](https://jsonbin.io) (free — 10,000 req/month)
2. Create a bin with initial value: `{ "data": [] }`
3. **Access Keys** → **Create Access Key** → grant **Read + Create + Update** on that bin only (not Delete)
4. In `index.html`, update the two constants at the top of the `<script>` block:

```js
const JSONBIN_BIN_ID  = 'YOUR_BIN_ID';
const JSONBIN_API_KEY = 'YOUR_ACCESS_KEY';
```

---

## Project Structure

```
├── index.html      ← Full app (HTML + CSS + JS)
├── netlify.toml    ← Deploy config + security headers
├── vercel.json     ← Deploy config + security headers
├── .gitignore
└── README.md
```

---

## License

MIT

## Author

Built by **Athira Anil Kumar**
