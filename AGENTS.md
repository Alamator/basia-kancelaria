# AGENTS.md

## Cursor Cloud specific instructions

This repository is a **static website** — plain HTML/CSS/JS with no framework, no
package manager, no build step, and no automated tests or linters. See `README.md`
for the project overview and file structure.

### Services

There is a single "service": the static site itself. To develop/run it, serve the
repository root over HTTP so relative asset paths resolve:

```
python3 -m http.server 8000
```

Then open `http://localhost:8000/`. Key routes: `/` (`index.html`),
`/podzial-majatku.html`, `/polityka-prywatnosci.html`.

### Notes / caveats

- **No dependencies to install** — the only external runtime dependency is Google
  Fonts, loaded from a CDN at page load, so the site needs outbound network access
  to render its intended typography (it still renders with fallback fonts offline).
- **No build / no tests / no lint.** There is nothing to compile and no test or lint
  command. "Testing" means serving the site and checking pages/behavior in a browser.
- **Contact form** (`#contactForm` in `index.html`) POSTs to the live Web3Forms API
  (`api.web3forms.com`) using a real `access_key`. Submitting it sends a real email to
  the law firm. When testing, fill/validate the form but do **not** submit it to the
  live endpoint.
- Do not open `index.html` via the `file://` protocol for form/asset testing — serve
  over HTTP instead.
