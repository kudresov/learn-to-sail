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
| 03 | Secondary Ports (tide heights and times) | planned |
| 04 | Buoys and Lights (IALA A) | planned |
| 05 | Rules of the Road (Rules 12–18, lights, shapes, sound signals, night encounters) | live |
| 06 | Night Watch (WebGL: lights and arcs in 3D, day shapes, fog signals, timed watch) | live |
| 07 | Weather | planned |

## Deploy

GitHub Pages from the `main` branch root. `.nojekyll` keeps Pages from processing the files.
