# Climate Change & Shallow Geothermal Potential in Germany

**M.Sc. Thesis Portfolio** · Karlsruhe Institute of Technology (KIT) · 2025-2026

**Author:** Vaibhav Jaiswal · M.Sc. Applied Geosciences

**Live site:** [vaibhavj97-thesis.vercel.app](https://vaibhavj97-thesis.vercel.app)

---

## Overview

This repository hosts the interactive web portfolio for my Master's thesis at KIT, which quantifies the impact of climate change on shallow geothermal energy potential across Germany. The work couples 8 CMIP6 global climate models with a semi-analytical borehole heat exchanger (BHE) model to map sustainable geothermal extraction rates at 5 km resolution under two future emissions scenarios.

The site is a static HTML, CSS, and vanilla JavaScript application with interactive Leaflet maps and JSON-backed climate datasets. No build step required.

## What's inside

- **Interactive map explorer** - 8 climate models × 2 scenarios × multiple layers, with switchable colormaps and toggleable layers
- **Methodology section** - the semi-analytical model coupling CMIP6 climate projections with finite line source (FLS) heat transport theory
- **Embedded GeoChat AI assistant** - ask questions about the thesis, grounded on the actual document
- **Cross-links** to BHE Recommender (an interactive feasibility tool built on this thesis data)

## Key methods

- **Climate input:** 8 CMIP6 GCMs (BCC, CanESM, GFDL, GISS, HadGEM, IPSL, MIROC, MPI), scenarios SSP 2-4.5 and SSP 5-8.5
- **Heat transport:** finite line source (FLS) method (Rivera 2017)
- **Solver:** Brent's root-finding method for maximum sustainable extraction rate
- **Constraint:** ground temperature minimum of -1.5 deg C, per SIA 384/6
- **Spatial resolution:** 5 km, processed in Google Earth Engine + Python
- **Time horizons:** 50-year depleting, 50-year sustainable, 100-year sustainable

## Key findings (preview)

- By 2100, subsurface warming of +1.7 deg C (SSP 2-4.5) to +3.1 deg C (SSP 5-8.5) is projected for Germany
- Mean sustainable extraction rate rises from 46.05 W/m to 47.39 W/m
- High-yield regions: southwestern Germany, Berlin, Munich, Frankfurt, Rhine-Ruhr
- Low-yield regions: northern and eastern Germany
- Climate warming reduces required drilling depth by roughly 4 m per 1 deg C

## Repository structure

```
.
├── index.html                      # main thesis portfolio page (self-contained)
├── data_json/                      # processed climate data for the maps
│   ├── meta.json                   # dataset metadata
│   ├── individual/                 # per-model JSON files (8 models × 2 scenarios)
│   │   └── {model}_{scenario}.json
│   └── ensemble/                   # ensemble-aggregated files (mean & median)
│       └── {scenario}_{stat}.json
├── files/                          # downloadable assets
│   └── Single_BHE_Analysis_GEE_CMIP6_Folium.ipynb
├── vercel.json                     # deployment config
└── README.md
```

## Running locally

This is a static site with no build step. Either:

```bash
# Option A: open directly
open index.html

# Option B: serve with any static server
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deployment

Auto-deployed via Vercel on every push to `main`.

## Related projects

- **[Personal portfolio](https://vaibhavj97.vercel.app)** - main portfolio site
- **[GeoChat](https://github.com/VaibhavJ97/geochat)** - AI assistant trained on this thesis
- **[BHE Recommender](https://github.com/VaibhavJ97/bhe-recommender)** - interactive feasibility tool using thesis data

## Contact

Vaibhav Jaiswal
M.Sc. Applied Geosciences · KIT · 2026

- Email: vaibhavjaiswal1234@gmail.com
- LinkedIn: [linkedin.com/in/vaibhavgeo](https://www.linkedin.com/in/vaibhavgeo/)
- Portfolio: [vaibhavj97.vercel.app](https://vaibhavj97.vercel.app)
