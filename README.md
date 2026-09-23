# HDD Profile Studio

An **offline** calculator for **Horizontal Directional Drilling (HDD)** crossing profiles. It reproduces the geometry from your `crossing_profile_geometry_calculator.xlsx` — segment lengths, node coordinates, depths, total pipe length — and tells you at a glance whether a profile is **feasible**. It also checks your design against two common HDD rules of thumb: minimum bend radius and minimum cover depth.

Built as a self-contained Progressive Web App: one folder, no internet, no install server required. See **[BUILD-APK.md](BUILD-APK.md)** to put it on your phone or package it as an `.apk`.

## What it does

- **5-segment profile model** A→B→C→D→E→F: entry tangent, entry curve, horizontal bottom, exit curve, exit tangent.
- **Separate entry / exit radii** (R1, R2) — not just a single shared ROC.
- **Live profile diagram** with ground surface, curves vs. tangents, depth grid, node markers and automatic vertical exaggeration.
- **Feasibility check** — flags any section that goes negative and tells you *why* and *by how much* (e.g. minimum plan distance or minimum entry depth required).
- **Setting-out table** — chainage X and depth for every node A–F.
- **Checks tab**: minimum bend radius (R ≥ 1000 × OD × FOS, with your Profile tab's R1/R2 checked against it) and minimum cover depth (≥ 5 × OD, floored at 4.6 m, checked against your entry/exit depths), each with a short citation.
- **Light / dark theme toggle**, remembered per device.
- Inputs are remembered on-device between sessions.

## Inputs (metric, matching the spreadsheet)

| Input | Symbol | Unit |
|---|---|---|
| Entry angle | θ1 | ° |
| Exit angle | θ2 | ° |
| Entry depth to bore | H1 | m |
| Exit depth to bore | H2 | m |
| Entry radius of curvature | R1 | m |
| Exit radius of curvature | R2 | m |
| Total plan distance | TPD | m |

## Verification

The engine matches the source spreadsheet exactly. Example (θ=6°, H=6 m, R=900 m, TPD=1500 m):

| Section | This app | Spreadsheet |
|---|---|---|
| AB entry tangent | 10.2336 | 10.2336 |
| BC entry curve | 94.2478 | 94.2478 |
| CD bottom run | 1291.4936 | 1291.4936 |
| DE exit curve | 94.2478 | 94.2478 |
| EF exit tangent | 10.2336 | 10.2336 |
| **AF HDD length** | **1500.4564** | **1500.4564** |

## Roadmap

- **v1 (this):** geometry / profile module.
- **v2 (planned):** structural design module porting `Design Calculation.xlsx` — pull force, hoop / longitudinal / bending / combined stresses, collapse & overburden, coating check, roller spacing, ROC limits, rig-capacity checks (ASME B31.4).

## License / privacy

Runs entirely on your device. No network calls, no analytics, no data collection.
