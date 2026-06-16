# BusinessPro

A complete, **local-first** business toolkit for freelancers and small businesses — invoices, quotes, contracts, and contacts — in a single HTML file. No accounts, no subscriptions, no cloud, no tracking. Your data never leaves your machine.

Free and open source under the [MIT License](LICENSE).

## Features

- **Invoices** — line items, tax, partial payments, payment history, balance tracking
- **Quotes** — convert a quote to an invoice or a contract in one click
- **Contracts** — generate from quotes, track status, turn into invoices
- **Contacts** — customers and the records linked to them
- **PDF export & print** for every document
- **JSON backup** — export and import all your data anytime
- **Local network sharing** — let others on your WiFi view your data read-only, no cloud involved
- **Works fully offline** — every dependency is vendored; nothing is fetched from the internet at runtime

## Storage

Your data lives in your browser's **IndexedDB** (via [Dexie](https://dexie.org/)) — not in the HTML file, not on a server. This handles large logos and a growing document history without the size limits of `localStorage`.

- On first launch the app starts **empty**. Open **Settings → Data Management → Load Sample Data** to explore a realistic dataset, then **Clear All Data** when you're ready to start for real.
- On startup the app asks the browser to mark your storage as **persistent** (`navigator.storage.persist()`) so it isn't evicted under storage pressure. Support varies by browser.
- Upgrading from an older version that used `localStorage`? Your data is migrated to IndexedDB automatically the first time you open this version.

> **Back up your data.** IndexedDB is tied to a specific browser profile on a specific machine. Clearing site data, switching browsers, or moving computers will not carry your records over. Use **Export Data** regularly — the app reminds you weekly.

## Running it

It's a static site with no build step.

**Just open it:** double-click `index.html`, or open it in any modern browser.

**Or serve it** (recommended for local-network sharing — see Settings for the in-app guide):

```bash
# from the project folder
python3 -m http.server 8080
# then open http://localhost:8080/index.html
```

**Live demo:** a hosted copy is published via GitHub Pages on every push to `main`
(see `.github/workflows/deploy.yml`). To enable it once, in your repo go to
**Settings → Pages → Source → GitHub Actions**. The demo runs entirely in the
visitor's browser — it stores nothing on any server.

## Project layout

```
index.html                 The entire app — HTML, CSS, and JS in one file
vendor/
  dexie.min.js             IndexedDB wrapper (v3.2.4)
  html2pdf.bundle.min.js   PDF export (v0.10.1)
  fonts/                   DM Sans, self-hosted (no Google Fonts call)
.github/workflows/
  deploy.yml               Publishes to GitHub Pages on push to main
LICENSE
README.md
```

All third-party libraries are vendored locally and pinned, so the app is fully self-contained and works with no network connection.

## Browser support

Any current version of Chrome, Edge, Firefox, or Safari. Requires IndexedDB (available in all of the above). Private/incognito windows may restrict or discard storage — use a normal window for real data.

## Privacy

There is no analytics, no telemetry, and no network calls at runtime. The app cannot send your data anywhere because it never tries to.

## Contributing

Issues and pull requests are welcome. Because the app is a single file, keep changes focused and test by opening `index.html` directly.

## License

[MIT](LICENSE) © [Rene Kropf](https://github.com/rene-kropf)

Bundled third-party libraries keep their own licenses: Dexie (Apache-2.0) and
html2pdf.js (MIT). Vendored fonts (DM Sans, Fraunces) are under the SIL Open
Font License 1.1 — see [`vendor/fonts/OFL.txt`](vendor/fonts/OFL.txt).
