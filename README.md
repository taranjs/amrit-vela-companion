# Amrit Vela

A quiet companion for rising in *amrit vela* — the hours before dawn, held in
Sikh practice as the best time for simran, the remembrance of Waheguru.

It exists to help with one thing: **wake up early, and stay turned toward
Waheguru through the rest of the day.**

Four movements, in the order a day actually runs:

- **Wake check-in** — log the moment you're up. A streak forms when you rise at
  or before your target time.
- **Today's sankalp** — one intention to carry through the day.
- **Simran** — a breathing circle to sit with, and minutes logged when you're
  done.
- **Evening reflection** — four lines before sleep: where you noticed
  Waheguru's presence, what you're grateful for, what you'll do differently,
  and tomorrow's sankalp — which is waiting in the sankalp box when you rise.

- **Rest** — press *Sleeping now* when you put the day down. Joined to the next
  morning's check-in it gives you the night's length, and once a few mornings
  have gone well it works backward from your target wake time to suggest a
  bedtime — from your own nights, not from a generic number.

Press *I'm up* and the morning card opens: the sankalp you left waiting, and the
day's Hukamnama from Sri Darbar Sahib. On the last day of each month — or the
first day of the next, if you missed it — the month opens for a look back.

If a night gets away from you, the reflection isn't lost. Past midnight it still
knows you mean last night, and the `‹ ›` arrows step back up to a week to fill in
one you missed.

Your last 7 days sit at the bottom, expandable to 30. Nothing is ever deleted.

Keep a backup. Everything lives in this browser and nowhere else, so a cleared
browser would take it with it — *Save a backup* writes the lot to one JSON file,
and restoring only ever fills gaps, never overwrites a day you already have.

The page itself follows the sky, shifting through night, amrit vela, dawn, and
daylight as the hours pass.

## Running it

One file, no build step, no dependencies:

```
open index.html
```

Or serve the folder and visit it from your phone — that's where it's meant to
live.

## Your data

Everything stays in your browser's `localStorage` under a single key. There's
no account and no server. The app makes exactly one network request — asking
GurbaniNow for the day's Hukamnama, once a day — and it sends nothing with it.
No reflection, intention, wake time or sleep time has ever left your device.

The flip side is that your record is tied to one browser on one device, and
clearing your site data would clear it. That is what the backup file is for.

## Contributing

Read [CLAUDE.md](CLAUDE.md) first. It records the aim, the architecture, and —
just as importantly — the features deliberately left out. The restraint is the
design.
