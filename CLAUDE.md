# Learn to Sail

Interactive drills that make the RYA Day Skipper / Coastal Skipper shorebased
syllabus stick. Learn by doing, keep it by repeating. Everything here serves that
one goal: a learner should close a tutorial able to do the thing under exam
pressure, not merely having read about it.

## Mission and pedagogy

Every tutorial is a **ladder of stages**, not a page of notes. Design rules,
derived from `tutorials/compass/` (the reference implementation):

- **One skill per stage, one stage on screen.** Start with the simplest case
  (variation only), add one complication per stage (wrap through 360, deviation,
  opposite signs, the card, the decoy). Never introduce two new ideas at once.
- **Gate progression on evidence, not clicks.** A stage unlocks the next only
  when the learner hits a pass bar (e.g. 6 of last 8, or 12 timed questions at a minute
  each with at most 1 wrong). Store recent results; never gate on a single
  answer.
- **Consequences, not red crosses.** Wrong answers should show what would
  happen at sea: a wrong course to steer plots where the boat actually ends up,
  three wrong on a passage puts you aground. Make errors memorable.
- **Feedback teaches the rule.** On every check, show the worked steps and
  restate the rule in one breath (mnemonic + example). Never just "incorrect".
- **Finish at exam pace.** The final stage of every tutorial is a timed mixed
  drill with no scaffolding, matching roughly the time the RYA exam allows.
- **Mnemonics and habits examiners like.** Surface the standard RYA phrasing
  (West is best / CADET / True Virgins Make Dull Company; three figures always,
  suffix always) and enforce those habits in answer validation.
- **Concept card per stage.** Short intro paragraph plus one worked example,
  collapsible, with a "rules in one breath" reference at the bottom of the page.
- **Small joys.** Streaks, a ship's log, tiny WebAudio tones, "10 in a row"
  pops. Fun is a retention tool, keep it light and never blocking.
- **Randomise generously.** Generate questions from config, not fixed lists,
  so repetition never becomes memorising answers.

## Content accuracy

- Follow RYA Day Skipper / Coastal Skipper shorebased syllabus terminology and
  conventions exactly. If unsure of a rule, sign convention, or IALA detail,
  say so and check rather than invent. Wrong sailing content is worse than no
  tutorial.
- Bearings: three figures, degree sign, suffix T/M/C. Wrap 000–359.
- Deviation is looked up by ship's heading, never by bearing of an object.
- Charts and passages are schematic but must be internally consistent
  (bearings computed from coordinates, distances in nm from a stated scale).

## Tech constraints

Plain static site, **no build step, no framework, no dependencies**. GitHub
Pages serves `main` root; `.nojekyll` is required.

```
index.html              landing page + tutorial catalogue (add a card per tutorial)
shared/site.css         colour tokens (light/dark), fonts, nav, footer
tutorials/<slug>/       one self-contained tutorial, index.html only
```

- **Tutorial pages are self-contained**: tutorial CSS and JS inline in
  `tutorials/<slug>/index.html`. Only `../../shared/site.css` and Google Fonts
  are external. Copy `site-nav` and `site-foot` markup from an existing tutorial.
- **Theme**: use the tokens in `shared/site.css` (`--ink`, `--paper`,
  `--magenta`, `--good`, `--bad` ...). Never hardcode colours. Light/dark must
  both work; dark is `prefers-color-scheme` or `[data-theme="dark"]`.
- **Fonts**: Libre Caslon Text (headings), Source Sans 3 (body), IBM Plex Mono
  (bearings, numbers, `tabular-nums`). Always with fallbacks.
- **Persistence**: `localStorage` under `lts:<slug>:v<n>`. Bump `v<n>` when the
  stored shape changes; do not write migrations. Wrap reads in try/catch.
- **Keyboard first**: Enter checks, Enter again advances, Alt+←/→ change stage.
  Every drill must be completable without a mouse.
- **Responsive**: works at 400px width. Body handles side padding; no
  horizontal scroll.
- **Accessibility**: `aria-label` on question regions, visible focus, no
  colour-only feedback (pair with text/icon).
- Vanilla ES2020+, no transpile. Keep each tutorial roughly under 60KB.

## Workflow

- Run locally: `python3 -m http.server 8080` then open `http://localhost:8080`.
- Before committing a tutorial change: load the page, check console for errors,
  click through every stage, clear `localStorage` and load again (first-run
  path crashes are the usual bug).
- New tutorial: create the folder, add a card to `index.html`, update the
  tutorials table in `README.md`.
- Commits: conventional style, scope is the tutorial slug
  (`feat(course-to-steer): ...`, `fix(compass): ...`). Body explains why.
- Source comments only for non-obvious *why*. No PR-context in code.

## Roadmap (see README table)

Three Norths is live. Next in order: Course to Steer (tidal vectors, leeway),
Secondary Ports, Buoys and Lights (IALA A), Rules of the Road, Weather. Each
follows the same ladder shape: isolate, combine, apply on a chart, exam pace.
