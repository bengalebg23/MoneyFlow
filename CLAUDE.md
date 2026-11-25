# Money Flow

Per-year Sankey diagrams of the household finances (SankeyMATIC / r/FIREUK style), built from the "2026 Finances" spreadsheet and bank statements. D3 7.9.0 + d3-sankey 0.12.3 + SheetJS 0.18.5.

Live: https://bengalebg23.github.io/MoneyFlow/

## How Ben works
- Ben works from his phone. He asks for changes in chat and Claude pushes them straight to the deploy branch. There's no local build and no pull-request review.
- Pushing to `main` deploys via GitHub Pages within a minute or two.
- The repo is **public**. Never commit secrets, API keys meant to stay private, family photos or personal data.

## Every release
- Bump `APP_VERSION` and the `<title>` in `index.html` and `CACHE` in `sw.js` together.
- Keep `HANDOFF.md` up to date (version, what changed, open threads) if the repo has one.
- After pushing, give Ben the live URL and the new version number so he can check it on his phone.

## Code rules
- Single-file app: keep HTML, CSS and JS in `index.html`. No build step, bundler or npm packages.
- Pin exact CDN versions (no `@latest` or floating majors). A floating Babel major broke an app before.
- Self-review before pushing: duplicate `const`/`let` in one scope, variable shadowing inside loops, unclosed template literals, undefined references.
- Defer re-renders triggered inside click handlers with `setTimeout(..., 0)` to avoid detached-node bugs from bubbled events.
- Don't swallow Firebase errors with a bare `console.warn`. Surface them so permission problems are visible.
- UK English in all user-facing text.

## This app
- Data rules: bank statements are the source of truth. The spreadsheet fills gaps only. Highlight anything that doesn't reconcile rather than guessing.
- Extra MIRA payments beyond salary are expense reimbursements that cancel a matching expense. Ask when the match isn't clear. "MIRA" spending means the Thomas Franks canteen only.
- Account closures (eToro, NatWest Invest 3) are money moved or withdrawn, not income into Invest 5.
- Chart behaviour Ben wants kept: opens zoomed out with small labels, zoom/pan for detail, labels drawn on their blocks (key only for blocks too small), and tapping an item shows a year-by-year comparison with the item moved to the top of each stack.
- The repo is public, so keep personal financial data out of committed files unless Ben has explicitly chosen to include it.
