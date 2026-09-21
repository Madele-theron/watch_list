# The Watch List

A personal movie & series watchlist — a single self-contained `index.html`
with no build step and no dependencies beyond two Google Fonts.

**Live:** https://madele-theron.github.io/watch_list/

## Features

- Genre filters, movie/series toggle, and search across title, cast, note and mood
- Star/pin picks, tick things off as watched, and note who recommended each one
- IMDb rating badges and a per-title YouTube trailer search link

## How state is stored

Watched / starred / recommended-by are saved to the browser's own
`localStorage` under the key `watchlist:state`. This is deliberate — there is
no backend and no database. State is per-device and does not sync.

## Adding or editing titles

Everything lives in the `DATA` array inside the `<script>` tag in
`index.html`. One object per title:

```js
{ t: "Title", genre: "drama", mood: "cosy", dur: "1h47",
  cast: "Actor, Actor", note: "One-line description.",
  plat: "Where to stream", sure: 0,      // 0|1 confidence in the platform guess
  rec: "Who recommended it",             // optional
  imdb: "8.5",                           // optional
  type: "series" }                       // omit for movies
```

`genre` must match a key in the `GENRE_LABELS` object just below `DATA` —
add a new key there when introducing a new genre.

Commit and push to the branch GitHub Pages serves; the site redeploys
automatically.

## Notes

- Streaming availability is best-effort for South Africa and goes stale —
  check [justwatch.com/za](https://www.justwatch.com/za) for the current home.
- Trailer links open a YouTube search for "<title> trailer" rather than one
  fixed video, so they survive takedowns and region locks.
