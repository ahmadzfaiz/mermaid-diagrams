# FlowChart Diagram Syntax

## 1. Left-Right Simple FlowChart
```mermaid
flowchart LR
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
```

## 2. Top-Down Simple FlowChart
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

    sediment_estimation["**Estimating Total Sediment discharge (MEP & SEMEP)**"]

    estimate_sd["**Estimating Specific Degradation (SD) using FD-SRC**"]

    decision_sd{"**Are the result (SD) for 35 points reliable**"}

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

    decision_result{"**Are the result (SD) for 35 points reliable**"}

    sugessting_model["**Suggesting developed model**"]

    %% Main diagram flow
    data_collection --> flow_duration & sediment_estimation --> estimate_sd

    estimate_sd --> decision_sd
    decision_sd --N--> decision_sd_no
    decision_sd --Y--> developing_model
    
    data_collection_gis --> developing_model
    data_collection_gis --> geospatial_analysis --- compare_model

    developing_model --> decision_result
    decision_result --Y--> sugessting_model
    decision_result --N--> developing_model
```
Chart inspiration source:
- [Geospatial analysis and model development for specific degradation in South Korea using model tree data mining](https://www.sciencedirect.com/science/article/pii/S0341816221000011)
- [Source full resolution chart image](https://ars.els-cdn.com/content/image/1-s2.0-S0341816221000011-gr4.jpg)

## 3. FlowChart with Styling
```mermaid
---
title: Selecting a Geospatial Method - Sheet 1
---
flowchart TB
    %% Define nodes
    start((start))
    optimization[Consider optimization questions to answer]
    meet_req{Does the data set meet the min data req's}
    add_sample[Consider additional sampling]
    perform_analysis[Perform exploratory data analysis]
    show_correlation{Does the variables show spatial correlation?}
    nonspatial_stats[Consider using nonspatial statistical methods]
    dense_sample{Is the variable densely sampled?}
    simple_method[Consider using a simple method]
    error_analysis{Do you want to do detailed error analysis}
    complex_method[\Consider using a more complex method. Go to Sheet 2/]
    advanced_method[\Consider using a more advanced method. Go to Sheet 3/]

    %% Styling nodes
    style start color:green
    style optimization fill:blue
    style meet_req fill:orange,color:black
    
    %% Define class-based styling nodes
    classDef process fill:blue
    classDef decision fill:orange,color:black
    classDef next fill:green
    
    class add_sample,perform_analysis,nonspatial_stats,simple_method process
    class show_correlation,dense_sample,error_analysis decision
    class complex_method,advanced_method next

    %% Define main workflow
    start --> optimization --> meet_req
    meet_req --N--> add_sample
    meet_req --Y--> perform_analysis
    perform_analysis --> show_correlation
    show_correlation --N--> nonspatial_stats
    dense_sample --N--> simple_method
    show_correlation --Y--> dense_sample --Y--> error_analysis
    error_analysis --N--> complex_method
    error_analysis --Y--> advanced_method
```
Chart inspiration source:
- [Flow Charts for Choosing Geospatial Methods](https://gro-1.itrcweb.org/flow-charts-for-choosing-geospatial-methods/)
- [Source full resolution chart image](https://gro-1.itrcweb.org/wp-content/uploads/2016/10/gro_flow_chart_1of4_10_26_16.png)

## 4. FlowChart with FontAwesome Icons
```mermaid
graph TD
    %% Define nodes
    from_sheet1[\From fa:fa-file-lines Sheet 1: Consider a more complex method/]
    pred_error{fa:fa-xmark Do you need a prediction error estimate?}
    splines_kernel[Consider using splines or kernel smoothing method]
    second_correlated{fa:fa-pen-to-square Are there secondary correlated data available?}
    non_parametric[Consider using a nonparametric method]
    regression[Perform regression and examine residuals for spatial correlation]
    regression_significant{fa:fa-globe Do the regression residual show significant spatial correlation}
    parametric[Consider using a pramateric regression method]
    verify[Verify model fit using cross-validation]

    %% Define a class-based styling
    classDef process fill:blue
    classDef decision fill:orange,color:black
    classDef next fill:green
    
    class splines_kernel,non_parametric,regression,parametric,verify process
    class pred_error,second_correlated,regression_significant decision
    class from_sheet1 next

    %% Define main workflow
    from_sheet1 --> pred_error
    pred_error --N--> splines_kernel
    pred_error --Y--> second_correlated
    second_correlated --Y--> regression
    second_correlated --N--> non_parametric
    regression --> regression_significant
    regression_significant --Y--> non_parametric --> verify
    regression_significant --N--> parametric --> verify
```

Chart inspiration source:
- [Flow Charts for Choosing Geospatial Methods](https://gro-1.itrcweb.org/flow-charts-for-choosing-geospatial-methods/)
- [Source full resolution chart image](https://gro-1.itrcweb.org/wp-content/uploads/2016/10/gro_flow_chart_2of4_10_26_16-1.png)
- [FontAwesome 6.7.2](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css)