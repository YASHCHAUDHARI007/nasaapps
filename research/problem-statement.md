# NASA Space Apps Challenge 2026: Challenge Brief & Problem Statement

## Challenge Overview

* **Challenge Title:** Interplanetary Survival Guide: Martian Map
* **Category:** Space Exploration / Software / Human Planetary Exploration
* **Challenge Level:** Intermediate
* **Skills Tagged:** Human Exploration, Mars, Planets & Moons, Software, Space Exploration
* **Official URL:** [NASA Space Apps Challenge 2026 - Interplanetary Survival Guide: Martian Map](https://www.spaceappschallenge.org/2026/challenges/interplanetary-survival-guide-martian-map/)
* **Organized By:** NASA Science Mission Directorate in partnership with Booz Allen Hamilton, Mindgrub, and SecondMuse.

---

## Official Challenge Description & Excerpt

> "NASA has explored Mars robotically for decades, studying its extreme environment, mapping its surface, and collecting many types of data. Far from home, the first astronauts to set foot on Mars will want the best map possible, with information on the details of their routes and destinations, updates on current conditions, and the data needed to complete their mission quickly and safely.
> 
> Your challenge is to create a layered, integrated view of a location or route on the Martian surface that pulls together data from multiple NASA science missions and could help a human explorer plan and carry out a successful Marswalk while conducting new and exciting science along the way."

---

## Official Background

Human explorers are able to conduct science and perform activities that robotic systems cannot replicate. As demonstrated during deep-space and lunar exploration missions (such as the Artemis program), human astronauts leverage critical thinking skills to make rapid cross-disciplinary connections, solve unexpected operational dilemmas, and apply contextual understanding to observations and scientific measurements in real time. This adaptability is the core reason NASA sends humans into extreme planetary environments—to illuminate how planetary bodies and the solar system formed, and to conduct science unachievable on Earth or solely with autonomous probes.

While current human exploration targets the lunar surface (under Artemis, laying the groundwork for a phased Moon Base), planetary science missions continuously pave the path for future human footsteps on Mars. Every robotic mission to Mars represents an intricate engineering and logistical milestone; sending human crews will be the most demanding and momentous endeavor in history. Becoming an interplanetary species demands the synthesis of extensive planetary datasets, cutting-edge spatial computing, and rigorous operational planning.

Decades of NASA orbiter, lander, and rover missions provide a rich, multi-spectral picture of the Red Planet. However, these datasets remain largely siloed and regional. Existing tools like the Jet Propulsion Laboratory's (JPL) **Mars Trek** and the **USGS-NASA Planetary Geologic Mapping Program** provide valuable regional and global macro-layers. However, they were engineered for broad scientific queries rather than the hyperlocalized, meter-scale operational environments that astronauts must navigate during individual Extravehicular Activities (EVAs / "Marswalks").

---

## Challenge Problem Statement & Objectives

### The Core Problem
Future astronauts conducting Extravehicular Activities (EVAs) on the Martian surface face lethal environmental conditions: near-vacuum atmospheric pressures, extreme temperature swings (-140 °C to +20 °C), unshielded cosmic and solar radiation, abrasive toxic dust containing perchlorates, steep treacherous topography, and an absolute communication latency of 4 to 24 minutes each way with Earth. 

Unlike Apollo moonwalkers who had direct real-time mission control assistance, Martian astronauts must operate with near-complete tactical autonomy. To survive and conduct high-value science, crew members require a unified, multi-layered, localized geospatial visualization tool that integrates topographic hazards, atmospheric dynamics, life-support constraints, and high-priority geological waypoints into an actionable navigation system.

### Core Objectives
1. **Hyperlocalized Focus Area:** Select a specific high-priority exploration site or route (e.g., Mount Sharp in Gale Crater, Jezero Crater delta, Valles Marineris canyon rims, or unexplored volcanic/subsurface ice corridors).
2. **Multi-Source Data Integration:** Integrate **at least three distinct types of planetary scientific data**—such as:
   * **Optical / Imagery:** High-resolution orthomosaics (HiRISE, CTX, rover navcams).
   * **Topographic / Elevation:** Laser altimetry and stereo digital elevation models (MOLA, HiRISE DTMs).
   * **Thermal / Thermophysical:** Day/night surface temperatures and thermal inertia (THEMIS).
   * **Spectral / Mineralogical:** Hydrated minerals, clays, carbonates, iron oxides (CRISM, OMEGA).
   * **Atmospheric & Space Weather:** Surface pressure, dust optical depth, ambient temperatures, and radiation dosage (Curiosity REMS/RAD, Perseverance MEDA).
   * **Chemical / Compositional:** Elemental composition and biosignature indicators (APXS, ChemCam, SuperCam, PIXL).
3. **Crew Safety & Hazard Mitigation:** Explicitly incorporate astronaut safety parameters, terrain traversability (slope angles, boulder fields, loose scree), space weather alerts, and consumable limits (oxygen, battery life, suit cooling).
4. **Mission Route & Scientific Waypoints:** Plot an optimal traversal path connecting designated scientific objectives (e.g., sampling ancient lacustrine sedimentary rocks, investigating boxwork structures, analyzing hydrothermal deposits) while avoiding impassable natural barriers.

---

## Potential Considerations & Modalities (From Official Guidance)

Teams may explore several operational form factors and architectural implementations:

1. **User Interface Modality:**
   * **Habitat / Cockpit Strategic Console:** A large high-resolution situational awareness workstation inside the pressurized habitat or pressurized rover used for pre-EVA planning and debriefing.
   * **Astronaut Field Tablet:** A ruggedized, touch- and glove-optimized portable interface carried by surface explorers.
   * **Heads-Up Display (HUD):** A holographic augmented reality visor display projecting directional waypoints, slope warnings, oxygen reserves, and environmental metrics directly within the astronaut's field of view.
2. **Product Delivery Format:**
   * An interactive digital application (web-based 2D/3D GIS dashboard, interactive mission route planner).
   * A dynamic map generation engine that synthesizes real-time sensor streams and static orbital datasets for any chosen Martian coordinates.
   * Visual point-of-view (POV) integration incorporating ground-level rover panorama imagery to give astronauts a clear preview of terrain features before arrival.
3. **Temporal Flexibility:**
   * Static baseline mapping (geology, topography, bedrock structures).
   * Historical mission timelines (reconstructing past rover traverses like Curiosity or Perseverance).
   * Predictive modeling (simulating diurnal temperature cycles, shifting shadows, and dust storm risks for a future human mission window in the 2030s/2040s).
4. **Crew & Logistics Dynamics:**
   * Accommodating two-person EVA buddy systems for safety and workload distribution.
   * Integrating unpressurized or pressurized exploration rovers and autonomous robotic scouts (e.g., aerial drones like Ingenuity) to transport tools, samples, and life-support spares.

---

## Expected Requirements & Deliverables

For the NASA Space Apps Challenge submission, the expected deliverables include:

| Deliverable | Description |
| :--- | :--- |
| **Interactive Map / Tool** | A functional digital tool or interface allowing astronauts or mission planners to toggle layers (elevation, slope, temperature, radiation, science targets) and inspect navigation paths. |
| **Comprehensive Documentation** | Clear architectural breakdown explaining how NASA data was parsed, processed, georeferenced, and synthesized. |
| **Use Case Walkthrough** | A concrete scenario detailing a simulated "Marswalk" (e.g., a 6-hour EVA covering a 2.5 km traverse to investigate sedimentary strata, including hazard avoidance and contingency routes). |
| **Open Source Repository** | Clean, well-documented source code deposited on GitHub with open-source licensing. |
| **Project Presentation / Video** | Standard Space Apps project pitch deck and optional 30-to-240-second demonstration video summarizing the solution. |

---

## Official Challenge Resources Cited by NASA

The official challenge page references the following verified NASA and USGS resources:

1. **Jet Propulsion Laboratory’s (JPL) Mars Trek:**  
   [https://trek.nasa.gov/mars/](https://trek.nasa.gov/mars/)  
   *NASA’s flagship web-based GIS portal for Mars surface exploration, providing access to dozens of mission layers and landing site dossiers.*
2. **USGS-NASA Planetary Geologic Mapping Program:**  
   [https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars](https://astrogeology-usgs.hub.arcgis.com/pages/interactive-maps-mars)  
   *Standardized, peer-reviewed planetary geologic maps providing structural and stratigraphic context.*
3. **Curiosity Rover Proposed Route up Mount Sharp:**  
   [https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/](https://science.nasa.gov/resource/curiositys-proposed-path-up-mount-sharp/)  
   *NASA visualization demonstrating annotated waypoints, scientific target zones, and traverse corridors across complex topography.*
4. **NASA Worldview:**  
   [https://worldview.earthdata.nasa.gov/](https://worldview.earthdata.nasa.gov/)  
   *NASA Earthdata satellite visualization architecture showcasing intuitive time-series and multi-layer satellite compositing.*
5. **Mars Perseverance Raw Images Gallery:**  
   [https://mars.nasa.gov/mars2020/multimedia/raw-images/](https://mars.nasa.gov/mars2020/multimedia/raw-images/)  
   *Over one million raw and calibrated surface images from Mars 2020 navigation, hazard, and science cameras.*

