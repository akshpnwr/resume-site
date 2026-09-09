# resume.akashpanwar.dev

The resume site — a hiring-focused counterpart to the portfolio at
[akashpanwar.dev](https://akashpanwar.dev), which is aimed at freelance client
acquisition. This one is what gets sent to hiring managers and recruiters.

Plain static HTML and CSS. No build step, no dependencies, no JavaScript.

```
index.html      the page
styles.css      its styles
resume.pdf      downloadable resume, linked from the hero
assets/         project screenshots
robots.txt      indexable
sitemap.xml
```

## Local preview

```sh
python -m http.server 8000
# then open http://localhost:8000
```

## Deploying

Hosted on Vercel as its own project, serving `resume.akashpanwar.dev`. Pushing
to `master` deploys. There is no `vercel.json` — the repo root is the site
root, so no routing configuration is needed.

## Why this is a separate repo

It began inside the portfolio repo, served at a subdomain via host-based
rewrites in `vercel.json`. Those rewrites never fired: the subdomain kept
serving the portfolio site with a 200. Two configurations that matched Vercel's
own documentation (`rewrites` with `has: host`, and the lower-level `routes`)
both failed to match the host on that project, while the files themselves
deployed correctly — `/resume-site/README.md` was reachable, but
`resume.akashpanwar.dev/styles.css` still returned the portfolio's CSS.

A separate repo and a separate Vercel project removes host matching from the
picture entirely. The maintenance cost is low because the two sites share no
code — separate HTML, separate CSS, no JS. Only `resume.pdf` and the six
project screenshots are duplicated, and those rarely change.

## Keeping content in sync

When a project screenshot or the PDF changes in the portfolio repo, copy it
here too. Nothing else is shared.

## Accessibility

The page was checked with axe-core against WCAG 2.1 A and AA in both light and
dark mode, with zero violations. Worth re-checking if the palette changes:
`--text-faint` and the "Live" badge green were both tuned specifically to clear
the 4.5:1 contrast threshold, and the dark-mode primary button uses dark ink
(`--on-accent`) because white text on the lighter dark-mode accent fails.
