# Master Thesis - Climate Change & Shallow Geothermal Potential in Germany

> A semi-analytical model coupling CMIP6 climate projections with borehole heat exchanger physics, quantifying how a warming subsurface reshapes Germany's renewable heating potential through 2100. M.Sc. Applied Geosciences at KIT, 2026.

**Live site:** [vaibhavj97-thesis.vercel.app](https://vaibhavj97-thesis.vercel.app)
**Fullscreen map explorer:** [vaibhavj97-thesis.vercel.app/map-fullscreen.html](https://vaibhavj97-thesis.vercel.app/map-fullscreen.html)

---

## About this repo

This is the web companion to my Master's thesis at Karlsruhe Institute of Technology (KIT), submitted February 2026. The site presents:

- The thesis abstract and methodology
- Four key findings (climate-driven subsurface warming, geothermal yield gains)
- A four-step methodology workflow
- A live, interactive map explorer with every result map from the thesis
- A floating AI assistant ([GeoChat](https://vaibhavj97-geochat.vercel.app)) for thesis Q&A
- A standalone fullscreen map page
- The original Jupyter notebook for download

## Key findings

- **+1.7 °C** mean shallow ground warming by 2100 under SSP 2-4.5
- **+3.1 °C** under SSP 5-8.5
- **+8 to +24 %** increase in geothermal heat-extraction potential by 2100
- **~4 m / °C** drilling equivalent (every degree of warming substitutes about 4 m of borehole depth)

## Features

- Hero with key thesis claim
- Abstract section
- 4 key-result stat cards
- 4-step methodology pipeline (Data, Model, Solve, Visual)
- Interactive map explorer with:
  - 8 CMIP6 climate models (BBC, CanESM, GFDL, GISS, HadGEM, IPSL, MIROC, MPI)
  - 2 SSP scenarios (2-4.5 and 5-8.5)
  - Ensemble statistics (mean, P25, P50, P75)
  - 16 selectable colormaps (9 for heat, 7 for power)
  - 6 toggleable data layers (50yr and 100yr horizons)
  - Click any pixel to read exact W/m and W values
  - Crisp pixel-rendered overlays at 5 km native resolution
- Floating GeoChat widget embedded via iframe
- Fullscreen map page (separate route, not in nav)
- Notebook download link

## Tech stack

- **Frontend:** Vanilla HTML / CSS / JavaScript
- **Mapping:** [Leaflet.js](https://leafletjs.com) + [chroma-js](https://gka.github.io/chroma.js/)
- **Data format:** 24 pre-computed JSON files (16 individual model+scenario, 8 ensemble statistics)
- **Source data:** CMIP6 GCMs from [Google Earth Engine](https://earthengine.google.com)
- **Modeling (in notebook):** Python with rasterio, geopandas, numpy, scipy, folium
- **Hosting:** Vercel (free tier), auto-deployed from GitHub
- **Total cost to run:** €0 / month

## How it works

The pipeline that produces this site is:

1. **CMIP6 data acquisition** - 8 GCMs from Google Earth Engine, both SSPs, reprojected to EPSG:4326
2. **BHE physics** - Finite Line Source (FLS) theory after Rivera (2017), superposed with surface boundary heating driven by CMIP6 trends
3. **Sustainable extraction** - Brent's method root-finding to compute the maximum heat extraction rate that keeps minimum fluid temperature above -1.5 °C over the operating horizon
4. **Per-pixel computation** - Run for every 5 km pixel across Germany, for every model and scenario
5. **JSON export** - `export_to_json.py` writes compact JSON files (~373 KB total) with the per-pixel results
6. **Live rendering** - JavaScript fetches the relevant JSON on demand, renders pixel-by-pixel to a canvas via chroma-js color scales, then overlays the canvas image on Leaflet with crisp-pixel rendering

Key model parameters: borehole depth H = 150 m, thermal diffusivity am = 1e-6 m²/s, borehole thermal resistance Rtb = 0.15 m K/W, minimum fluid temperature Tmin = -1.5 °C.

## How to reproduce locally

The site itself is static. To run it:

```bash
git clone https://github.com/VaibhavJ97/kit-master-thesis-portfolio.git
cd kit-master-thesis-portfolio
python3 -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000).

### To re-run the underlying Python analysis

The Jupyter notebook is in `files/Single_BHE_Analysis_GEE_CMIP6_Folium.ipynb`. Open it in Google Colab (recommended, no setup) or locally. Requirements:

- Google Earth Engine authentication (free)
- Python 3.10+
- rasterio, geopandas, numpy, scipy, folium, matplotlib

After running all cells, `export_to_json.py` writes the JSON files to `data_json/`, which the frontend reads.

## Project structure

```
kit-master-thesis-portfolio/
├── index.html              Main thesis page (hero, findings, methodology, explorer)
├── map-fullscreen.html     Standalone fullscreen map page
├── data_json/
│   ├── meta.json
│   ├── individual/         16 JSON files (model × scenario)
│   └── ensemble/           8 JSON files (statistic × scenario)
├── files/
│   └── Single_BHE_Analysis_GEE_CMIP6_Folium.ipynb
├── vercel.json
└── README.md
```

## Deploy

Push to `main` and Vercel auto-deploys. No build step.

## Thesis supervisors

- **PD Dr. Kathrin Menberg** - Institute of Applied Geosciences (AGW), Chair of Engineering Geology, KIT
- **Dr. Susanne Benz** - Institute for Photogrammetry and Remote Sensing (IPF), GRUSS group, KIT

## AI coding assistance disclosure

The interactive map explorer (JSON-based architecture, canvas rendering pipeline, colormap switching, layer toggles, click-to-query, styling) was developed with [Claude](https://claude.ai) (Anthropic) as a coding partner. The original scientific code in the Jupyter notebook (BHE physics, CMIP6 ingestion, FLS implementation, Brent's iteration, per-pixel computation) is the author's own work.

## Author

**Vaibhav Jaiswal**
M.Sc. Applied Geosciences, Karlsruhe Institute of Technology, 2026

- Email: vaibhavjaiswal1234@gmail.com
- LinkedIn: [linkedin.com/in/vaibhavgeo](https://www.linkedin.com/in/vaibhavgeo/)
- GitHub: [@VaibhavJ97](https://github.com/VaibhavJ97)
- Portfolio: [vaibhavj97.vercel.app](https://vaibhavj97.vercel.app)

## License

Code and visualizations are released under the MIT License for academic and research reuse with appropriate attribution. The thesis itself remains under standard KIT academic terms; cite as:

> Jaiswal, V. (2026). *Impact of Climate Change on the Geothermal Potential of Closed Systems Using GIS and Python.* M.Sc. Thesis, Karlsruhe Institute of Technology.
