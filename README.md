# HDD Profile Studio

**Open the app:** https://ashuchaudhari58-cyber.github.io/HDD_profile_geometry_calculator/

A web app for designing **Horizontal Directional Drilling (HDD)** crossings. Share the link above with anyone. It runs in any modern browser on phone, tablet or desktop, needs no install or login, and does all calculation on the device.

## What it does

**Crossing types.** River, Road / Highway, Railway, Canal / Drain / Nala, or Open Ground. The input form and the profile drawing change to match the type (water and scoured bed, road on embankment, ballast and rails, lined canal).

**Setback from cover (river, canal, road, rail).** Give the obstacle width, the bed depth (plus side slope and scour) and the **minimum cover**. The app then works out:
- the design bottom elevation, and
- the **minimum entry and exit setback** from the bank / road edge at which the bore stays on or below the min-cover line under the banks and the bed.

Fix a setback yourself when the rig position is set by the site, and the cover check flags any shallow point.

**Basic page.** The 5-segment profile A→B→C→D→E→F (entry tangent, entry curve, bottom run, exit curve, exit tangent), a feasibility check, segment lengths, key dimensions, a cover check at the banks / toes / centre, node coordinates, a station–elevation table at any interval, and an AutoCAD `PLINE` point export.

**Advanced page (rod-by-rod).** The same inputs plus the rod length, and an optional first rod / tooling length. For every rod it gives:
- MD, pitch (% and °), inclination from vertical and Δ pitch per rod
- away distance, depth below entry, elevation and cover
- section and location

It also produces a drilling programme ("rod 11: entry curve starts, steer ≈ 1.09°/rod"), CSV download and AutoCAD export. You can **log as-drilled readings** (% pitch, ° pitch or ° inclination). They are computed by the average-angle method and compared against the plan, with an alarm when the bore goes off plan.

**Pipe page.** Pick the API 5L grade (A25 to X120, custom SMYS/SMTS, or non-steel), the OD (or an NPS quick pick), the wall thickness and the material density. It gives:
- weight per metre (kg/m, lb/ft, kN/m, plus the API 5L plain-end formula check), per joint and for the whole string
- ID, D/t, steel area, moment of inertia and section modulus
- internal, steel and displaced volumes (water to fill the string in m³ / bbl / US gal)
- buoyancy in the drilling fluid: empty and water-filled effective weight, and the water fill needed for neutral buoyancy
- Barlow burst and design pressure, tensile capacity at 90% SMYS, and bending stress at the design ROC

Optional coating is included. The string length defaults to the HDD length of your design, and "Copy spec" puts a text summary on the clipboard.

**Units page.** A universal converter covering length, area, volume, mass, force, pressure/stress, density/mud weight, pressure gradient, flow rate, speed, torque, energy, power, temperature, angle/slope (incl. % pitch and inclination), weight per length and viscosity. It has unit search, a swap button and an "all units" table.

**Checks page.** Minimum bend radius (1000 × OD × FOS), minimum cover (max of 5 × OD and 4.6 m) and steering per rod, each checked live against the design.

**Other features:**
- % or ° angle entry
- Light / Dark / High Contrast themes
- "Share this design" link that carries your inputs
- Print / save as PDF

## Verification

| Case | This app | Source sheet |
|---|---|---|
| θ 6°, H 6 m, R 900 m, TPD 1500 m | HDD length 1500.4564 | crossing_profile_geometry_calculator.xlsx: 1500.4564 |
| 10°/8°, R 3600, elev 47.1 / −30 / 44.6, 1900 horizontal | PC1 127.08, PT1 752.22, PC2 1117.46, PT2 1618.48, length 1909.54 | Automated HDD profile calc.xlsx: same |
| Degrees per 31.5 joint at R 3600 | 0.501° | Automated HDD profile calc.xlsx: 0.50134° |
| As-drilled 1 m @ 83° inc, then 9.55 m @ 82.89 / 82.94 / 82.91 | away / TVD 10.47 −1.29, 19.95 −2.47, 29.42 −3.65 | HDD_Pilot_Master_Sheet-Rev2.xlsx (average-angle): same |

## Files

- `index.html`: the whole app (HTML, CSS and JavaScript in one file)
- `sw.js`: network-first service worker (always serves the latest version and keeps a copy for use offline on site)
- `manifest.webmanifest`, `icons/`: install-to-home-screen support
- `BUILD-APK.md`: optional notes for wrapping the site as an Android app

## Updating the live site

The site is served by GitHub Pages from the `main` branch. Commit and push changes to `main`, and the link updates within a minute or two.

## Disclaimer

Planning aid only. The final design must be checked and approved by a qualified engineer.
