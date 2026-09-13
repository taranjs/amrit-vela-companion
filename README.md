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

If a night gets away from you, the reflection isn't lost. Past midnight it still
knows you mean last night, and the `‹ ›` arrows step back up to a week to fill in
one you missed.

Your last 7 days sit at the bottom, expandable to 30. Nothing is ever deleted.

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

Everything stays in your browser's `localStorage` under a single key. Nothing
is uploaded, there's no account, and no server ever sees a word of it. The
flip side: it's tied to one browser on one device, and clearing your site data
clears your history with it.

## Contributing

Read [CLAUDE.md](CLAUDE.md) first. It records the aim, the architecture, and —
just as importantly — the features deliberately left out. The restraint is the
design.
