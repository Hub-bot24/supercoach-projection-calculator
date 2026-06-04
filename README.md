# SuperCoach Intelligence Dossier

Premium-looking NRL SuperCoach projection report app.

## Files

- `index.html` — the GitHub Pages app.
- `data/players.json` — the player data feed the app loads.
- `scripts/update_supercoach_data.py` — updater script.
- `.github/workflows/update-supercoach-data.yml` — one-click / scheduled GitHub Action updater.

## How the data update works

Static GitHub Pages cannot safely scrape external websites from inside the browser because of CORS and browser restrictions.

So this setup uses a proper method:

1. GitHub Action runs `scripts/update_supercoach_data.py`.
2. The script pulls the NRL SuperCoach Stats 2026 player table.
3. It writes clean data to `data/players.json`.
4. The app button **Update SC Data** loads that JSON into the browser.

## One-click update from GitHub

Go to:

`Actions → Update SuperCoach data → Run workflow`

After it finishes, open the app and click:

`Update SC Data`

## Daily auto-update

The workflow also runs daily by schedule.

## Player images

The updater attempts to collect player image URLs from player profile pages. If it cannot find one, the app shows initials. That is better than fake images.

You can also add local images:

`images/players/payne-haas.png`

## Data rules

- SuperCoach positions are kept exactly from the source.
- Dual-position strings are preserved where the source supplies them.
- Price and BE are stored but not used to predict score.
- Projection logic protects against byes, DNPs and tiny-minute poison data.
