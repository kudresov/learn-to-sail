# Learn to Sail

Interactive drills for the RYA Day Skipper / Coastal Skipper shorebased syllabus.
Plain static HTML, no build step. Open `index.html` or serve the folder.

```sh
python3 -m http.server 8080   # then http://localhost:8080
```

## Layout

```
index.html              landing page and tutorial catalogue
shared/site.css         colour tokens (light/dark), fonts, nav and footer
tutorials/<slug>/       one self-contained tutorial per folder (index.html)
```

## Adding a tutorial

1. Create `tutorials/<slug>/index.html`. Link `../../shared/site.css`, copy the `site-nav` and `site-foot` markup from an existing tutorial.
2. Keep tutorial-specific CSS and JS inline in that page. Persist progress in `localStorage` under `lts:<slug>:v<n>`.
3. Add a card to `index.html`.

## Tutorials

| # | Tutorial | Status |
|---|----------|--------|
| 01 | Three Norths (true / magnetic / compass, variation, deviation, passage) | live |
| 02 | Course to Steer (tidal vectors, leeway) | next |
| 03 | Tidal Heights (datum, twelfths, tidal curve, secondary ports, harbour entry) | live |
| 04 | Buoys and Lights (IALA A) | planned |
| 05 | Rules of the Road (Rules 12–18, lights, shapes, sound signals, night encounters) | live |
| 06 | Night Watch (WebGL: lights and arcs in 3D, buoys by night, who gives way, day shapes, fog signals, timed watch) | live |
| 07 | Night Sim (real-time conn under sail: helm and tack, steady bearing, port tack gives way) | prototype |
| 08 | Weather | planned |

## Reference

| Page | Contents |
|------|----------|
| `cheatsheet/` | Day Skipper theory cheat sheet: print-first HTML plus `rya-day-skipper-cheatsheet.pdf` (A4, 19 pages) covering all 14 syllabus areas and a single-page summary. |

Regenerate the PDF after editing `cheatsheet/index.html`:

```sh
python3 -m http.server 8080 &
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu \
  --no-pdf-header-footer --virtual-time-budget=20000 \
  --print-to-pdf=cheatsheet/rya-day-skipper-cheatsheet.pdf http://localhost:8080/cheatsheet/
```

## Deploy

GitHub Pages from the `main` branch root. `.nojekyll` keeps Pages from processing the files.
