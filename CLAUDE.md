# Mustang Karyotype Lab

Single-file web game for Biology Standard 2.1, Chromosomes and Karyotyping (HS-LS3-1), Little Chute High School. Everything (HTML, CSS, JS) lives in `index.html`. No build step. Hosted on Vercel from the `main` branch of this GitHub repo, so every push to `main` redeploys automatically.

## Working rules

- Keep it a single self-contained `index.html`. No frameworks, no external scripts. Fonts come from Google Fonts only.
- No emoji anywhere in the app. Use the inline SVG icon set (`IC`) instead.
- Students have not learned mitosis yet. Do not use interphase, prophase, metaphase, or anaphase in lesson or game text unless the term is explained.
- Proficiency wording: Level 1 starts with "I can…", Levels 2 and 3 start with "Additionally, I can…".
- Prove It must stay auto-graded. No free-response questions.
- An NE (Not Enough Evidence) is never framed as failure.
- Every part of every lesson should have something students interact with, not just read.
- Respect `prefers-reduced-motion` (the `reduced` flag) for any new animation.
- Before committing, open `index.html` in a browser (or a local server) and check the change at desktop and phone widths in light and dark mode. Check the browser console for errors.
- Commit with a clear message and push to `main` when the change is verified.

## Where things live (search for these names in index.html)

- `LVINFO` – level names and "I can" statements.
- `LEARN` – all lesson pages for Levels 1–3. Each page is built from `SEC(...)` parts and `ACT(...)` activity boxes; `task(el)` registers an activity that must be finished before Continue unlocks.
- `SCREENS.intro`, `SCREENS.hub`, `SCREENS.learn`, `SCREENS.prove`, `SCREENS.results`, `SCREENS.report`, `SCREENS.arcade` – each screen.
- `buildRound(lv)` – which items appear in Level 1 and Level 2 Prove It. `GQ` – each graded item type (points, hints, feedback). `BANK`, `SORT`, `VOCAB`, `CONN` (Connections groups), `CAT_QS` (Chromo Catapult), `INV_PAIRS` (Vocab Invaders).
- `startProve`, `finishProve`, `makeCase`, `RENDER.case`, `RENDER.create` – Level 3 patient cases (1 point per diagnosis question) and the build-a-karyotype lab order (4/3/2/1 points by submission).
- `final()`, `bestAtt`, `complete`, `CUTS`, `L3_MAX` – scoring. Finishing a level's Prove It at any score unlocks the next level; the best round per level (by points) counts. The final level exists only once all three are finished: overall % of best points, 80/60/40 cut-offs, then the hint cap. No NE before that.
- `NOTES` – My Notes entries; each unlocks when the lesson part with the matching `note` key is finished.
- `HINT_MAX`, `hintCap`, `TIPS`, `HQ`, `hintFor` – Marty's hints and lesson tips. `martySVG`, `renderMarty`, `xaviMessage` – Marty the Mustang.
- `CONDS`, `BODY`, `FEAT`, `featArt` – conditions, the Level 3 body map, and the trait illustrations.
- `AMB_MODES`, `ambInit`, `burst` – animated background and celebration effects.
- Student progress is stored in localStorage under the key `mustang-karyo-lab-v1`. Changing that key wipes everyone's saved progress, so don't.
