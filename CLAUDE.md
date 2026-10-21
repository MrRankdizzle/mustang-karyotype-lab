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
- Respect the `reduced` flag for any new animation (and use `.rm` in CSS, not a `prefers-reduced-motion` media query; SVG `<animate>` goes through `noMotion`). The flag comes only from the Motion setting in Settings (`setMotion`, saved in localStorage under `mustang-karyo-motion`). It defaults to Full for everyone. Never read the operating system's `prefers-reduced-motion`: many school computers have it on, and following it froze the animations. Background animation is a separate on/off setting.
- Color-blind-friendly mode (`.cb` on `<html>`, `CB()` in JS): anything new that uses color to carry meaning (right/wrong, groups, rows, mom/dad, progress) also needs a non-color cue under `.cb`, such as a check/X badge, a shape, a number, or a label.
- Size new text in rem, not px, so the Text size setting scales it.
- Animation loops book their next frame first (`raf=requestAnimationFrame(loop)` at the top), so one bad frame can't stop them.
- Before committing, open `index.html` in a browser (or a local server) and check the change at desktop and phone widths in light and dark mode. Check the browser console for errors.
- Commit with a clear message and push to `main` when the change is verified.

## Where things live (search for these names in index.html)

- `LVINFO` – level names and "I can" statements.
- `LEARN` – all lesson pages for Levels 1–3. Each page is built from `SEC(...)` parts and `ACT(...)` activity boxes; `task(el)` registers an activity that must be finished before Continue unlocks.
- `SCREENS.intro`, `SCREENS.hub`, `SCREENS.learn`, `SCREENS.prove`, `SCREENS.results`, `SCREENS.report`, `SCREENS.arcade` – each screen.
- `buildRound(lv)` – which items appear in Level 1 and Level 2 Prove It. `GQ` – each graded item type (points, hints, feedback). `BANK`, `SORT`, `VOCAB` (word games; `xtra` words appear only in lessons and the Arcade, never in Prove It; `freshWord` avoids words a student saw recently), `CONN` (Connections groups), `CAT_QS` (Chromo Catapult), `INV_PAIRS` (Vocab Invaders).
- `startProve`, `finishProve`, `makeCase`, `RENDER.case`, `RENDER.create` – Level 3 patient cases (1 point per diagnosis question) and the build-a-karyotype lab order (4/3/2/1 points by submission).
- `final()`, `bestAtt`, `complete`, `CUTS`, `L3_MAX` – scoring. Finishing a level's Prove It at any score unlocks the next level; the best round per level (by points) counts. The final level exists only once all three are finished: overall % of best points, 80/60/40 cut-offs, then the hint cap. No NE before that.
- `PACK_STAGES`, `packFrame`, `drawPack`, `PACK_LABELS`, `packCinema` – the Level 1 DNA packing animation: five scenes on one timeline (seconds), step controls in `LEARN[1][0].bind`, and the full-screen "Play full animation" view.
- `photoBooth`, `martySig`, `S.photo` – the webcam lab ID photo on the credential report (kept in the student's saved progress, never uploaded) and Marty's signature (Marty the Mustang, Lab Assistant), which appears once all three levels are finished.
- `reportCanvas`, `jpegPDF`, `downloadReport` – the Download PDF / Download PNG buttons on the credential report. The report is redrawn on a canvas as one light-colored, letter-width page (it grows taller if needed); the PDF wraps a JPEG of that page and is written by hand, so no library is needed. Anything new on the report screen should be added there too.
- `SET`, `SET_KEYS`, `applySettings`, `setSetting`, `openSettings` – the Settings drawer (menu button in the top bar): Theme, Text size, Motion, Background animation, Color vision, Dyslexia-friendly reading (Lexend), Reading ruler (`ruler`), plus Contents, Credential report, and Start over. Each setting has its own localStorage key (`mustang-karyo-theme`, `-text`, `-motion`, `-bg`, `-cvd`, `-dyslexia`, `-ruler`), so Start over keeps them. A small script in `<head>` applies them before the page paints. Canvases repaint on theme changes through `onScheme`; use `isDark()` instead of reading the color-scheme media query.
- `ORGS`, `FAKES`, `impostor` – the Level 1 species match (Human plus three others each time) and the Spot the impostor activity.
- `tableGame`, `rowMark` – the rebuild-the-table game: placed tiles lock in their row color with a checkmark stamp.
- `mountUnscramble` – Prove It scramble items: students can type the answer or tap/drag letter tiles; both stay in sync.
- `ndFigure`, `ndRows`, `ndAnim` – Level 2 "Too many, too few": the mistake can happen in the egg or the sperm (Mistake in: Egg/Sperm), and chromosome 21 is drawn as a copied, banded chromosome like the Level 3 karyotypes.
- `layoutPins`, `watchPins` – placed gene pins sit in a column beside the chromosome 11 ideogram with leader lines, so they never cover a band.
- `AMB.calm` – the animated background holds still if the page runs under about 24 frames a second.
- `NOTES` – My Notes entries; each unlocks when the lesson part with the matching `note` key is finished.
- `HINT_MAX`, `hintCap`, `TIPS`, `HQ`, `hintFor` – Marty's hints and lesson tips. `martySVG`, `renderMarty`, `xaviMessage` – Marty the Mustang.
- `CONDS`, `BODY`, `FEAT`, `featArt` – conditions, the Level 3 body map, and the trait illustrations.
- `AMB_MODES`, `ambInit`, `burst` – animated background and celebration effects.
- Student progress is stored in localStorage under the key `mustang-karyo-lab-v1`. Changing that key wipes everyone's saved progress, so don't.
