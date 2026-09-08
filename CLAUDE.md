# stock-alarm-charts

Static site (no build step) served via GitHub Pages from the `main` branch.

## Workflow

- `main` has no branch protection and no required reviews. Push changes
  directly to `main` (or open a PR and merge it immediately) without asking
  for confirmation each time — this has standing approval from the repo
  owner.
- Prefer small, direct commits to `main` for this repo unless the user asks
  for a review step.

## stock-alarm-bot

A separate automation (`stock-alarm-bot`, commits as `kyk0068@gmail.com`)
regenerates and force-overwrites these files directly on `main`, often
multiple times a day:
- `index.html`
- `sitemap.xml`
- `stock-*.html` (all tickers/languages)

Any hand-edit to those files (e.g. a new card on the homepage, a meta tag)
can be silently wiped by the bot's next run, since it rebuilds them from a
source outside this repo. After editing one of these files, it's worth
re-checking `main` a bit later to confirm the change survived. Files the
bot doesn't manage (e.g. `exchange-rate-*.html`, `guide.html`,
`robots.txt`) are safe from this.
