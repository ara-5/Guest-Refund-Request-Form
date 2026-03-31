# GuestStay — Refund Request Form

A polished, production-ready guest refund request form with cloud data persistence, dark mode, CSV export, and print-to-PDF. Built as a single-file static HTML application — no build step, no dependencies, deploys anywhere.

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/YOUR_USERNAME/gueststay-refund)

---

## ✨ Features

| Feature | Details |
|---|---|
| **All required fields** | Full Name, Email, Booking Reference, Booking Date, Refund Reason (dropdown), Additional Details, File Upload |
| **Conditional logic** | Yellow warning banner auto-shows when booking date is > 90 days ago; hides when corrected |
| **Full validation** | Required field checks, email format, future-date guard, dropdown allowlist |
| **Cloud persistence** | Submissions saved to JSONBin.io (free, retrievable via dashboard/API) |
| **Local backup** | localStorage always written as offline fallback |
| **Detailed summary** | Success screen shows every submitted field + generated Request ID + timestamp |
| **Dark mode** | Toggle in header; preference saved to localStorage |
| **CSV export** | Download the submission as a UTF-8 BOM `.csv` (Excel-compatible) |
| **Print / PDF** | Clean print stylesheet; hides form chrome, shows summary only |
| **Character counter** | Live count on textarea; warns at 700, red at 900+ |
| **Drag & drop upload** | With MIME-type validation, 10 MB size limit, max 5 files |
| **Rate limiting** | Client-side: max 3 submissions per 60 seconds |
| **Loading spinner** | Button shows spinner during cloud save |
| **Toast notifications** | Non-intrusive save/export/error feedback |
| **Accessible** | ARIA labels, roles, `aria-live` regions, `focus-visible` rings |
| **Security hardened** | CSP meta tag, HTTP security headers, XSS-safe rendering, input allowlists, length caps |
| **Mobile responsive** | Two-column layout collapses at 560 px; full mobile optimisation at 480 px |

---

## 🖼️ Screenshots

> Add your own screenshots here after deploying.

---

## 🚀 Deploy in Under 5 Minutes

### Option A — Netlify *(recommended)*

1. Push this repo to GitHub
2. Go to [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
3. Select your repo — leave all settings default
4. Click **Deploy site**
5. You get a free live URL: `https://your-site.netlify.app`

Security headers are applied automatically via `netlify.toml`.

### Option B — Vercel

1. Push to GitHub
2. Go to [vercel.com](https://vercel.com) → **Add New Project** → import repo
3. Framework preset: **Other**
4. Click **Deploy**

Security headers applied via `vercel.json`.

### Option C — GitHub Pages *(no extra account needed)*

1. Push to GitHub
2. Repo **Settings** → **Pages** → Source: `main` branch, `/ (root)`
3. Live at: `https://yourusername.github.io/gueststay-refund`

> Note: GitHub Pages does not apply custom HTTP headers, so `netlify.toml`/`vercel.json` headers won't be active — the CSP `<meta>` tag still protects against XSS.

---

## 🗄️ Data Persistence — JSONBin.io

Submissions are stored in a **JSONBin.io** bin as a JSON array under the key `data`.

### View your submissions

1. Go to [jsonbin.io](https://jsonbin.io) and sign in (or sign up — it's free)
2. Navigate to **Bins** → find your bin by the ID in `index.html`
3. You can view all submissions directly in the dashboard or via the REST API

### Use your own private bin (recommended for production)

```bash
# 1. Sign up at https://jsonbin.io (free tier: 10,000 req/month)
# 2. Create a new bin with initial value:
{ "data": [] }

# 3. Go to Access Keys → Create New Key
#    Grant: Read + Update on that specific bin ONLY (NOT the Master Key)

# 4. In index.html, update these two constants at the top of <script>:
```

```js
const JSONBIN_BIN_ID  = 'YOUR_BIN_ID_HERE';
const JSONBIN_API_KEY = 'YOUR_ACCESS_KEY_HERE';
```

> **Security note:** The included Access Key is scoped to read + update this demo bin only.  
> It is **not** the Master Key. It cannot delete data, access other bins, or touch account settings.  
> For production, always create your own bin and key.

---

## 🔒 Security Notes

| Measure | Implementation |
|---|---|
| **XSS prevention** | All user input rendered via `textContent` or the `esc()` HTML-escape function — never raw `innerHTML` |
| **Input allowlist** | Dropdown value validated server-side-style against `ALLOWED_REASONS` array |
| **Input length caps** | `maxlength` attributes + JS `.slice()` on all text fields |
| **Future-date guard** | Date input `max` attribute + JS validation rejects future dates |
| **File validation** | MIME type allowlist + 10 MB per-file limit + 5 file maximum |
| **Rate limiting** | Client-side: 3 submissions per 60 seconds (localStorage timestamp tracking) |
| **CSP meta tag** | Restricts scripts, styles, fonts, and connections to known safe origins |
| **HTTP headers** | `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Referrer-Policy` |
| **Scoped API key** | JSONBin Access Key has minimum permissions (no delete, no account access) |

---

## 📁 Project Structure

```
gueststay-refund/
├── index.html      ← Complete app: HTML + CSS + JS (single file, no build needed)
├── netlify.toml    ← Netlify deployment config + security headers
├── vercel.json     ← Vercel deployment config + security headers
├── .gitignore
└── README.md
```

---

## 🧪 Testing Checklist

| Test | How to verify |
|---|---|
| All fields required | Submit empty — every field should show an error message |
| Email validation | Enter `notanemail` — should reject |
| Future date rejected | Pick tomorrow — should show "cannot be in the future" |
| 90-day warning | Pick a date > 90 days ago — amber banner should appear; update to recent date — banner hides |
| Dropdown allowlist | Open DevTools, change an `<option>` value to `Hacked` — submission should reject it |
| File type guard | Try uploading an `.exe` — should be skipped with a toast |
| File size guard | Try a file > 10 MB — should be skipped |
| Dark mode | Click 🌙 in the header |
| Success summary | Submit — verify every field appears correctly in the confirmation |
| Cloud save | Submit — check your JSONBin dashboard for the new record |
| CSV export | Click "Export CSV" on success screen — open in Excel |
| Print | Click "Print / Save PDF" — form should be hidden, only summary printed |
| Rate limit | Submit 3 times quickly — 4th should be blocked |
| Mobile | Resize browser to < 480 px — layout should remain usable |

---

## 🛠️ Customisation

### Change the brand name / colours

Edit the CSS variables in `:root` at the top of `index.html`:

```css
:root {
  --terracotta: #c4673a;   /* accent colour */
  --cream:      #faf8f4;   /* page background */
  /* ... */
}
```

### Add more refund reasons

Update both the `<select>` options in the HTML **and** the `ALLOWED_REASONS` array in JS:

```js
const ALLOWED_REASONS = Object.freeze([
  'Property Issue', 'Booking Error', 'Personal Reasons', 'Other',
  'YOUR_NEW_REASON'
]);
```

---

## 📄 Licence

MIT — free to use, modify, and distribute.
