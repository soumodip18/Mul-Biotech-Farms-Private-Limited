# Mul Biotech Farms — Dashboard Build Status & Roadmap

Internal tracking document. Not linked from public-facing dashboard UIs.
Last updated: 20 June 2026

Status legend:
- ✅ **Built** — live in the current version, real data wired in
- 🚧 **Partial** — UI/logic scaffolded but running on estimated/placeholder data
- ⛔ **Not built** — deferred, with reason
- 🔒 **Blocked on input** — needs real data or a decision from you before it can be built honestly

---

## 1. Agri-GIS Soil & Climate Dashboard (v4.0)

Source roadmap: 8-phase commercial upgrade plan.

| Phase | Module | Status | Notes |
|---|---|---|---|
| 1 | Remove random thermal layer / static charts / fixed risk score | ✅ Built | Replaced with Open-Meteo + NASA GIBS LST, live forecast charts, computed Climate Risk Engine |
| 2 | Live Weather KPI panel | ✅ Built | Temp, humidity, rain, cloud, wind speed/direction, pressure, UV — Open-Meteo `current` endpoint |
| 2 | Soil KPI panel | ✅ Built | Moisture (0–27cm) and temperature (0–54cm), real Open-Meteo soil model |
| 2 | Irrigation KPI (ET₀) | 🚧 Partial | Using a simplified Hargreaves-style proxy, not full FAO-56 Penman-Monteith — needs daily solar radiation data to upgrade |
| 2 | Plant Stress KPI (VPD) | ✅ Built | Computed live from temperature & humidity, 4-zone classification |
| 3 | Historical analytics (1/3/5yr rainfall, temp) | 🚧 Partial | 1-year monthly aggregation built via Open-Meteo Archive API; 3yr/5yr ranges not yet added (same API, just needs date-range params + UI toggle) |
| 3 | Historical drought/flood trend, Climate Variability Index | ⛔ Not built | Needs a defined index methodology — not something to invent without your input on weighting |
| 4 | Satellite/GIS layers (NDVI, LST, flood, drought, satellite basemap) | ✅ Built | Live toggleable layers |
| 4 | KML/KMZ/GeoJSON/Shapefile upload | ⛔ Not built | Shapefile parsing needs binary/projection handling libraries; meaningful build effort, not a quick add |
| 4 | Farm boundary digitization, area calc, GPS point collection | ⛔ Not built | Same effort bucket as above — recommend building alongside Pond Measurement pattern from Aquadashboard v2.4 |
| 5 | Farm Health Score | ✅ Built | Composite from soil moisture, VPD, ET₀, temp anomaly |
| 5 | Crop Suitability Engine | ✅ Built | Using static 2025 state soil survey + live climate inputs |
| 5 | Irrigation Advisory | ✅ Built | Tied to ET₀ + soil moisture thresholds |
| 6 | Carbon Readiness Score | 🔒 Blocked on input | This is IRBAS-CARBON™ territory — needs your proprietary scoring formula/weights, which per your own copilot-instructions.md should not be disclosed or guessed at |
| 6 | Agroforestry Suitability Index | 🔒 Blocked on input | Same — IRBAS-RESTORE™/GEOSPATIAL™ logic |
| 6 | Carbon Project Screening Tool | 🔒 Blocked on input | Same |
| 6 | Tree Plantation Monitoring | ⛔ Not built | Needs time-series NDVI per-plot tracking + a defined baseline methodology |
| 6 | Baseline Environmental Report | ⛔ Not built | Depends on Phase 6 scoring being defined first |
| 7 | Executive KPI board | ✅ Built | Farm Health, Climate/Water/Flood/Drought Risk, crop portfolio, coordinates |
| 8 | Data governance badges (Real/Modelled/Estimated) + source/timestamp | ✅ Built | Applied across all panels |

**Next recommended build:** ET₀ upgrade to full FAO-56 (needs solar radiation — available from Open-Meteo, just needs wiring), or Phase 4 farm boundary tools (reusable pattern already exists in Aquadashboard v2.4's pond measurement module).

---

## 2. Aquadashboard (v2.4+)

Source roadmap: 4-phase, 16-module enterprise upgrade plan.

| Version | Module | Status | Notes |
|---|---|---|---|
| 2.3→2.4 | Exposed API key removal | ✅ Built | Same OpenWeatherMap key was duplicated across both dashboards — removed, migrated to Open-Meteo |
| 2.4 | Module 1: Pond Measurement | ✅ Built | Leaflet.draw + Turf.js — area, perimeter, volume, holding capacity, excavation estimate |
| 2.4 | Module 2: Economics Calculator | 🔒 Blocked on input | Needs real West Bengal feed/fingerling/labour/electricity cost figures. Can source typical regional benchmarks if you'd rather start there and clearly label them as estimates — your call |
| 2.4 | Module 3: Species Recommendation Engine | ✅ Built | Ranks 8 species by live temp, estimated NDWI, rainfall; suitability %, risk tier, culture method |
| 2.4 | Module 4: Water Quality Assessment | ⛔ Not built | Needs real sensor inputs (pH, DO, EC, TDS, ammonia, nitrite, salinity) — not something to simulate credibly |
| 2.4 | Module 5: Report Generator (PDF) | ⛔ Not built | Best built after Economics Calculator exists, so reports have real numbers to include |
| 2.5 | Module 6: Real NDWI (Sentinel-2/Landsat) | ⛔ Not built | Requires server-side band math (Earth Engine or similar) — not possible client-side in a static HTML file |
| 2.5 | Module 7: Water Persistence Analysis | ⛔ Not built | Depends on Module 6 |
| 2.5 | Module 8: Historical Satellite Analytics (2018–present) | ⛔ Not built | Depends on Module 6 |
| 2.5 | Module 9: Terrain Intelligence (SRTM/ALOS DEM) | ⛔ Not built | Possible without backend via Esri/OpenTopography tile services — worth scoping separately |
| 2.6 | Module 10: Fish Disease Risk System | 🔒 Blocked on input | Needs disease-specific threshold data (temp/humidity/water-quality correlations per disease) — should be sourced from veterinary/fisheries literature, not estimated |
| 2.6 | Module 11: Climate Risk Assessment | 🚧 Partial | Flood/drought signals already exist informally in the Water Analysis panel; not yet a dedicated scored module |
| 2.6 | Module 12: Water Security Index | ⛔ Not built | Needs a defined scoring methodology |
| 3.0 | Module 13: AI Aquaculture Advisor | ⛔ Not built | Strategic-tier, needs backend LLM integration |
| 3.0 | Module 14: dMRV Integration | 🔒 Blocked on input | Needs to connect to your actual dMRV dashboard (GitHub: soumodip18, Alpha v0.1) — integration point not yet defined |
| 3.0 | Module 15: Carbon Accounting | 🔒 Blocked on input | Standards alignment (Verra/Gold Standard/ISO 14064) needs real protocol selection, not assumed |
| 3.0 | Module 16: Multi-Farm Management | ⛔ Not built | Needs a defined data model for multiple farm records — larger architectural decision |

**Next recommended build:** Economics Calculator, since it unlocks the Report Generator and is the most client-facing "this looks production-ready" module. Needs your real cost inputs first.

---

## How to use this file

- Update the status column as modules move from ⛔/🔒 → 🚧 → ✅.
- 🔒 items should not be built on guessed numbers or invented methodology — flag them in chat when you have the real inputs.
- When a module ships, note the version it shipped in directly in this table rather than just in commit messages, so this stays the single source of truth for "what's actually live right now."
