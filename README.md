# Lomy Studio — marketing site

Static implementation of the `MarketingSite.dc.html` template from the Lomy
Studio design system (Claude Design handoff bundle). No build step, no
dependencies: open `index.html` or serve the folder.

```
index.html              one page: header, hero, marquee, services, process,
                        why us, testimonial, CTA, footer
assets/css/ds.css       design-system CSS, generated from the bundle
                        (fonts.css + tokens/*.css + base.css, concatenated)
assets/css/site.css     page styles — the design's inline styles as classes
assets/fonts/*.woff2    self-hosted Archivo, Poppins, Libre Baskerville,
                        Bricolage Grotesque
assets/img/             logo.svg, logo-mark.svg (mark is the favicon)
netlify.toml            publish the repo root as-is, no build command
```

## Hosting

The site is hosted on Netlify (project `lomy-studio`, team `el-omar`), linked
to this repository: every push to `main` deploys automatically. `netlify.toml`
tells Netlify to publish the repo root with no build step.

## Serving locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

Opening `index.html` via `file://` works too, but self-hosted fonts are
subject to the browser's local-file rules — prefer the server.

## Notes on fidelity

- Every value in `site.css` is taken verbatim from the design file. Nothing was
  rounded or snapped to a grid.
- **Responsive rules are an addition.** The design is desktop-only. Rendering at
  >900px is untouched; below that the service and "why us" rows stack, the three
  process steps go to one column, the header nav wraps onto a second row, and
  the two decorative circles scale down so they stay behind their headings.
- **`--header-h` is 72px, not the design's 64px.** The sticky header measures
  69px, so 64px left section tops slightly under the bar. 72px makes anchors
  land 2–5px clear of it, which is what the design chat asked for.
- The logo is set in live type (Bricolage Grotesque 800 with the coral dot,
  letterspaced STUDIO beneath), matching the design. `assets/img/logo.svg` is
  the same lockup as a file — it also uses live text, so outline the type before
  sending it to a print vendor.
- "Start a campaign" links point at the on-page `#contact` CTA. The design
  also had a contact-page template, which is not part of this build.
- Dark mode: the tokens ship a `[data-theme="dark"]` block, and `<html>` carries
  `data-theme="light"`. Switching the attribute mostly works, but the design was
  only tuned for light — the dark process band's hairline is a hardcoded
  `rgba(240,234,224,.25)` that nearly disappears when the band inverts.

## Content that is still placeholder

The testimonial (Yoshi De Schrijver) came from the design as a real quote;
everything else is the copy the user settled on in the design chat. The contact
address is `info@lomy.studio` throughout.
