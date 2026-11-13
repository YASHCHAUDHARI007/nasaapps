# NASA Mars Data Sources, Mission Archives & Integration Guide

## 1. NASA Planetary Data Ecosystem Overview

All scientific data acquired by NASA planetary missions is rigorously processed, peer-reviewed, and archived in the **Planetary Data System (PDS)**. The PDS is organized into disciplinary nodes (Geosciences, Imaging, Atmospheres, Planetary Plasma, Small Bodies). For the *Interplanetary Survival Guide: Martian Map* project, we leverage calibrated spatial and temporal datasets from active and legacy Mars exploration missions.

```
                                  ┌───────────────────────────────┐
                                  │   NASA Planetary Data System  │
                                  │           (PDS)               │
                                  └───────────────┬───────────────┘
                     ┌────────────────────────────┼───────────────────────────┐
                     ▼                            ▼                           ▼
        ┌─────────────────────────┐  ┌─────────────────────────┐  ┌─────────────────────────┐
        │   PDS Geosciences Node  │  │    PDS Imaging Node     │  │  PDS Atmospheres Node   │
        │  (Washington Univ. StL) │  │       (NASA JPL/USGS)   │  │   (New Mexico State)    │
        ├─────────────────────────┤  ├─────────────────────────┤  ├─────────────────────────┤
        │ • MOLA Elevation & DEMs │  │ • HiRISE 25cm/px Images │  │ • REMS/MEDA Weather     │
        │ • CRISM Hyperspectral   │  │ • HiRISE Stereo DTMs    │  │ • Atmospheric Dust (Tau)│
        │ • THEMIS Thermal Inertia│  │ • CTX 6m Context Images │  │ • Ambient Temperatures  │
        │ • RIMFAX Radar Sounding │  │ • Rover Navcam/Mastcam  │  │ • Surface Pressure Data │
        └─────────────────────────┘  └─────────────────────────┘  └─────────────────────────┘
```

---

## 2. Core Datasets & Mission Deep-Dive

### 2.1 MOLA (Mars Orbiter Laser Altimeter)
* **Mission:** Mars Global Surveyor (MGS)
* **Operating Period:** 1997–2006
* **Instrument Specifications:** Neodymium-doped Yttrium Aluminum Garnet (Nd:YAG) laser operating at 1,064 nm wavelength, firing 10 pulses per second with an 8-nanosecond pulse width.
* **Archived Data Products:**
  * **MEGDR (Mission Experiment Gridded Data Record):** Global digital elevation models available in resolutions of 4, 16, 32, 64, and 128 pixels per degree (~463 meters/pixel at the equator).
  * **PEDR (Precision Experiment Data Record):** Raw altimetry profiles measuring individual shot points along ground tracks with vertical precision of ~37.5 cm.
  * **Areoid Reference Datum:** Established the global Martian zero-elevation datum (gravitational equipotential matching a mean radius of 3,396,000 meters).
