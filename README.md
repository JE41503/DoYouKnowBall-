[README (1).md](https://github.com/user-attachments/files/30727811/README.1.md)
# Think You Know Ball?

First of its kind, NFL and CFB crossover grid. A daily 3×3 puzzle crossing NFL teams
with college programs — name a player who fits both, before you run out of guesses.

## Files

- `index.html` — the entire game (markup, styles, logic)
- `data.json` — ~18,500 player records (college, NFL teams, years played, fame rating)
- `netlify.toml` — deployment config for Netlify

`index.html` loads `data.json` via a relative fetch, so **both files must stay in the
same folder** wherever this is deployed.

## Running locally

No build step, no dependencies. Just serve the folder over HTTP — you can't open
`index.html` directly via `file://` because the browser blocks the fetch to
`data.json` from a local file path. Easiest options:

```bash
# Python
python3 -m http.server 8000

# Node
npx serve .
```

Then visit `http://localhost:8000`.

## Deploying

### Netlify
1. Push this repo to GitHub.
2. In Netlify: **Add new site → Import an existing project → connect this repo.**
3. Build command: leave blank. Publish directory: `.` (repo root).
4. Deploy — `netlify.toml` already has this configured, so the defaults Netlify
   suggests should just work.

### GitHub Pages
Repo → Settings → Pages → Deploy from branch → select `main` / root. No build step
needed here either.

## How it works

- The puzzle is generated deterministically from the date, so everyone gets the same
  grid on a given day and it's replayable from the in-app archive picker.
- Three difficulty modes — Rookie, Pro, Hall of Fame — each generate a genuinely
  different grid, ranked by how many valid answers a cell has and how well-known those
  answers tend to be. Pro and Hall of Fame unlock via a real 3-day qualifying streak
  played in the tier below.
- All progress, stats, and streaks are stored in the browser's `localStorage` —
  there's currently no backend, so nothing is shared across devices or users yet.
  Cross-user rarity data and real leaderboards would require adding one later.
