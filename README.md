# South Ridge Ballistics

A self-contained ballistics calculator that generates printable DOPE cards and BDC reticle cards for rifle shooting. Runs entirely in the browser — no install, no server, no dependencies, works offline once loaded.

## What it does

Enter your rifle, load, optic, and conditions, and it produces two field-ready cards:

- **DOPE card** — range, velocity, energy, drop, elevation (MIL or MOA), turret clicks, and wind hold for each distance. The classic "range → dial/hold" table.
- **BDC / reticle card** — the inverse lookup: for each reticle holdover mark, the range it actually hits with your load. Useful for mil-hash and BDC reticles, since a generic factory BDC chart is rarely right for your specific muzzle velocity and zero.

Both cards include a write-in **ACTUAL / NOTES** column so you can record true dope at the range and true the solution against real impacts.

## Features

- Point-mass trajectory solver using standard **G1 and G7** drag models
- **Factory load presets** for .22 LR, .223 Rem, 5.56 NATO, .22-250, .243 Win, 6.5 Creedmoor, .308 Win, .30-06 Springfield, and .300 Win Mag (SK, Lapua, RWS, Eley, Federal, Hornady, Nosler, Winchester, Remington, and more) — pick a load and the ballistic fields auto-fill
- Full **atmosphere model** (temperature, altitude, humidity) and **wind** by speed and clock direction with automatic crosswind value
- Switchable **MIL / MOA** turret units with matching click-value and clicks column
- Subsonic / transonic velocity flagging and trajectory summary (max ordinate, near zero, supersonic range)
- **Print**, **PNG download** (DOPE and BDC), and **profile save/load** via browser localStorage plus Export / Import JSON
- Adjustable card range (start / end / step) and BDC mark spacing / count

## Usage

Open the hosted page, fill in your rifle and load (or apply a factory preset), set your zero and conditions, and the cards update live. Use **Print** or **DOPE PNG / BDC PNG** to take a card to the range.

### Important

Computed dope is a **starting point**, not gospel. Factory muzzle velocities are usually from a 24" test barrel and your rifle will differ. Chronograph your actual load when possible, true the drops against real impacts at distance, and record results in the ACTUAL / NOTES column. Adjust muzzle velocity first, then ballistic coefficient (for far-range-only error), until predicted matches actual.

## Adding your own loads

Factory loads live in the `FACTORY_LOADS` object near the top of the script in `index.html`. Each entry is one line:

```js
{ name: "Your Load 55gr V-MAX", gr: 55, bc: 0.255, model: "G1", mv: 3240 }
```

Add an entry under the appropriate caliber, verify the numbers against the ammo box, and commit. No build step required.

## Hosting

This is a single static file (`index.html`). Any static host works — GitHub Pages, an internal web server, Netlify, etc. On GitHub Pages: put `index.html` in the repo root, enable Pages (Settings → Pages → deploy from `main`, root folder), and the site is live in a minute.

Saved profiles are stored per-browser and per-device (localStorage is tied to the page origin), so use **Export / Import JSON** to move a setup between devices.

## Notes on accuracy

- BC values for match .22 LR (~0.15 G1) are working estimates, not measured figures — expect to true them at distance.
- The BDC card assumes evenly spaced reticle marks (every X MIL / MOA). Unevenly marked commercial BDC reticles would need per-mark subtension entry.
- G1 suits flat-base and shorter-range bullets; G7 tracks long boat-tail match bullets better past ~400–500 yards. Use whichever the manufacturer publishes and don't mix them.

## License

Personal use. No warranty — verify all data against manufacturer sources and your own chronograph before relying on it.