* **Official Data Access URLs:**
  * PDS Geosciences Node: [https://pds-geosciences.wustl.edu/missions/mgs/mola.html](https://pds-geosciences.wustl.edu/missions/mgs/mola.html)
  * USGS Astrogeology MOLA DEM Portal: [https://astrogeology.usgs.gov/search/map/mars_mgs_mola_dem_463m](https://astrogeology.usgs.gov/search/map/mars_mgs_mola_dem_463m)
* **Project Role & Utility:**
  * Provides the overarching macro-elevation grid across any selected region on Mars.
  * Powers macro-slope calculation, regional topographic profile rendering, and broad catchment/watershed drainage modeling.

---

### 2.2 HiRISE (High Resolution Imaging Science Experiment)
* **Mission:** Mars Reconnaissance Orbiter (MRO)
* **Operating Period:** 2006–Present
* **Instrument Specifications:** 0.5-meter aperture Cassegrain reflecting telescope equipped with 14 Time Delay Integration (TDI) CCD detectors covering visible red (570–830 nm), blue-green (400–600 nm), and near-infrared (800–1000 nm).
* **Ground Resolution:** **25 to 30 centimeters (0.25–0.30 m) per pixel** from a 300 km orbital altitude.
* **Key High-Level Products:**
  * **RDR (Reduced Data Records):** Map-projected, radiometric and geometrically calibrated color and panchromatic orthomosaics.
  * **Stereo DTMs (Digital Terrain Models):** High-precision stereo-pair elevation models generated at **1.0-meter horizontal grid spacing with sub-meter relative vertical precision**.
* **Official Data Access URLs:**
  * HiRISE Operations Center (Univ. of Arizona / JPL): [https://hirise.lpl.arizona.edu/](https://hirise.lpl.arizona.edu/)
  * HiRISE DTM Catalog: [https://www.uahirise.org/dtm/](https://www.uahirise.org/dtm/)
  * PDS Imaging Node: [https://pds-imaging.jpl.nasa.gov/volumes/mro.html](https://pds-imaging.jpl.nasa.gov/volumes/mro.html)
* **Project Role & Utility:**
  * **The linchpin for human surface EVA route planning:** At 25–30 cm/px and 1 m DTM resolution, HiRISE is the only orbital instrument capable of resolving meter-scale boulders, small impact craters, fissures, and sand ripples that represent physical obstacles to walking astronauts or rovers.
  * Enables micro-topographic slope and roughness analysis on the scale of human strides (1–2 meters).

---

### 2.3 THEMIS (Thermal Emission Imaging System)
* **Mission:** 2001 Mars Odyssey
* **Operating Period:** 2001–Present
* **Instrument Specifications:** Multi-spectral infrared camera (9 bands spanning 6.78 μm to 14.88 μm) and a 5-band visible camera (425 nm to 860 nm).
* **Archived Data Products:**
  * **Daytime Infrared Global Mosaic:** 100 meters/pixel spatial resolution; captures solar heating variations governed by topography and albedo.
  * **Nighttime Infrared Global Mosaic:** 100 meters/pixel spatial resolution; measures nighttime cooling rates, which directly correlate to physical thermal inertia.
  * **Thermal Inertia (TI) Quantitative Maps:** Units of $\text{J}\cdot\text{m}^{-2}\cdot\text{K}^{-1}\cdot\text{s}^{-1/2}$. High thermal inertia indicates solid bedrock or dense duricrust; low thermal inertia indicates loose, fine, insulating dust.
* **Official Data Access URLs:**
  * Arizona State University (ASU) THEMIS Archive: [https://themis.asu.edu/](https://themis.asu.edu/)
  * USGS THEMIS Nighttime Infrared Global Mosaic: [https://astrogeology.usgs.gov/search/map/mars_odyssey_themis_ir_night_100m](https://astrogeology.usgs.gov/search/map/mars_odyssey_themis_ir_night_100m)
* **Project Role & Utility:**
  * **Trafficability Assessment:** Distinguishes stable, load-bearing bedrock paths from hazardous, low-bearing-strength fine dust drifts where astronauts or rover wheels could sink.
  * **Thermal Hazard Prediction:** Forecasts ground contact temperatures for spacesuit boots and equipment thermal budgeting during morning and evening excursions.

---

### 2.4 CTX (Context Camera)
* **Mission:** Mars Reconnaissance Orbiter (MRO)
* **Operating Period:** 2006–Present
* **Instrument Specifications:** 350 mm focal length panchromatic telescope (500–800 nm wavelength band).
* **Spatial Resolution:** **6.0 meters per pixel** over a 30 km wide swath.
* **Coverage:** Has mapped over **99% of the entire Martian surface**.
* **Official Data Access URLs:**
  * Malin Space Science Systems (MSSS): [https://www.msss.com/msss_images/subject/context_images.html](https://www.msss.com/msss_images/subject/context_images.html)
  * Bruce Murray Laboratory Caltech Global CTX Mosaic: [https://murray-lab.caltech.edu/CTX/](https://murray-lab.caltech.edu/CTX/)
* **Project Role & Utility:**
  * Serves as the primary high-resolution visual context basemap, seamlessly bridging the gap between coarse global datasets (MOLA/THEMIS at 100–463 m) and focused high-resolution patches (HiRISE at 0.25 m).

---

### 2.5 CRISM (Compact Reconnaissance Imaging Spectrometer for Mars)
* **Mission:** Mars Reconnaissance Orbiter (MRO)
* **Operating Period:** 2006–2023
* **Instrument Specifications:** Hyperspectral imaging spectrometer with 544 spectral channels covering visible and near-infrared (362 to 3920 nm) with 15–38 m/pixel targeted spatial resolution.
* **Key Spectral Data Products:**
  * Targeted Empirical Data Records (TRDR) and Map-Projected Targeted Reduced Data Records (MTRDR).
  * Spectral Parameter Maps identifying diagnostic absorption bands for hydrated phyllosilicates (smectite, chlorite), sulfates (gypsum, jarosite), olivine, pyroxene, and water-ice frost.
* **Official Data Access URLs:**
  * Johns Hopkins University Applied Physics Laboratory: [https://crism.jhuapl.edu/](https://crism.jhuapl.edu/)
  * PDS Geosciences Node CRISM Archive: [https://pds-geosciences.wustl.edu/missions/mro/crism.htm](https://pds-geosciences.wustl.edu/missions/mro/crism.htm)
* **Project Role & Utility:**
  * **Scientific Waypoint Generation:** Enables mission planners to identify high-priority geological sampling sites where ancient aqueous alteration or biosignature preservation is greatest.
  * **ISRU Volatile Scouting:** Pinpoints subsurface hydrated minerals that could serve as water extraction feedstocks for human habitats.

---

### 2.6 Surface In-Situ Datasets: MSL Curiosity & Mars 2020 Perseverance

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                          IN-SITU SURFACE ROVER SENSOR SUITES                           │
├───────────────────────────────────────────┬────────────────────────────────────────────┤
│           MSL Curiosity (Gale)            │        Mars 2020 Perseverance (Jezero)     │
├───────────────────────────────────────────┼────────────────────────────────────────────┤
│ • REMS (Rover Environmental Monitoring)   │ • MEDA (Mars Environmental Dynamics)       │
│   - Ground/Air Temperature (K)            │   - Pressure, Temperature, Humidity        │
│   - Atmospheric Pressure (Pa)             │   - Dust Optical Depth (Tau) & Wind Vector │
│   - Relative Humidity & Wind Speed        │ • RIMFAX (Ground-Penetrating Radar)        │
│ • RAD (Radiation Assessment Detector)     │   - Subsurface stratigraphy (0–10m depth)  │
│   - Surface GCR Dose Equivalent (~0.64mSv)│ • Mastcam-Z & SuperCam Spectrometers       │
│   - SPE Flare Dose Rates                  │   - True-color 3D stereo panoramic imaging │
└───────────────────────────────────────────┴────────────────────────────────────────────┘
```

* **Official Data Access URLs:**
  * NASA PDS Atmospheres Node (REMS Data): [https://pds-atmospheres.nmsu.edu/data_and_services/atmospheres_data/MARS/curiosity/rems.html](https://pds-atmospheres.nmsu.edu/data_and_services/atmospheres_data/MARS/curiosity/rems.html)
  * NASA PDS Atmospheres Node (MEDA Data): [https://pds-atmospheres.nmsu.edu/data_and_services/atmospheres_data/MARS/mars2020/meda.html](https://pds-atmospheres.nmsu.edu/data_and_services/atmospheres_data/MARS/mars2020/meda.html)
  * NASA PDS Geosciences Node (RIMFAX Radar Data): [https://pds-geosciences.wustl.edu/missions/mars2020/rimfax.htm](https://pds-geosciences.wustl.edu/missions/mars2020/rimfax.htm)
  * Mars Perseverance Raw Images Gallery: [https://mars.nasa.gov/mars2020/multimedia/raw-images/](https://mars.nasa.gov/mars2020/multimedia/raw-images/)
* **Project Role & Utility:**
  * Supplies real, empirical ground-truth time series for ambient temperature, air density, dust storm progression, and radiation dose rates.
  * Provides POV surface imagery to simulate what astronauts see from their helmet visors.

---

## 3. NASA Web GIS Portals & Web Map Services (WMS/WMTS)

### 3.1 JPL Mars Trek (NASA Solar System Treks)
* **Overview:** A web-based application developed by NASA JPL that provides 2D and 3D visualization of Mars data from multiple instruments and missions.
* **Capabilities:** Layer compositing, elevation profile generation, slope calculation, sun angle visualization, 3D printing STL export, and VR headset support.
* **Official URL:** [https://trek.nasa.gov/mars/](https://trek.nasa.gov/mars/)
* **API & Tile Services:** Mars Trek exposes standardized OGC (Open Geospatial Consortium) Web Map Tile Services (WMTS) and RESTful API endpoints for loading base maps and product overlays into web mapping engines (Leaflet, CesiumJS, MapLibre).

### 3.2 USGS Astrogeology Planetary GIS & Geologic Maps
* **Overview:** The USGS Astrogeology Science Center produces standardized, peer-reviewed planetary geologic maps and Cloud-Optimized GeoTIFFs (COGs).
* **Official URL:** [https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars](https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars)
* **Standard Map Projections:**
  * Global/Equatorial: Equirectangular (Plate Carrée), Sinusoidal, or Mercator referenced to the IAU 2000 Mars Sphere (mean radius: 3,396,190 m).
  * Polar Regions: Polar Stereographic.

---

## 4. Multi-Layer Data Architecture for the Martian Map

To satisfy the challenge requirement of integrating **at least three distinct types of data**, our system architecture integrates five specialized functional layers:

| Layer Category | Source Mission & Sensor | Data Products Used | Operational Value for Astronaut |
| :--- | :--- | :--- | :--- |
| **Layer 1: Visual Base Map** | MRO CTX & Mars 2020 Navcam | 6m orthomosaic & ground panoramas | High-contrast visual reference of natural features and surface morphology. |
| **Layer 2: Topography & Slope** | MGS MOLA + MRO HiRISE DTM | 463m global DEM + 1m local DTM | Detects hazardous slopes (>15°), cliffs, boulder fields, and calculates terrain elevation profiles. |
| **Layer 3: Thermophysical Stability** | 2001 Mars Odyssey THEMIS | Nighttime IR & Thermal Inertia | Distinguishes firm bedrock from soft sinking dust; forecasts surface temperatures. |
| **Layer 4: Environmental / Radiation** | MSL RAD + Mars 2020 MEDA | Cumulative mSv/day dose & dust $\tau$ | Informs space weather danger zones, shelter proximity, and life-support limits. |
| **Layer 5: Science Waypoints** | MRO CRISM + USGS Geologic Maps | Mineral indices (clays, sulfates, ice) | Marks high-priority scientific sampling stations along the Marswalk traverse. |

---

## 5. Summary Matrix of NASA Data Sources

| Instrument | Spacecraft / Mission | Primary Data Type | Spatial Resolution | Official Archive URL |
| :--- | :--- | :--- | :--- | :--- |
| **MOLA** | Mars Global Surveyor | Laser Altimetry / DEM | 463 m/px (128 ppd) | [PDS MOLA](https://pds-geosciences.wustl.edu/missions/mgs/mola.html) |
| **HiRISE** | Mars Reconnaissance Orbiter | High-Res Optical & DTM | 0.25–0.3 m/px (1 m DTM) | [HiRISE Ops](https://hirise.lpl.arizona.edu/) |
| **THEMIS** | 2001 Mars Odyssey | Thermal IR & Inertia | 100 m/px | [ASU THEMIS](https://themis.asu.edu/) |
| **CTX** | Mars Reconnaissance Orbiter | Panchromatic Context | ~6.0 m/px | [MSSS CTX](https://www.msss.com/msss_images/subject/context_images.html) |
| **CRISM** | Mars Reconnaissance Orbiter | Hyperspectral Mineralogy| 18–36 m/px | [CRISM JHU/APL](https://crism.jhuapl.edu/) |
| **REMS & RAD**| MSL Curiosity Rover | Weather, In-Situ Radiation| In-situ point sensor | [PDS Atmospheres MSL](https://pds-atmospheres.nmsu.edu/) |
| **MEDA** | Mars 2020 Perseverance | Weather, Dust Optical Depth| In-situ point sensor | [PDS Atmospheres M2020](https://pds-atmospheres.nmsu.edu/) |
| **Mars Trek**| JPL / NASA | Web GIS Tile Services | Multi-resolution | [JPL Mars Trek](https://trek.nasa.gov/mars/) |
| **USGS Mars GIS**| USGS Astrogeology | Standard Geologic Maps | 1:5,000,000 to 1:24,000 | [USGS Astrogeology](https://astrogeology.usgs.gov/) |

