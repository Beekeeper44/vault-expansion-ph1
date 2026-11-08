# Mt Hood #3 Vault — Locations & Bins (prototype)

Static single-page app. No build step.

## Deploy
- Drag & drop: vercel.com/new → "Deploy" → drop this folder (or the zip contents).
- CLI: `npx vercel --prod` from this folder.
- GitHub: push this folder to a repo and import it in Vercel (Framework preset: Other, no build command, output = root).

Data is stored in each browser's localStorage. The camera scanner works on the Vercel domain (HTTPS).

## Nov 6, 2026 updates
- Sizes: Standard is fixed at 100 slots (blue); Custom is 1–100 or no cap (violet). Bins start as Standard 100.
- Rack size sets what fits: Small → S · Medium → S, M · Large → S, M, L · X-Large → all four. Standard racks have no limit.
- Spot-fit rule: a bin fits a spot its size or bigger. Standard spots take S, M, Standard (not L or XL).
- Locations keep their own size; a smaller bin shows its own size while it sits there and the spot reverts when it leaves.
- New locations are created empty (no bins). Empty spots show a dashed outline in their size colour.
- Clicking an empty location opens a "place a bin" pop-up with the required size.
- Locations tab: checkboxes, Column Min–Max range, Actions menu (Change size, on/off, scan in, remove, Print labels).
- Print labels (Locations and Bins Actions): one label per page, 6 × 1.5 in / 4 × 1.5 in.
- Off locations still change size in bulk edits and stay off; locations whose bin holds items are skipped.
See the PRD: https://arena-club.atlassian.net/wiki/spaces/AC/pages/1383989280
