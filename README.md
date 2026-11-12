# Arena Club Admin — Scan & Revault Prototype

Single-file static prototype. No build step, no dependencies.

    public/index.html   the whole app
    vercel.json         static config

## Deploy

**Drag and drop:** zip the `arena-scan-prototype` folder and drop it on
https://vercel.com/new — Vercel serves `public/` automatically.

**CLI:**

    npm i -g vercel
    cd arena-scan-prototype
    vercel          # preview
    vercel --prod   # production

**Git:** push the folder to a repo and import it on Vercel. Framework preset
"Other", build command empty, output directory `public`.

## What's in it

- Home page. Operations and Vaulting are the working nav menus; the rest are greyed out.
- **Operations › Scan** — Pending Scan with Scan / Rescan / Hardware tabs.
  Clicking a BOXES button opens the scan station: scanner-station picker, per-scanner
  Scan and Load, green sweep animation, card images landing one per second, positions
  you can clear and rescan front or back, and the card table flipping to Pending Grading.
- **Hardware tab** — only when the Hardware skill is green on the grader page.
  Station setup (one user per station, add/remove stations) and Hardware setup
  (drag V600 / Fuji / printers between the shelf and stations).
- **Vaulting › Revault** — only when the Revault skill is green. Scan cards for the
  storage and shipping bin, live QR reading through the camera, bin contents with slot
  ordering, and Revault / Data Issue / Customer Support dialogs. The demo panel
  bottom-left has bins, cards and a reset.
- **Graders** — searchable list, per-grader skill grid; Hardware and Revault gate the
  pages above.

State lives in the browser's localStorage under `ac-admin-proto-v6`. Bump that key in
the source to reset everyone's saved state after a data change.

## Editing the data

Near the top of the script block:

- `STATIONS` — the station map: scanners and printer per station.
- `SPARE` — hardware sitting on the shelf.
- `GRADERS` — the team.
- `hwType()` — naming rules: `Fuji *` is Fuji, `FJ *` is a printer, else V600.
- `stationUsers()` — which user starts on which station.
- `binItems()` — the bin contents list; `RV` inside `cardDialog` — the revault demo cards.

## Camera

The Revault page uses `getUserMedia` plus jsQR to read bin labels. It needs https and
a permission prompt, so it works on the deployed Vercel URL; sandboxed preview frames
usually block it. The Demo buttons cover the same flow without the camera.

## Changes (Nov 2026)

- **Routing:** internal routes like `#/retrieval/mthood` are mirrored to the address bar as plain names (`#retrieval--mthood`) so the page works when hosted as a claude.ai artifact. `go()` works the same as before.
- **Light mode pinned** (`color-scheme: light`) so a dark-mode viewer doesn't restyle inputs.
- **Mt Hood has no card images.** Its retrieval queue is watches, wallets and comics:
  - `MH_WATCHES`, `MH_WALLETS`, `MH_COMICS` hold `{name, img, back}` (fronts are real photos, backs are drawn stand-ins).
  - Category filter: ALL / WATCHES / WALLETS / COMICS.
  - Each row shows type and item name under the number.
- **Location column** (Mt Hood only) between Number and Bin: `A#, B#, C#, D#` = Aisle, Bay, Column, Deck. Dummy, stable per bin; limits in `MH_MAX` (aisle 8, bay 4, column 32, deck 10). Sortable.
- **Bin sizes** (`BIN_SIZES`): Standard 100, Custom, Small 6, Medium 3, Large 2, X-Large 1.
  - `MH_KIND_BIN`: watches and wallets in Small (6), comics in Custom (10 for testing).
  - Every bin has its own barcode: `MH` + size letter + bin number, e.g. `MHS-00668`. Drawn as Code 128 with JsBarcode; scanning it loads the bin.
  - Shipping bin shows size, fill count, barcode and one box per slot. A full bin, or the wrong bin size for an item, blocks the scan.
- Stale saved queues (item numbers that no longer exist) refill automatically.

## Changes (Nov 11, 2026, later)

- Alan's Mt Hood #3 Locations & Tins app is built in (Vaulting › Vaults). It's stored compressed inside `index.html`, so there are no extra files.
- Retrieval and Bay Setup read its layout (real aisles, bays, columns, decks and tin numbers).
- Phase 1 / Phase 2 toggle in the top bar; Operations greyed out.
- Order # search, VIP retrieval banner, × to remove the current shipping bin, Complete Bin at the bottom, no slot cap on shipping bins.
- `vercel.json` now sends `Permissions-Policy: camera=(self)` so the camera works on the Vercel domain.

## Changes (Nov 12, 2026)

- Mt Hood shipping station holds 3 bins: tab 1 is always Items; tabs 2 and 3 get one or more item types (Watches, Wallets, Comics, Cards, Coins) once a bin is loaded. Tabs use the item-type colors; several types split the tab.
- Scanning an item jumps to the bin set up for its type and the confirm dialog shows the suggestion. Comics and cards can't go in Items: with no bin for them, a prompt asks to set one up.
- Removing a bin (×) clears its type. Bin slots are one item each and grow as you pick (no cap).
- Type column in the Mt Hood queue; Card and Coin demo items; demo item buttons never grey out (each press adds a copy).
- Vaulting › Vaults opens Alan's Mt Hood #3 Locations & Tins app (built in); retrieval and Bay Setup use its real layout.
