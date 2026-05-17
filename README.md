# Master Thesis Project - Climate Change and Geothermal Potential in Germany

> Interactive web maps of climate-projected shallow geothermal heat-extraction rates across Germany, coupling CMIP6 climate projections with borehole heat exchanger physics.

**Live**: [vaibhavj97-thesis.vercel.app](https://vaibhavj97-thesis.vercel.app)

## What this is

The thesis page is a live interactive companion to my M.Sc. thesis at the Karlsruhe Institute of Technology. It renders 5 km gridded data over Germany showing sustainable heat-extraction rates under two climate scenarios (SSP 2-4.5 and SSP 5-8.5) and three time horizons (50 years, 100 years depleting, 100 years sustainable).

## Thesis info

- **Title**: Impact of Climate Change on the Geothermal Potential of Closed Systems Using GIS and Python
- **Author**: Vaibhav Jaiswal
- **Institution**: Karlsruhe Institute of Technology (KIT), M.Sc. Applied Geosciences
- **Graduated**: February 2026
- **Grade**: 2,5
- **Supervisors**: PD Dr. Kathrin Menberg, Dr. Susanne Benz

## How this was built - AI-pair-programming disclosure

This project was built with **AI-assisted development workflows** at every stage:

**Python notebook (data pipeline + scientific modeling)**: ChatGPT and Anthropic Claude were my pair-programmers for code structure, numerical methods (Brent's method via scipy.optimize), data engineering, and refactoring. The MATLAB-to-Python migration, the JSON export pipeline, and the iteration over 24 output files were all AI-accelerated.

**Web app (interactive maps + chatbot integration)**: Claude was the primary collaborator for the Leaflet.js map rendering, custom canvas optimization for 5 km grid performance, and the JSON pipeline architecture.

**What was mine**: the thesis research question, methodology choices (MFLS coupling, SIA 384/6 standard, parameter selection), the supervisor-guided scientific interpretation, every architecture decision, every line review, and the final deployment.

**What AI accelerated**: code generation, debugging, refactoring, documentation, and "what's the cleanest way to do X" iteration.

The thesis itself was written by me. The supporting tools were built with AI as a pair-programmer.

## Tech stack

| Layer | What |
|---|---|
| Map rendering | Leaflet.js + chroma-js for color scales |
| Frontend | Vanilla HTML, CSS, JavaScript (no framework) |
| Data | 24 pre-computed JSON files (~373 KB total) exported from a Jupyter notebook |
| Source data | Google Earth Engine for CMIP6, MFLS solver in Python |
| Notebook stack | Python (scipy.optimize, numpy, pandas, geopandas, rasterio, folium) |
| Hosting | Vercel |
| Development | AI-pair-programming (Claude, ChatGPT, Copilot) with full manual review |

## Architecture

```
Jupyter notebook (offline)
  ├── Pull CMIP6 climate data from Google Earth Engine
  ├── Run MFLS solver (scipy.optimize.brentq) for each 5 km pixel
  ├── For each pixel × scenario × time horizon → maximum sustainable q
  └── Export 24 JSON files (~373 KB total)
        ↓
Static web page (browser only, no backend)
  ├── Fetch JSON for current selection
  ├── Render each pixel via chroma-js color scale onto canvas
  ├── Overlay canvas on Leaflet map with pixel-perfect rendering
  └── Click events query the underlying array and show exact value
        ↓
Embedded GeoChat widget
  └── iframe → vaibhavj97-geochat.vercel.app (separate repo)
```

## How it works

1. The Jupyter notebook runs the **Moving Finite Line Source (MFLS)** model from Rivera et al. (2017), coupling 8 CMIP6 GCMs (BCC, CanESM, GFDL, GISS, HadGEM, IPSL, MIROC, MPI) with standard BHE parameters (150 m depth, lambda = 2.5 W/m.K, Rtb = 0.15 m.K/W, Tmin = -1.5 deg C per SIA 384/6).
2. For every 5 km pixel in Germany, Brent's method finds the maximum extraction rate that keeps fluid temperature above the -1.5 deg C threshold over 50, 100, and 100-year sustainable horizons.
3. Output is exported as 24 JSON files (16 individual GCM results + 8 ensemble files).
4. The web page renders these files as toggleable Leaflet overlays with custom canvas rendering for performance.

## Features

- Hero with thesis abstract
- Cite this work box (APA and BibTeX with copy buttons)
- Key findings with quantitative numbers
- Methods overview
- Interactive map explorer with 6 toggleable layers and a fullscreen mode
- AI Projects banner (links to GeoChat and BHE Recommender)
- Behind the scenes section (how the page itself was built)
- Floating GeoChat widget (embedded chatbot in iframe)

## Key findings

- Mean heat extraction rate in Germany: **26.97 W/m** (SSP 2-4.5, 50-year) rising to **47.39 W/m** (SSP 5-8.5, 100-year sustainable)
- Subsurface warming projection by 2100: **+1.7 deg C** (SSP 2-4.5) to **+3.1 deg C** (SSP 5-8.5)
- Climate change provides a modest **1-3% increase** in BHE output on top of geological factors
- Sustainable 100-year operation provides much bigger gains (**+20-35%**) than climate change alone
- High-yield regions: southwestern Germany, Berlin, Munich, Frankfurt, Rhine-Ruhr metropolitan area
- Each 1 deg C of additional ground warming reduces required borehole depth by roughly **4 m** for the same heating capacity

## Citations and references

If you reference this work, please cite the thesis:

```
Jaiswal, V. (2026). Impact of Climate Change on the Geothermal Potential of
Closed Systems Using GIS and Python. M.Sc. Thesis, Karlsruhe Institute of
Technology, Germany. Supervisors: PD Dr. Kathrin Menberg, Dr. Susanne Benz.
```

BibTeX is also available on the live site under "Cite this work".

**Underlying methods and standards referenced in the thesis**:

- Rivera, J. A., Blum, P., & Bayer, P. (2017). *Increased ground temperatures in urban areas: Estimation of the technical geothermal potential.* Renewable Energy, 103, 388-400.
- SIA 384/6 (Swiss Society of Engineers and Architects): Standard for ground-source heat exchanger systems. Minimum fluid temperature constraint Tmin = -1.5 deg C.
- CMIP6 (Coupled Model Intercomparison Project Phase 6): 8 General Circulation Models accessed via Google Earth Engine. Scenarios SSP 2-4.5 and SSP 5-8.5.

## Run locally

```bash
git clone https://github.com/VaibhavJ97/kit-master-thesis-portfolio.git
cd kit-master-thesis-portfolio
python3 -m http.server 8000
# Open http://localhost:8000
```

To re-run the Python notebook (`Single_BHE_Analysis_GEE_CMIP6_Folium.ipynb`), you'll need a Google Earth Engine account and Python 3.9+ with: `numpy`, `scipy`, `pandas`, `geopandas`, `rasterio`, `folium`, `earthengine-api`.

## Project structure

```
.
├── index.html                              # Main thesis page
├── map-fullscreen.html                     # Standalone fullscreen map explorer
├── og-preview.png                          # 1200x630 social-media preview
├── assets/
│   ├── style.css                           # Styles
│   └── map-app.js                          # Leaflet + canvas rendering
├── data/
│   ├── *_individual.json (16 files)        # Per-GCM × per-scenario results
│   └── *_ensemble.json (8 files)           # Ensemble mean / median statistics
├── files/
│   └── Single_BHE_Analysis_*.ipynb         # Source Jupyter notebook
└── README.md
```

## Limitations

- Single BHE only, no borehole field interaction modeled
- Uniform soil thermal properties (lambda held constant at 2.5 W/m.K), real geology varies
- Groundwater advection neglected, real groundwater flow can add 10-20% to yield
- Surface heat flux modeled uniformly, local microclimates and shading not included
- No heat-pump system modeling, only the ground side

See the thesis PDF for full details.

## Disclaimer

This work is research output, not engineering design. The numbers reflect ensemble-averaged climate projections at 5 km resolution and standard BHE parameters. Real-world borehole design must consider local geology, groundwater flow, regulatory permits, contractor pricing, and equipment specifications. Treat results as a first-pass screening estimate, not a substitute for site-specific engineering analysis. CMIP6 climate projections carry inherent uncertainty; SSP scenarios are pathways, not predictions.

## License

MIT for the code. Data follows CMIP6 fair-use terms. Thesis itself is the intellectual property of the author and the Karlsruhe Institute of Technology.

## About me / Contact

- **Email**: vaibhavjaiswal1234@gmail.com
- **Portfolio**: [vaibhavj97.vercel.app](https://vaibhavj97.vercel.app)
- **LinkedIn**: [linkedin.com/in/vaibhavgeo](https://www.linkedin.com/in/vaibhavgeo/)
- **GitHub**: [github.com/VaibhavJ97](https://github.com/VaibhavJ97)
- **Book a 30-min call**: [calendly.com/vaibhavjaiswal1234/30min](https://calendly.com/vaibhavjaiswal1234/30min)
- **Location**: Karlsruhe, Germany

### My other repos

- [Portfolio homepage](https://github.com/VaibhavJ97/VaibhavJ97.github.io) - the front door
- [GeoChat](https://github.com/VaibhavJ97/geochat) - AI chatbot grounded in this thesis
- [BHE Recommender](https://github.com/VaibhavJ97/bhe-recommender) - interactive feasibility tool built on this thesis data
