# UEFA European Championship League Ledger

**Site will be live at:** <https://ecclubtracker.com/>

Every UEFA European Championship goal, assist and save, credited back to the **club league** the player earns his living in. Live tracking for **EURO 2024/2028-style updates**, plus settled ledgers for **2020, 2016, 2012 and 2008** — the last five tournaments.

Sort by Premier League, La Liga, Bundesliga, Serie A, Ligue 1, Eredivisie, Primeira Liga, Süper Lig, and more. Tap any league row to see exactly which players (and clubs) delivered.

## Files

- `index.html` — the single-page app (vanilla JS, no build step)
- `data/2026.json` — the live ledger payload. The page polls this file every 60s. Schema: `{updated, goals[], assists[], saves[], notes{}}`, each stat an array of `{league, total, players:[{name, nat, n, club}]}`.
- `data/players-2026.json` — index of tournament players, mapping the competition player ID to `{name, nat, club, clubnat}`. Seeded from the competition's squad endpoints joined with public club data.
- `data/leagues.json` — club-country → league-name defaults, plus per-club overrides for second-tier and unusual cases.
- `scripts/build_ledger.py` — hourly aggregator. Reads the competition timeline feed, joins on the player index, buckets into leagues, writes the ledger payload. No secrets — public sources only.
- `scripts/seed_players.py` — rebuilds the player index. Run once and after each transfer window.
- `.github/workflows/update-euro.yml` — runs the builder every hour and commits the updated ledger payload back to `main` when it changes.
- `robots.txt`, `sitemap.xml` — SEO basics
- `world-cup-league-tracker.html` — original prototype, kept for history while the Euro version is being reshaped
- `poll-worker/` — optional Cloudflare Worker that aggregates the predictions poll.

## Hosting

GitHub Pages — set `Settings → Pages → Source` to `main / (root)`. The site is served from `index.html`.

## Contributing

Corrections welcome — especially for the historical tournaments, which list confirmed top contributors per league but aren't fully exhaustive. Open an issue or PR with a source link.

## License

MIT — see source. Not affiliated with UEFA.
