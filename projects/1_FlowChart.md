# FlowChart Diagram Syntax

```mermaid
---
title: Geospatial analysis and model development for specific degradation in South Korea using model tree data mining
---
flowchart TB
    %% Define Nodes
    data_collection["`
        **Data collection for the sediment discharge**
        1. Daily discharge (10 yr)
        2. Field sediment data
    `"]

    flow_duration["**Flow duration curve**"]

    sediment_estimation@{ shape: rect, label: "**Estimating Total Sediment discharge (MEP & SEMEP)**" }

    estimate_sd@{ shape: rect, label: "**Estimating Specific Degradation (SD) using FD-SRC**" }

    decision_sd@{ shape: diamond, label: "**Are the result (SD) for 35 points reliable**" }

    decision_sd_no["**Do not use SD for calibaration**"]

    data_collection_gis["`
        **Data Collection for GIS/geospatial analysis**
        1. Watershed characteristics
        2. Satellite images
        3. Aerial photos
    `"]

    developing_model["**Developing models for redicting SD from MEP and SEMEP using model tree**"]

    geospatial_analysis["**Geospatial analysis with Erosion maps using RUSLE Satellite images Aerial Photos**"]

    compare_model["**Compare to the existing empirical models**"]

    decision_result@{ shape: diamond, label: "**Are the result (SD) for 35 points reliable**" }

    sugessting_model["**Suggesting developed model**"]

    %% Main diagram flow
    data_collection --> flow_duration --> estimate_sd
    data_collection --> sediment_estimation --> estimate_sd

    estimate_sd --> decision_sd
    decision_sd --N--> decision_sd_no
    decision_sd --Y--> developing_model
    
    data_collection_gis --> developing_model
    data_collection_gis --> geospatial_analysis <--> compare_model

    developing_model --> decision_result
    decision_result --Y--> sugessting_model
    decision_result --N--> developing_model
```
Chart inspiration source:
- [Geospatial analysis and model development for specific degradation in South Korea using model tree data mining](https://www.sciencedirect.com/science/article/pii/S0341816221000011)
- [Source full resolution chart image](https://ars.els-cdn.com/content/image/1-s2.0-S0341816221000011-gr4.jpg)