# Amrit Vela — Morning Companion

## The aim (in the user's own words)

> "an app that helps me wake up early and make the most of my day so I can
> fulfil the purpose of my life to experience Vaheguru Jee while alive"

Everything below serves that one sentence. It is a companion for a daily
practice, not a habit-tracking product. **The bar for any new feature is: does
this help someone rise in amrit vela and stay turned toward Waheguru through
the day?** If it doesn't, leave it out — the quiet of this app is a
feature, and four screens of widgets would work against the thing it's for.

*Amrit vela* is the pre-dawn window (~3–6am), held in Sikh practice as the best
hours for simran / remembrance. The app has four movements, in daily order:
wake check-in → simran → one intention (sankalp) → evening reflection.

## Files

- `index.html` — the entire app. No build step, no dependencies except Google
  Fonts via `@import`. Open it directly in a browser, or serve the folder.

## Data model

One JS object, saved as a single JSON blob under `amrit-vela-data`
(deliberately one key, not several, to keep writes batched):

```js
state = {
  wakeLog:     [{ date: 'YYYY-MM-DD', time: 'HH:MM' }, ...],
  intentions:  { 'YYYY-MM-DD': 'text' },
  reflections: { 'YYYY-MM-DD': { presence, gratitude, tomorrow } },
  meditation:  { 'YYYY-MM-DD': minutesAsNumber },
  targetTime:  'HH:MM'
}
```

Storage is `localStorage` via `loadState()` / `saveState()`. `saveState()`
returns a boolean — **keep it that way**. Private windows and full disks both
throw on write, and the UI must not print "Saved ✓" over a failed write. All
four save paths go through `flash(el, ok)`, and the wake check-in rolls its own
entry back out of `state` if the write fails.

### Dates are local, never UTC

`dateStr(d)` builds `YYYY-MM-DD` from `getFullYear/getMonth/getDate`.

Do **not** replace this with `toISOString().slice(0,10)`. That returns the UTC
date, so a 4am check-in anywhere east of UTC lands on the previous day — in
India, Japan, and New Zealand every single amrit vela check-in was filed under
yesterday. An app about the hours before dawn has to use the dawn you're
standing in. `computeStreak()` walks backward with the same helper.

## Architecture (vanilla JS, no framework)

- `updateSky()` — reads the clock, picks one of 4 bands (night / vela / dawn /
  day), sets `data-band` on `<html>`, swaps the `#sky` gradient and the
  greeting copy. Runs on load and every 30s.
- `computeStreak()` — walks back day-by-day from today through `wakeLog`,
  comparing each logged time against `state.targetTime`; stops at the first gap
  or first late day.
- Simran timer — 1s `setInterval` over `sessionSeconds`; the breathing circle is
  pure CSS (`@keyframes breathe`, 8s), so it stays smooth regardless of the
  tick. Minutes are added to `state.meditation` on "Finish & log".
- `renderHistory()` — last 7 dates (union of intention + reflection keys),
  newest first. **All interpolated text goes through `esc()`** — it builds an
  `innerHTML` string, so an unescaped `<` in a reflection would silently eat the
  rest of the line.
- `render()` — the single "repaint everything from state" entry point.

## Colour: bands, not hardcoded values

Text and surfaces are driven by tokens that flip with `data-band`, so the same
markup stays readable against a 4am sky and a 1pm one:

```
--fg       body text          (cream on dark bands, --ink on light)
--fg-rgb   "245,240,230"      the same colour for rgba() borders/surfaces
--accent   numbers, dates     (--gold on dark; #8A5F17 on light — --gold
                              only reaches ~2.1:1 contrast on cream)
color-scheme                  so the native time picker follows the sky
```

Base palette: `--night #0D0E24`, `--vela #2B2F63`, `--gold #D4A24E`,
`--day #F5F0E6`, `--violet #7A6FA3`, `--ink #2A2740`.
Fonts: Fraunces (display), Inter (body), JetBrains Mono (clock, numbers).

**Never hardcode a text colour or a `rgba(245,240,230,…)` surface again** — use
the tokens, or the daytime view goes cream-on-cream and the evening reflection
becomes invisible (it was, until it was fixed).

The dawn gradient is deliberately all-light (`#E8C88F → #F5F0E6`). It used to
run dark-navy → gold, which no single text colour can sit on: dark ink drowned
in the navy at the top of the page, cream washed out on the gold at the bottom.
Keep any new gradient inside one luminance range.

Verified at 375px — nothing overflows, `.streak-box` and `.wake-row` wrap
cleanly. There is no mobile stylesheet and none is needed.

## Deliberately not built

Each of these was considered and set aside as more machinery than the aim
justifies. Don't add them without the user asking:

- **Sunrise/geolocation API** to compute a real amrit vela window. Adds a
  network dependency and a permission prompt to replace a fixed 3–6am band that
  already matches the traditional window.
- **Multi-device sync / any backend.** `localStorage` is per-browser, and a
  solo practice log doesn't need a server.
- **Tap-to-tally rep counter.** The breathing circle already holds the simran.
- **Data export.** Add it the day there's an actual reason to get the data out.
- **Push notifications / alarms.** The app is where you arrive once awake; it
  isn't trying to be the alarm clock.

## Conventions to keep

- Single HTML file, no build tooling. This was intentional.
- New persisted fields go inside the one `state` object under the one storage
  key — don't add keys.
- Spell it **"Waheguru"** everywhere — app copy, README, and these notes. The
  one exception is the quotation of the user's aim at the top of this file,
  which preserves their own wording verbatim.
- Don't add scripture quotations or specific Gurbani verses without the user's
  explicit direction. The app uses only "Waheguru" as a widely-used term,
  deliberately avoiding misattribution.
- Copy is plain, warm, and unhurried. No streak-shaming, no gamification, no
  exclamation marks.
