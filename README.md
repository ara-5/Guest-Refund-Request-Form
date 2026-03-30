# GuestStay — Refund Request Form

A polished, production-ready guest refund request form with cloud data persistence, dark mode, CSV export, and print-to-PDF.

## ✨ Features

- **All required fields** — Full Name, Email, Booking Reference, Booking Date, Refund Reason, Additional Details, File Upload
- **Conditional logic** — 90-day warning banner appears automatically when booking date is outside the refund window
- **Real data persistence** — Submissions saved to [JSONBin.io](https://jsonbin.io) (free cloud storage), with localStorage as an automatic fallback
- **Detailed submission summary** — Shows every field back to the user after submit, including a generated Request ID and timestamp
- **Dark mode** — Toggle in the header, preference saved to localStorage
- **CSV export** — Download the submission as a `.csv` file
- **Print / Save as PDF** — Clean print stylesheet hides UI chrome
- **Character counter** — Live counter on the Additional Details textarea
- **Drag & drop file upload** — With file size validation (10MB limit)
- **Mobile responsive** — Two-column layout collapses on small screens
- **Toast notifications** — Non-intrusive feedback on save/copy/download actions
- **XSS-safe** — All user input is HTML-escaped before rendering

---

## 🚀 Deploy in 2 Minutes

### Option A — Netlify (recommended, easiest)

1. Push this folder to a GitHub repository
2. Go to [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
3. Select your repo, leave all settings as default
4. Click **Deploy site** — done ✅

### Option B — Vercel

1. Push this folder to a GitHub repository
2. Go to [vercel.com](https://vercel.com) → **Add New Project**
3. Import your GitHub repo
4. Framework preset: **Other**
5. Click **Deploy** — done ✅

### Option C — GitHub Pages (no build needed)

1. Push to GitHub
2. Go to repo **Settings** → **Pages**
3. Source: `main` branch, `/ (root)`
4. Save — your site is live at `https://yourusername.github.io/repo-name`

---

## 🗄️ Data Persistence — JSONBin.io

Submissions are stored in a free JSONBin.io bin. Each submission is appended to a JSON array.

### View your submissions
1. Go to [jsonbin.io](https://jsonbin.io) and sign in
2. Navigate to **Bins** → find your bin by ID
3. You can view, edit, or export all submissions

### Use your own JSONBin bin
1. Sign up at [jsonbin.io](https://jsonbin.io) (free tier: 10,000 requests/month)
2. Create a new bin with initial value: `[]`
3. Copy your **Bin ID** and **Master Key**
4. In `index.html`, update these two lines at the top of the `<script>` block:

```js
const JSONBIN_BIN_ID = 'YOUR_BIN_ID_HERE';
const JSONBIN_API_KEY = 'YOUR_MASTER_KEY_HERE';
```

---

## 📁 Project Structure

```
refund-form/
├── index.html       # Complete single-file app (HTML + CSS + JS)
├── netlify.toml     # Netlify deployment config
├── vercel.json      # Vercel deployment config
└── README.md        # This file
```

---

## 🧪 Testing Checklist

| Feature | How to test |
|---|---|
| Validation | Submit with empty fields — each should show an error |
| 90-day warning | Pick a booking date > 90 days ago |
| Dark mode | Click the moon icon in the header |
| File upload | Drag a file onto the upload zone |
| CSV export | Submit a form, click "Export CSV" on the success screen |
| Print / PDF | Submit a form, click "Print / Save PDF" |
| Data persistence | Submit a form, check your JSONBin dashboard |

---

## 📄 License

MIT — free to use and modify.
