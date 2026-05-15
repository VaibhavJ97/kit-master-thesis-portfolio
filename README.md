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
- **Grade**: 2.5
- **Supervisors**: PD Dr. Kathrin Menberg, Dr. Susanne Benz

## Tech stack

| Layer | What |
|---|---|
| Map rendering | Leaflet.js + chroma-js for color scales |
| Frontend | Vanilla HTML, CSS, JavaScript (no framework) |
| Data | 24 pre-computed JSON files (~373 KB total) exported from a Jupyter notebook |
| Source data | Google Earth Engine for CMIP6, MFLS solver in Python |
| Hosting | Vercel |

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

## Run locally

```bash
git clone https://github.com/VaibhavJ97/kit-master-thesis-portfolio.git
cd kit-master-thesis-portfolio
python3 -m http.server 8000
# Open http://localhost:8000
```

## Limitations

- Single BHE only, no borehole field interaction modeled
- Uniform soil thermal properties (lambda held constant at 2.5 W/m.K), real geology varies
- Groundwater advection neglected, real groundwater flow can add 10-20% to yield
- Surface heat flux modeled uniformly, local microclimates and shading not included
- No heat-pump system modeling, only the ground side

See the thesis PDF for full details.

## License

MIT for the code. Data follows CMIP6 fair-use terms.

## About me

[Portfolio](https://vaibhavj97.vercel.app) · [GitHub profile](https://github.com/VaibhavJ97) · [LinkedIn](https://www.linkedin.com/in/vaibhavgeo/) · [Email](mailto:vaibhavjaiswal1234@gmail.com)
