# Executive Research Summary: Interplanetary Survival Guide — Martian Map
## NASA Space Apps Challenge 2026 Reference Document

---

## 1. Challenge & Problem Statement Overview

* **Challenge Name:** Interplanetary Survival Guide: Martian Map
* **Official URL:** [https://www.spaceappschallenge.org/2026/challenges/interplanetary-survival-guide-martian-map/](https://www.spaceappschallenge.org/2026/challenges/interplanetary-survival-guide-martian-map/)
* **Official Prompt:** Create a layered, integrated view of a location or route on the Martian surface that pulls together data from multiple NASA science missions to help human explorers plan and carry out a successful Marswalk while conducting new and exciting science along the way.
* **The Core Problem:** Unlike Apollo lunar missions with instantaneous ground communication, astronauts on Mars will operate under a 3.1-to-22.3-minute one-way communication latency. They must survive lethal surface conditions (near-vacuum pressure, radiation, sub-zero cold, and perchlorate dust) using localized, highly autonomous navigation and decision-support tools.
* **Core Deliverables Required:**
  1. Interactive layered map or route planner integrating at least three distinct planetary datasets.
  2. Architectural documentation detailing dataset retrieval, processing, and visualization.
  3. Simulated Marswalk use-case scenario demonstrating hazard mitigation and scientific waypoints.
  4. Open-source code repository with clear documentation and presentation pitch deck.

---

## 2. Key Martian Environmental Realities & Astronaut Hazards

| Hazard / Parameter | Environmental Reality on Mars | Physiological & Operational Impact | Mitigation & System Requirement |
| :--- | :--- | :--- | :--- |
| **Atmospheric Pressure** | $\sim 6.1\text{ hPa}$ ($<1\%$ of Earth; below Armstrong Limit of $\sim 63\text{ hPa}$) | Immediate ebullism (body fluids boil at $37^\circ\text{C}$); asphyxiation within seconds. | Pressurized EVA spacesuits ($20\text{--}30\text{ kPa}$ pure $O_2$); rigid pressure seals. |
| **Atmospheric Composition** | 95.3% $\text{CO}_2$, 2.6% $\text{N}_2$, 1.9% $\text{Ar}$, 0.16% $\text{O}_2$ | Toxic for inhalation; ambient air cannot be breathed directly. | Closed-loop life support; MOXIE-style ISRU electrolysis of $\text{CO}_2$ to generate $\text{O}_2$. |
| **Surface Temperature** | Diurnal equatorial swing: $+20^\circ\text{C}$ midday to $-80^\circ\text{C}$ night; polar lows of $-140^\circ\text{C}$ | Steep vertical thermal gradient ($+20^\circ\text{C}$ at feet vs. $0^\circ\text{C}$ at head); battery depletion; material embrittlement. | Spacesuit Liquid Cooling & Ventilation Garments (LCVG); heater-assisted electronics; diurnal travel windows. |
| **Radiation Environment** | No global magnetic field. GCR baseline $\approx 0.64\text{ mSv/day}$ ($\sim 230\text{ mSv/yr}$); SPE solar proton flares $>1,000\text{ mSv}$ | Elevated long-term cancer risk; acute radiation sickness (ARS) from coronal mass ejections. | Space weather telemetry alerts; mapping topographical shelters (lava tubes, canyon overhangs, regolith berms). |
| **Regolith & Perchlorates** | Soil contains 0.5%–1.0% toxic perchlorates ($\text{ClO}_4^-$); abrasive angular basalt dust | Endocrine disruption, thyroid failure, pulmonary inflammation if dust is inhaled in habitat. | Multi-stage airlock cleaning, suitports, electrostatic repulsion, sacrificial dust covers. |
| **Topography & Traversability** | Extreme relief ($-8.2\text{ km}$ to $+21.9\text{ km}$ vs. MOLA Areoid). Regolith angle of repose $30^\circ\text{--}34^\circ$ | Slopes $>15^\circ$ cause metabolic strain; slopes $>25^\circ$ risk avalanches, rover rollovers, and falls. | Dynamic slope gradient heatmaps ($0^\circ\text{--}15^\circ$ green, $15^\circ\text{--}25^\circ$ yellow, $>25^\circ$ red hazard). |
| **Light & Vision** | Low atmospheric scatter produces harsh shadows and flat lighting in diffuse dust haze | Inability to judge subtle terrain depressions, cracks, and boulder obstacles. | High-contrast hillshade elevation overlays and visual odometry landmarks. |

---

## 3. NASA Planetary Data Sources & Multi-Layer Schema

To build an interplanetary map, data from distinct robotic missions is layered into a unified operational stack:

```
┌────────────────────────────────────────────────────────────────────────┐
│                   MARSWALK TACTICAL INTERFACE STACK                    │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 5: Science Waypoints & Astrobiology Targets                     │
│          • MRO CRISM (Hydrated Clays, Carbonates, Sulfates)            │
│          • USGS Geologic Maps (Stratigraphy & Formation Ages)          │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 4: Space Weather & Atmospheric Telemetry                        │
│          • MSL RAD (Cumulative mSv/day Surface Radiation)              │
│          • Mars 2020 MEDA / MSL REMS (Surface Temp, Pressure, Dust Tau)│
├────────────────────────────────────────────────────────────────────────┤
│ Layer 3: Thermophysical Stability & Soil Bearing Strength              │
│          • 2001 Mars Odyssey THEMIS (Thermal Inertia: Bedrock vs Dust) │
├────────────────────────────────────────────────────────────────────────┤
│ Layer 2: Micro & Macro Topography / Slope Hazards                     │
│          • MGS MOLA (463m Regional DEM & Elevation Profile)            │
│          • MRO HiRISE DTM (1.0m Sub-meter Stereo Elevation & Obstacles)│
├────────────────────────────────────────────────────────────────────────┤
│ Layer 1: High-Resolution Visual Orthomosaics                          │
│          • MRO CTX (6m/px Regional Context Mosaic)                     │
│          • MRO HiRISE (0.25m/px Ultra-High-Resolution Feature Base)    │
└────────────────────────────────────────────────────────────────────────┘
```

### Official NASA Challenge Data Portals & Resources

The challenge prompt explicitly highlights five core NASA and USGS resources:

1. **Jet Propulsion Laboratory’s (JPL) Mars Trek:**  
   * **URL:** [https://trek.nasa.gov/mars/](https://trek.nasa.gov/mars/)  
   * **NASA Description:** NASA web-based portal for exploration of Mars, showcases data collected by NASA at various landing sites.  
   * **Project Integration:** Serves as the primary reference for interactive 2D/3D map tiles, landing site dossiers, and standardized OGC WMTS endpoints.
2. **USGS-NASA Planetary Geologic Mapping Program:**  
   * **URL:** [https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars](https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars)  
   * **NASA Description:** High-quality standardized geologic map of Mars.  
   * **Project Integration:** Provides peer-reviewed geologic stratigraphy, age classifications (Noachian/Hesperian/Amazonian), and structural fault vectors.
3. **Curiosity Rover Proposed Route Up Mount Sharp (Visual Benchmark):**  
   * **URL:** [https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/](https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/)  
   * **NASA Description:** This animation shows a proposed route for NASA's Curiosity rover, which is climbing lower Mount Sharp on Mars. The annotated version of the map labels different regions that scientists working with the rover would like to explore in coming years. A flyover video explains them in more detail.  
   * **Project Integration:** Directly guides our traversal visualization model—labeling scientific stop regions, hazard bypasses, and ascent corridors.
4. **NASA Worldview:**  
   * **URL:** [https://worldview.earthdata.nasa.gov/](https://worldview.earthdata.nasa.gov/)  
   * **NASA Description:** Visually explore the past and the present of this dynamic planet from a satellite's perspective. Select from an array of stories below to learn more about Worldview (a part of NASA Earthdata), the satellite imagery we provide and events occurring around the world.  
   * **Project Integration:** Inspires our UI/UX layout for multi-layer satellite toggling, opacity mixing, and diurnal/seasonal timeline scrubbing.
5. **Mars Perseverance Raw Images Gallery:**  
   * **URL:** [https://mars.nasa.gov/mars2020/multimedia/raw-images/](https://mars.nasa.gov/mars2020/multimedia/raw-images/)  
   * **NASA Description:** Over 1 million images captured by the rover on its journey across the Mars surface.  
   * **Project Integration:** Powers our ground-level Point-of-View (POV) feature, enabling astronauts to preview rover-ground images at waypoints.

---

### Detailed Mission & Dataset Matrix

| Dataset / Sensor | Spacecraft | Spectral / Data Type | Resolution | Data Access URL | Key Role in Project |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **JPL Mars Trek** | NASA JPL | Web GIS Tile Services (WMTS)| Multi-scale | [JPL Mars Trek](https://trek.nasa.gov/mars/) | Standard OGC tile endpoints to feed Leaflet/Cesium map viewports. |
| **USGS Mars GIS** | USGS Astrogeology | Geologic Map Vector Layers | 1:5M to 1:24k | [USGS Interactive Maps](https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars) | Standardized planetary geologic units and age classifications. |
| **Mount Sharp Route** | NASA Science / MSL | Annotated Traversal Visual | Perspective | [Curiosity Route Visual](https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/) | Benchmark for waypoint annotation and safe corridor plotting. |
| **NASA Worldview** | NASA Earthdata | Multi-layer Satellite Engine | Dynamic | [NASA Worldview](https://worldview.earthdata.nasa.gov/) | Architectural reference for temporal scrubbing and layer toggling. |
| **Perseverance Gallery** | Mars 2020 Rover | In-Situ Ground Camera Imagery | POV Images | [Perseverance Raw Images](https://mars.nasa.gov/mars2020/multimedia/raw-images/) | Ground-level photographic verification along traverse path. |
| **MOLA** | Mars Global Surveyor | Laser Altimeter DEM | 463 m/px | [PDS MOLA Record](https://pds-geosciences.wustl.edu/missions/mgs/mola.html) | Global elevation basemap, large-scale slope profiles. |
| **HiRISE** | Mars Reconnaissance Orbiter | Optical & Stereo DTM | 0.25 m/px optical, 1 m DTM | [HiRISE Ops Center](https://hirise.lpl.arizona.edu/) | Tactical boulder identification, crevasse avoidance, micro-slope mapping. |
| **CTX** | Mars Reconnaissance Orbiter | Panchromatic Optical | 6.0 m/px | [Caltech Murray CTX Mosaic](https://murray-lab.caltech.edu/CTX/) | Comprehensive regional visual basemap covering >99% of Mars. |
| **THEMIS** | 2001 Mars Odyssey | Thermal Infrared (9 bands) | 100 m/px | [ASU THEMIS Archive](https://themis.asu.edu/) | Thermal inertia mapping: distinguishes firm bedrock from hazardously deep dust. |
| **CRISM** | Mars Reconnaissance Orbiter | Hyperspectral Imaging | 18–36 m/px | [JHU/APL CRISM](https://crism.jhuapl.edu/) | Mineralogical targets (clays, sulfates) for astronaut sampling. |
| **REMS / MEDA** | Curiosity & Perseverance | Surface Weather Sensors | In-situ point telemetry | [PDS Atmospheres](https://pds-atmospheres.nmsu.edu/) | Ground truth for atmospheric density, diurnal temperatures, dust tau. |
| **RAD** | Curiosity Rover | Energetic Particle Detector | In-situ point telemetry | [PDS Atmospheres MSL RAD](https://pds-atmospheres.nmsu.edu/) | Measures surface GCR and SPE solar flare radiation dosages. |
| **RIMFAX** | Perseverance Rover | Ground-Penetrating Radar | Deep subsurface (0–10m) | [PDS Geosciences RIMFAX](https://pds-geosciences.wustl.edu/missions/mars2020/rimfax.htm) | Detects shallow subsurface rock layers, voids, and potential ice. |

---

## 4. Operational Marswalk (EVA) Simulation Scenario

To validate the multi-layer map, a representative 6-hour Marswalk traverse can be modeled:
* **Location:** Lower Mount Sharp, Gale Crater (or Western Jezero Crater Delta).
* **Traverse Distance:** 2.5 km outbound, 2.5 km return (5.0 km total).
* **Consumable Budget:**
  * Oxygen store: 8 hours maximum nominal capacity.
  * Point of No Return (PNR): Triggered when remaining consumable capacity reaches $120\%$ of return transit requirement.
* **Traverse Path Rules:**
  1. All segments maintain slope $<15^\circ$ to minimize suit cooling and metabolic strain.
  2. Path avoids high-albedo, low-thermal-inertia ripple fields (deep soft dust) identified by THEMIS.
  3. Boulders $>0.5\text{ m}$ visible in HiRISE are circumnavigated by at least 3 meters.
  4. Scheduled stops at CRISM-identified clay/sulfate contact boundaries for sample extraction.
  5. Constant line-of-sight communication relay maintained with the base habitat or pressurized exploration rover.

---

## 5. Verified NASA References & Citations

1. **NASA Jet Propulsion Laboratory:** Mars Exploration Program & Rover Science Archives. [https://mars.nasa.gov](https://mars.nasa.gov)
2. **NASA Planetary Data System (PDS):** Geosciences and Atmospheres Nodes. [https://pds.nasa.gov](https://pds.nasa.gov)
3. **NASA Langley Research Center:** Mars Global Reference Atmospheric Model (Mars-GRAM). [https://software.nasa.gov/software/MFS-33157-1](https://software.nasa.gov/software/MFS-33157-1)
4. **USGS Astrogeology Science Center:** Planetary Geologic Mapping and Digital Elevation Models. [https://astrogeology.usgs.gov](https://astrogeology.usgs.gov)
5. **Hassler, D. M., et al. (2014):** *Mars' Surface Radiation Environment Measured with the Mars Science Laboratory's Curiosity Rover.* Science 343, 1244797.
6. **Hecht, M. H., et al. (2009):** *Detection of Perchlorate by the Mars Phoenix Lander and Implications for Habitability.* Science 325, 64–67.

