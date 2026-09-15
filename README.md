# League HQ

A single-page fantasy football site for your Sleeper league, built to run entirely in the browser (no backend, no build step) — perfect for GitHub Pages.

It pulls live data straight from the public Sleeper API:
- **Standings** — current-season W-L-T, an **All-Play** record (what your record would be if you'd played every team every week — a good "luck" indicator), PF, PA, and an estimated **Max PF**, plus an **All-Time** toggle that adds up every season it can find. Click any column header to sort by it. A line marks the top-5 playoff cutoff (and the bottom 5, in leagues of 11+), and a prominent gold **★ Wild Card** tag flags the highest scorer sitting outside the top 5. Below the table, a **projected playoff bracket** seeds the top 5 by record plus that wild-card team as a 6-seed, with 1 and 2 getting byes to the semifinals (where 1 faces whichever surviving team ends up the lower seed), followed by an **On the Bubble** list showing exactly how many more points each non-playoff team needs to have scored to leapfrog the wild card.
- **Team pages** (click any team) — team logo, a week-by-week results log for the current season, head-to-head record against every other current team, and the full roster with player headshots.
- **Hall of Records** — split into **Regular Season** and **Postseason** sub-tabs (postseason is determined from each season's playoff start week on Sleeper), each as a scannable list with a large team logo so it's obvious at a glance who owns the record: most/fewest points in a game, biggest blowout, closest game, highest combined score, best single season, most wins/losses, longest win & loss streaks, biggest "bench blunder," most efficient manager, luckiest & unluckiest manager. The postseason tab also includes the league champions list.
- **Analytics** — a Points For vs. Points Against scatter plot with team logos as the markers (toggle between actual scoring and optimal/"max" scoring to strip out matchup luck and bad lineup decisions), a colorblind-friendly week-by-week position scoring heatmap (QB/RB/WR/TE/FLEX/K/DEF) that also shows each team's season average and an ▲/▼ indicator so you're not relying on color alone, and a position distribution chart for any position including FLEX.

It automatically walks the league's `previous_league_id` chain, so if this league has been renewed year over year on Sleeper, it'll pull in that whole history for the All-Time tab and records — no extra setup needed.

## Publish it on GitHub Pages

1. Create a new GitHub repository (or use an existing one).
2. Add `index.html` to the **root** of the repo (or to a `/docs` folder — just make sure it matches what you pick in step 4).
3. Commit and push.
4. In the repo, go to **Settings → Pages**, set **Source** to "Deploy from a branch," pick your branch (usually `main`) and the folder (`/root` or `/docs`), then save.
5. GitHub will give you a URL like `https://yourusername.github.io/your-repo/` — that's your live site. It can take a minute or two to go live the first time.

## Changing the league

Open `index.html`, find this near the top of the `<script>` block:

```js
var LEAGUE_ID = "1387553090483273728";
```

Swap in a different Sleeper league ID to point the site at another league.

## Notes

- Everything runs client-side against `api.sleeper.app` — each visitor's browser fetches the data directly, so there's nothing to host or maintain beyond the static file.
- The full NFL player list (~5MB) is cached in the visitor's browser for a day at a time so repeat visits load fast.
- "Optimal"/"Max PF" numbers are an estimate: the site takes each week's actual player scores and works out the best lineup your league's roster slots would've allowed. It's a good approximation, not an official Sleeper stat.
- The playoff bracket is a **projection built from current standings** (top 5 by record + highest scorer outside the top 5 as a 6-seed, with 1 and 2 getting byes) — it's not pulled from your league's actual playoff settings on Sleeper, since those vary league to league. If your league's real format is different, treat it as a "if the season ended today" snapshot rather than official seeding.
- Team logos prefer the custom per-league team logo a manager sets in Sleeper (`metadata.avatar`) over their personal account profile picture, falling back to the profile picture only if no custom team logo exists.
