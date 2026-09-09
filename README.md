# Fantasy League Standings

A single-page site that pulls live standings from the Sleeper API. No build step, no dependencies — it's one HTML file.

Your league ID (`1387553090483273728`) is already wired in, so it's ready to deploy as-is.

## Deploy to GitHub Pages

1. Create a new repository on GitHub (public repos get free Pages hosting).
2. Upload `index.html` to the repository (drag-and-drop on the GitHub website works, or `git add`, `git commit`, `git push` from the command line).
3. In the repository, go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to "Deploy from a branch," pick the `main` branch and the `/ (root)` folder, then save.
5. GitHub gives you a URL like `https://your-username.github.io/your-repo-name/` — that's your live site. It can take a minute or two to go live the first time.

## Changing the league later

If you ever start a new league (new season, new league ID), open `index.html`, find this line near the top of the `<script>` section, and swap in the new ID:

```js
const LEAGUE_ID = "1387553090483273728";
```

## What it shows right now

Just standings: rank, team, record, points for, points against, and point differential — sorted by wins, then points scored. The page re-fetches from Sleeper every time someone loads it, so it's always current.

Good next additions once you want them: weekly matchups/scoreboard, power rankings, draft recap, or a transactions feed — all doable from the same Sleeper API.
