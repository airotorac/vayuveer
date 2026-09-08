# Vayuveer — vayuveer.in

Single-file 3D scrolling website for Vayuveer (UAV / drone company).
Everything lives in `index.html`: markup, styles, and the Three.js scene.
No build step. Upload the file to any static host and point vayuveer.in at it.

## Run locally

```bash
python3 -m http.server 8765
```

Then open http://localhost:8765

## Deploy

Any static host works. Examples:

- **Netlify / Vercel / Cloudflare Pages** — drag the folder in, add `vayuveer.in` as a custom domain, set the DNS records they give you.
- **GitHub Pages** — push this folder to a repo, enable Pages, add a `CNAME` file containing `vayuveer.in`.
- **cPanel / shared hosting** — upload `index.html` to `public_html`.

External dependencies (loaded from CDNs, so the host needs no build tooling):

- Three.js 0.160 from jsdelivr
- Google Fonts: Rajdhani, Manrope, JetBrains Mono

## Editing content

Everything that names a product or a number is placeholder copy written to look real. Replace before launch:

| What | Where in `index.html` |
|---|---|
| Product names (Baaz, Netra, Vahak, Agni, Rakshak, Urdhva, Pushpak) | each `<article class="bay">`, the altimeter rail, the contact form `<select>`, the footer |
| Specs (endurance, payload, range, etc.) | the `<dl class="specs">` block inside each bay |
| Contact emails | `hello@vayuveer.in`, `partners@vayuveer.in` in the contact section and the form script |
| Autonomy / compliance claims | `#capabilities` and `#compliance` sections |

The contact form opens the visitor's mail client (mailto). To collect submissions server-side instead, point the form at Formspree, Netlify Forms, or your own endpoint and remove the submit handler at the bottom of the script.

## The 3D models

The seven drones are built procedurally in `buildBaaz`, `buildNetra`, etc. near the bottom of `index.html`. To use real models instead, export GLB files from your CAD tool, load them with Three.js `GLTFLoader`, and return the loaded group from the matching builder. Camera distance per bay is set in the `BAYS` array (`dist`), so larger models just need a bigger number there.
