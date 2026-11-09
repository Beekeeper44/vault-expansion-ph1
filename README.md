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
- New locations are created empty (no bins). Adding a location or aisle asks for the rack type: 6 or 8 bins per level, or a custom number (1–30); 10 levels. Empty spots show a dashed outline in their size colour.
- Clicking an empty location opens a "place a bin" pop-up with the required size.
- Locations tab: checkboxes, Column Min–Max range, Actions menu (Change size, on/off, scan in, remove, Print labels).
- Print labels (Locations and Bins Actions): one label per page, 6 × 1.5 in / 4 × 1.5 in.
- Off locations still change size in bulk edits and stay off; locations whose bin holds items are skipped.
See the PRD: https://arena-club.atlassian.net/wiki/spaces/AC/pages/1383989280
- Bin numbers run aisle by aisle, odd rack then the even rack facing it (Columns 1–11 = #1–60, Columns 2–12 = #61–120).
- Create bins (Bins tab): next numbers in order, Storage or Shipping (Ship #1, #2…), optional label print. Shipping bins never go on a shelf.
- Bins list: Type and Printed columns, Bin Type and Printed filters; printing marks labels as printed.
- Rack cards: Print location labels / Print bins; aisle header: Print location barcodes.
- Actions opens as a side panel; Turn on / Turn off / Remove ask to confirm and list the bins and locations first.
- Enter closes the bin pop-up, like Esc.
- Bin history: 🕘 History in the bin pop-up lists every item in / out, every slot taken / cleared, and every time the bin was placed, moved or taken off a shelf, with who and when.
- Location history: 📍 Location history (in the bin history and the empty-location pop-up) lists every bin that arrived or left, plus item and slot changes while a bin sat there.
- Locations Actions opens as a side panel (like Bins). "Change location size…" sets the size of the spots themselves; a smaller bin already there stays, bigger bins are skipped and listed in a red pop-up.
- A bin that won't fit where it's scanned shows a red "Bin won't fit here" pop-up with its size and what the location takes.
- Phase 1 / Phase 2 toggle (top bar). Phase 1: a bin only goes in a spot of its own size. Phase 2: Small fits every spot; Medium → M, L, XL, Standard; Large → L, XL; X-Large → XL only.
- Add location and Create aisle also ask for Levels (1–10): e.g. 8 bins across × 5 levels = 40 spots. Only the built levels show and count.
- Scanning a bin into a filled location only bumps the bin there if it is empty; if it holds even one item, a red "A bin is already in this location" pop-up shows and nothing moves.
- Item sizes: an item fits a bin its size or bigger (Small → S, M, L, XL · Medium → M, L, XL · Large → L, XL · X-Large → XL only); Standard items go in Standard/Custom bins. Store item offers same-size bins first, then the next size up. Scanning a known-size item into a bin that is too small shows a red pop-up.
- Standard bins fit Medium, Large and X-Large spots and racks (Phase 2).
- Phase 2 shared spots: several smaller bins can share one location if they fit. Space in Small-units: Small 1, Medium 2, Large 4, X-Large 8, Standard 2 (a Large spot holds 4 Smalls, an XL spot 8). Grid shows "#2 +3"; the bin pop-up lists the shared bins; when the main bin leaves the next one takes its place. Phase 1 keeps one bin per location.
- Off locations take nothing: scanning or moving a bin into an off location (or storing an item there) shows a red "This location is off" pop-up and nothing moves.
- Any aisle or location (original or added) can be deleted as long as nothing in it holds an item. If even one item is stored, a red pop-up lists where and in which bins, and nothing is deleted.
