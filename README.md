# Marvel Ranker

One self-contained web app (`index.html`) that builds your definitive ranking of every Marvel film and show — 117 titles through July 2026, from *Howard the Duck* to *Spider-Man: Brand New Day* — through quick head-to-head matchups.

## How it works

Pick everything you've seen, optionally do a 10-second-per-title warm-up (Loved / Liked / Fine / Nah) that cuts matchups by about a third, then settle it in the arena: two posters, tap the better one. The engine uses binary insertion sort, so every pick is placed with transitive logic (if you ranked A over B and B over C, it never asks about A vs C) — a 60-title list takes roughly 300 matchups instead of 1,770 brute-force pairs. Progress autosaves in the browser after every tap, so you can close the tab and resume any time.

When you finish you get the full ranked list with podium, category filters (MCU films, MCU TV, Fox, Sony, Marvel Television, classics), search, and drag-to-reorder editing. Adding a title you watch later only takes a handful of matchups — it binary-searches into your existing list.

## Multiple lists

You can keep several rankings at once — say *MCU Movies*, *Full MCU*, and *The Total List* — with one-tap presets for the common ones. Lists are smart about each other: if a new list's titles are all covered by one you've already finished, its order derives instantly with zero matchups; if they overlap partially, a "head start" keeps your existing order as the backbone so you only rank the new titles. You never answer the same matchup twice. Each list shares, compares, and re-ranks independently, and older single-ranking saves migrate automatically.

## Sharing & comparing

"Copy share link" produces a URL with your entire ranking encoded in the fragment — no server, no accounts. A friend opening it sees the compare view: similarity score, biggest disagreements, where you agree, and both top 10s. Friends' rankings are saved locally so you can re-compare any time. There are also raw share codes (for texting) and full save export/import (for moving devices).

## Hosting

It's one file with zero dependencies. Options:

1. **GitHub Pages** (recommended): push this repo, then Settings → Pages → deploy from branch → root. Your app lives at `https://<user>.github.io/marvel-ranker/` and share links work out of the box.
2. **Netlify Drop / Vercel**: drag `index.html` in.
3. **Just send the file**: it works opened directly from disk, too.

## Updating the catalog

Titles live in the `CATALOG` array at the top of the script in `index.html`. To add new releases, **append to the end of the array** — never reorder or insert, because share codes and saves reference titles by index. Poster art hotlinks Wikipedia's poster images; any title without a working image gets a styled fallback card automatically.

The old Create React App prototype is preserved in `src/`.
