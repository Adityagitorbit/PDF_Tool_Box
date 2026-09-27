# PDF Toolbox (Web)

A single-page, client-side PDF utility — **Images → PDF** and **Merge PDFs**.
No backend, no uploads: everything runs in the visitor's browser using
[pdf-lib](https://pdf-lib.js.org/) and [jsPDF](https://github.com/parallax/jsPDF),
loaded from a CDN. Files never leave the user's device.

**Live structure:** it's one self-contained file, `index.html` — no build
step, no `npm install`, no server.

## Features

- Drag-and-drop (or click to browse) file selection, with drag-to-reorder.
- **Images → PDF**: converts a batch of images into one PDF, with an
  optional auto-rotate-landscape-to-portrait option.
- **Merge PDFs**: combines multiple PDFs into one, skipping any file that
  fails to parse.
- A rough, honest memory-budget estimate (browsers don't expose real free
  RAM, so this is an approximation) that warns before a batch is likely to
  make the tab slow or crash, plus a live safety check during processing.
- Light/dark theme aware (follows the OS/browser preference).

## Run it locally

No install needed — just open the file:

```bash
open index.html        # macOS
start index.html        # Windows
xdg-open index.html     # Linux
```

Or serve it (some browsers restrict file:// access to certain APIs):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy for free with GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`,
   branch `main`, folder `/ (root)`.
4. Save. Your site will be live at
   `https://<your-username>.github.io/<repo-name>/` within a minute or two.

Any other static host works the same way (Netlify, Cloudflare Pages,
Vercel, S3 + CloudFront, etc.) — just point it at `index.html`.

## Project structure

```
pdf-toolbox-web/
├── index.html     # the entire app: markup, styles, and JS in one file
├── README.md
└── LICENSE
```

## Notes for future changes

- All logic lives in the single `<script>` block at the bottom of
  `index.html` — `setupList()` handles the drag-and-drop file lists (shared
  by both tools), and each tool's "run" button has its own handler.
- The memory-estimate logic (`navigator.deviceMemory`, the budget
  calculation, and the warning banners) is near the top of the script if
  you want to tune the percentage or wording.
- If you add ads (e.g. Google AdSense), remember the page currently loads
  scripts only from `cdnjs.cloudflare.com` — an ad network's script tag
  will need its own `<script src="...">` added; there's no CSP restricting
  this file once it's hosted outside Claude's artifact environment.
- If you host this elsewhere and add any tracking/ads, add a short privacy
  note — the tool itself never uploads user files, but ad scripts may set
  cookies.

## License

MIT — see [LICENSE](LICENSE).
