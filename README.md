# Interplanetary Survival Guide: Martian Map
## NASA Space Apps Challenge 2026 — Research Documentation & Project Summary

[![NASA Space Apps Challenge 2026](https://img.shields.io/badge/NASA%20Space%20Apps-2026-blue.svg)](https://www.spaceappschallenge.org/2026/challenges/interplanetary-survival-guide-martian-map/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status: Research & Documentation](https://img.shields.io/badge/Status-Research%20%26%20Documentation-green.svg)](#)

---

## 📌 Challenge Information

* **Challenge Title:** Interplanetary Survival Guide: Martian Map
* **Year:** NASA Space Apps Challenge 2026
* **Official Challenge URL:** [https://www.spaceappschallenge.org/2026/challenges/interplanetary-survival-guide-martian-map/](https://www.spaceappschallenge.org/2026/challenges/interplanetary-survival-guide-martian-map/)
* **Organized By:** NASA Science Mission Directorate
* **Focus Area:** Human Planetary Exploration, Planetary GIS, Multi-Mission Data Fusion, Extravehicular Activity (EVA) Planning

### Official Challenge Excerpt
> "NASA has explored Mars robotically for decades, studying its extreme environment, mapping its surface, and collecting many types of data. Far from home, the first astronauts to set foot on Mars will want the best map possible, with information on the details of their routes and destinations, updates on current conditions, and the data needed to complete their mission quickly and safely.
>
> Your challenge is to create a layered, integrated view of a location or route on the Martian surface that pulls together data from multiple NASA science missions and could help a human explorer plan and carry out a successful Marswalk while conducting new and exciting science along the way."

---

## 📂 Research Documentation Index

All detailed research deliverables have been compiled inside the [`research/`](research/) directory:

| Document | File Link | Description |
| :--- | :--- | :--- |
| **Problem Statement & Requirements** | [`research/problem-statement.md`](research/problem-statement.md) | Official problem statement, objectives, constraints, form factors (HUD/console/tablet), and Space Apps deliverables. |
| **Mars Science & Survival Guide** | [`research/mars-research.md`](research/mars-research.md) | In-depth analysis of Mars geography, atmosphere, Armstrong limit, diurnal temperatures, radiation (GCR & SPE), perchlorate toxicity, and EVA constraints. |
| **NASA Data Sources & Integration Guide** | [`research/nasa-data-sources.md`](research/nasa-data-sources.md) | Comprehensive catalog of NASA datasets (MOLA, HiRISE, THEMIS, CTX, CRISM, REMS, MEDA, RAD, RIMFAX, Mars Trek WMS), resolutions, APIs, and multi-layer schema. |
| **Executive Research Summary** | [`research/research-summary.md`](research/research-summary.md) | Consolidated reference summary combining all findings for rapid mission planning and architectural design. |

---

## 🔬 Executive Summary of Research Findings

### 1. The Operational Problem on Mars
Future astronauts executing surface excursions ("Marswalks") must operate with near-total autonomy due to an absolute communication latency of **3.1 to 22.3 minutes each way** with Earth. Apollo moonwalkers had real-time Mission Control support; Martian astronauts must rely on onboard geospatial intelligence to survive:
* **Near-Vacuum Atmosphere:** Mean surface pressure of $\approx 6.1\text{ hPa}$ ($<1\%$ of Earth), well below the **Armstrong Limit ($\approx 63\text{ hPa}$)** where body fluids boil at $37^\circ\text{C}$. Pressurized EVA suits ($20\text{--}30\text{ kPa}$) are non-negotiable.
* **Extreme Thermal Cycling:** Midday equatorial highs of $+20^\circ\text{C}$ plummet to $-80^\circ\text{C}$ at night (down to $-140^\circ\text{C}$ at polar regions). Severe vertical temperature gradients ($+20^\circ\text{C}$ at boots, $0^\circ\text{C}$ at helmet) induce material fatigue.
* **Lethal Radiation:** No global magnetic field. Astronauts face continuous **Galactic Cosmic Rays (GCR)** at $\approx 0.64\text{ mSv/day}$ ($\sim 230\text{ mSv/year}$, measured by Curiosity RAD) and sporadic **Solar Particle Events (SPE)** delivering $>1,000\text{ mSv}$ within hours without shielding.
* **Toxic Regolith & Perchlorates:** Soil contains **0.5%–1.0% calcium/magnesium perchlorates ($\text{ClO}_4^-$)**—strong oxidizers that destroy thyroid function and cause aplastic anemia. Multi-stage airlock dust mitigation is mandatory.
* **Topographic Traversability:** Dry regolith angle of repose is $30^\circ\text{--}34^\circ$. Slopes $>15^\circ$ cause heavy suit fatigue; slopes $>25^\circ$ present severe avalanche and rollover hazards.

---

### 2. Multi-Layer NASA Data Architecture

The project synthesizes multi-mission datasets into an integrated 5-layer operational map:

```
┌────────────────────────────────────────────────────────────────────────┐
│                   ASTRONAUT TACTICAL MARSWALK MAP                      │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 5: Science Waypoints & ISRU (MRO CRISM & USGS Geologic Maps)     │
│          • Clays (Phyllosilicates), Sulfates, Hydrated Silica, Ice     │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 4: Space Weather & Microclimate (MSL RAD & M2020 MEDA / REMS)    │
│          • Cumulative Radiation Dose (mSv), Dust Tau, Ambient Temp     │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 3: Thermophysical Stability & Soil Bearing (Odyssey THEMIS)      │
│          • Thermal Inertia (Firm Bedrock vs. Soft Sinking Dust)        │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 2: Micro & Macro Topography / Slopes (MGS MOLA + MRO HiRISE DTM) │
│          • 463m Regional DEM + 1m Local DTM (Slope Hazards & Crevasses)│
├────────────────────────────────────────────────────────────────────────┤
│ Layer 1: High-Resolution Visual Orthomosaics (MRO CTX & HiRISE)        │
│          • 6m/px CTX Context Basemap + 0.25m/px HiRISE Feature Details │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 3. Key NASA Missions & Datasets Summary

#### Core Challenge Portals & Benchmarks
1. **Jet Propulsion Laboratory’s (JPL) Mars Trek:** [https://trek.nasa.gov/mars/](https://trek.nasa.gov/mars/)  
   *NASA web-based portal for exploration of Mars, showcases data collected by NASA at various landing sites.*  
   *Utility:* Provides standardized OGC WMTS endpoints, 2D/3D viewers, and landing site dossiers.
2. **USGS-NASA Planetary Geologic Mapping Program:** [https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars](https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars)  
   *High-quality standardized geologic map of Mars.*  
   *Utility:* Peer-reviewed stratigraphic layers, structural fault lines, and geological epoch boundaries.
3. **Curiosity Rover Proposed Route Up Mount Sharp (Route Map Visual):** [https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/](https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/)  
   *This animation shows a proposed route for NASA's Curiosity rover, which is climbing lower Mount Sharp on Mars. The annotated version of the map labels different regions that scientists working with the rover would like to explore in coming years. A flyover video explains them in more detail.*  
   *Utility:* Prime visual benchmark for annotating mission corridors, scientific waypoints, and topography traversal.
4. **NASA Worldview:** [https://worldview.earthdata.nasa.gov/](https://worldview.earthdata.nasa.gov/)  
   *Visually explore the past and the present of this dynamic planet from a satellite's perspective. Select from an array of stories below to learn more about Worldview (a part of NASA Earthdata), the satellite imagery we provide and events occurring around the world.*  
   *Utility:* Architectural and UX model for timeline scrubbing, satellite multi-layer compositing, and dynamic opacity.
5. **Mars Perseverance Raw Images Gallery:** [https://mars.nasa.gov/mars2020/multimedia/raw-images/](https://mars.nasa.gov/mars2020/multimedia/raw-images/)  
   *Over 1 million images captured by the rover on its journey across the Mars surface.*  
   *Utility:* Ground-level first-person view (POV) Navcam/Mastcam imagery to preview terrain at each waypoint.

#### Multi-Mission Sensor Matrix
| Instrument | Spacecraft / Mission | Primary Data Type | Spatial Resolution | Official Access URL | Project Role |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **MOLA** | Mars Global Surveyor | Laser Altimetry / DEM | 463 m/px (128 ppd) | [PDS MOLA](https://pds-geosciences.wustl.edu/missions/mgs/mola.html) | Macro-elevation grid & regional slope relief |
| **HiRISE** | Mars Reconnaissance Orbiter | Ultra-High-Res Optical & DTM | 0.25–0.3 m/px (1 m DTM) | [HiRISE Ops](https://hirise.lpl.arizona.edu/) | Boulder avoidance, crevasse detection & 1m slope profile |
| **CTX** | Mars Reconnaissance Orbiter | Panchromatic Context Mosaic | 6.0 m/px | [Caltech Murray CTX](https://murray-lab.caltech.edu/CTX/) | High-contrast visual base map across landing zones |
| **THEMIS** | 2001 Mars Odyssey | Thermal Infrared & Inertia | 100 m/px | [ASU THEMIS](https://themis.asu.edu/) | Ground bearing capacity & bedrock vs. fine dust identification |
| **CRISM** | Mars Reconnaissance Orbiter | Hyperspectral Mineralogy | 18–36 m/px | [JHU/APL CRISM](https://crism.jhuapl.edu/) | Scientific waypoint designation & hydrated mineral targets |
| **RAD** | MSL Curiosity Rover | Surface Radiation Dosimetry | In-situ point sensor | [PDS Atmospheres MSL](https://pds-atmospheres.nmsu.edu/) | Baseline GCR and SPE solar flare hazard metrics |
| **MEDA / REMS** | Mars 2020 & Curiosity | Weather & Dust Optical Depth | In-situ point sensor | [PDS Atmospheres M2020](https://pds-atmospheres.nmsu.edu/) | Real-time atmospheric pressure, wind & dust opacity ($\tau$) |
| **RIMFAX** | Mars 2020 Perseverance | Ground-Penetrating Radar | Deep subsurface (0–10m) | [PDS Geosciences RIMFAX](https://pds-geosciences.wustl.edu/missions/mars2020/rimfax.htm) | Shallow subsurface stratigraphy and ice-layer identification |
| **Mars Trek** | NASA JPL | Web GIS Tile Services (WMTS) | Multi-resolution | [JPL Mars Trek](https://trek.nasa.gov/mars/) | Standardized tile endpoints for map visualization |
| **Geologic GIS** | USGS Astrogeology | Standard Stratigraphic Maps | 1:5,000,000 to 1:24,000 | [USGS Astrogeology](https://astrogeology.usgs.gov/) | Structural and geological epoch classification |

---

### 4. EVA Route Planning & Mission Walkthrough Criteria

To demonstrate a valid Marswalk traversal (e.g., Mount Sharp in Gale Crater or Jezero Delta):
1. **Consumable Budgeting:** Standard EVA timeline is **6 to 8 hours** max, governed by $O_2$ stores, $\text{CO}_2$ scrubbing, battery life, and cooling water.
2. **Safe Corridor Routing:** Enforce slope ceiling $\le 15^\circ$, avoid known sand ripple dune fields (wheel entrapment), and maintain line-of-sight or beacon relays with the habitat/pressurized rover.
3. **Scientific Value Maximization:** Waypoint stops mapped to mineral transitions (e.g., clay-bearing units transitioning to sulfate units) indicating past habitability.
4. **Emergency Abort Thresholds:** Automated real-time return-to-base countdown based on remaining consumables and distance-to-shelter.

---

## 🔗 Official References & NASA Portals

* **NASA Planetary Data System (PDS):** [https://pds.nasa.gov/](https://pds.nasa.gov/)
* **JPL Mars Trek:** [https://trek.nasa.gov/mars/](https://trek.nasa.gov/mars/)
* **USGS Mars Interactive Maps:** [https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars](https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars)
* **NASA Mars Exploration Program:** [https://science.nasa.gov/mars/](https://science.nasa.gov/mars/)
* **Curiosity Path Up Mount Sharp:** [https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/](https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/)
* **Perseverance Raw Image Gallery:** [https://mars.nasa.gov/mars2020/multimedia/raw-images/](https://mars.nasa.gov/mars2020/multimedia/raw-images/)

