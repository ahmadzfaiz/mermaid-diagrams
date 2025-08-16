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

## 5. FlowChart with SubGraph
```mermaid
graph TD
    %% Define nodes
    from_sheet1[\From fa:fa-file-lines Sheet 1: Consider a more advanced method/]
    normal_dist{Are data normally distributed with no outliers?}
    transform[Transform the data and/or remove outliers]
    second_order{Do the data meet second-order or intrinsic stationary?}
    success{successful?}
    sheet2[Go to sheet 2]
    spatial_trend{Are spatial trends of interest?}
    detrending[Conduct data detrending]
    success2{successful?}
    second_correlated{Are there secondary correlated data available?}
    correlogram[Construct the correlogram, or variogram]
    cross_correlogram[Construct the cross-correlogram, or cross-variogram]
    anisotrophy{Does the data exibit anisotrophy?}
    crossval_stats{Do cross-validation statistics support the fitted model?}
    revisit[Revisit experimental variography or consider simple or more complex methods. Return to sheet 1]
    optimize_sample{Do you want to optimize sampling design?}
    use_result[Use the result of correlograms and variography results]
    to_sheet4[\Consider using an advanced method. Go to Sheet 4/]

    %% Define subgraph
    subgraph DataDistribution
        examine_dist[Examine data distribution and outliers.]
        note_examine_dist[Note: Data should be standardized to perform conditional simulation and factorial kriging.]
        examine_dist -.- note_examine_dist
    end

    subgraph Kriging
        universal_kriging["Consider using: universal kriging, or kriging with external drift (KED)"]
        note_kriging[Both methods, krige the trend and spatial correlation components simultaneously. KED also uses secondary data. You must still construck a correlogram or variogram for these method]
        
        universal_kriging -.- note_kriging
    end

    subgraph Variography
        variography_omnidir[Use variogram fitting with omnidirectional variography]
        variography_dir[Use variogram fitting with directional variography]
        note_variography["`
            **Note: Variography**
            - Often several models are tested
            - mean error and mean standardized error are close to zero
            - Variance error and variance of standardized error are close to 1
            - Rho value between predicted fits is close to the bisector
            - Residuals are uncorrelated
        `"]

        variography_omnidir -.- note_variography
        variography_dir -.- note_variography
    end

    %% Define a class-based styling
    classDef process fill:blue
    classDef decision fill:orange,color:black
    classDef next fill:green
    classDef note fill:pink,color:black

    class examine_dist,transform,detrending,universal_kriging,correlogram,cross_correlogram,variography_dir,variography_omnidir,use_result process
    class normal_dist,success,second_order,spatial_trend,success2,second_correlated,anisotrophy,crossval_stats,optimize_sample decision
    class from_sheet1,sheet2,revisit,to_sheet4 next
    class note_examine_dist,note_kriging,note_variography note

    %% Define main workflow
    from_sheet1 --> DataDistribution --> normal_dist
    normal_dist --Y--> second_order
    normal_dist --N--> transform
    transform --> success
    success --Y--> second_order
    success --N--> sheet2
    second_order --Y--> spatial_trend
    spatial_trend --N--> detrending
    spatial_trend --Y--> Kriging
    detrending --> success2
    success2 --N--> Kriging
    second_order --Y--> second_correlated
    success2 --Y--> second_correlated
    second_correlated --N--> correlogram
    second_correlated --Y--> cross_correlogram
    correlogram --> anisotrophy
    cross_correlogram --> anisotrophy
    anisotrophy --N--> variography_omnidir
    anisotrophy --Y--> variography_dir
    Variography --> crossval_stats
    crossval_stats --N--> revisit
    crossval_stats --Y--> optimize_sample
    optimize_sample --Y--> use_result
    optimize_sample --N--> to_sheet4
```

Chart inspiration source:
- [Flow Charts for Choosing Geospatial Methods](https://gro-1.itrcweb.org/flow-charts-for-choosing-geospatial-methods/)
- [Source full resolution chart image](https://gro-1.itrcweb.org/wp-content/uploads/2016/10/gro_flow_chart_4of4_10_26_16.png)

## 6. FlowChart with Animation
```mermaid
graph TD
    %% Define nodes
    from_sheet3[\From Sheet 3: Consider using an advanced method/]
    answer_quest{Can you answer your question osing only spatial mean and variance?}
    cons_kriging[Consider Kriging]
    cons_sim[Consider conditional simulation method that attempt to reconstruct intrinsic heteroginity, which are favorable for mapping probabilities, uncertainity and risk]
    sim_points[If you are interested in simulating values at points, then]
    sim_area[If you are interested in simulating values at a predefined area or volume, then]
    est_points[If you are interested in estimating values at points, then]
    est_area[If you are interested in estimating values at a predefined area or volume, then]
    sample_avail1{Are secondary sampled data available to generatespatial simulation?}
    sample_avail2{Are secondary sampled data available to generatespatial simulation?}
    sample_avail3{Are secondary sampled data available to generatespatial simulation?}
    sample_avail4{Are secondary sampled data available to generatespatial simulation?}
    cons_sim_points[Consider point conditional simulation methods]
    cons_cosim_points[Consider point conditional co-simulation methods]
    cons_sim_blocks[Consider block conditional simulation methods]
    cons_cosim_blocks[Consider block conditional co-simulation methods]
    cons_kri_points[Consider point kriging methods]
    cons_cokri_points[Consider point co-kriging methods]
    cons_kri_blocks[Consider block kriging methods]
    cons_cokri_blocks[Consider block co-kriging methods]

    %% Define a class-based styling
    classDef process fill:blue
    classDef decision fill:orange,color:black
    classDef next fill:green
    classDef note fill:pink,color:black

    class cons_kriging,cons_sim,sim_points,sim_area,est_points,est_area,cons_cosim_points,cons_sim_points,cons_sim_blocks,cons_cosim_blocks,cons_kri_points,cons_cokri_points,cons_kri_blocks,cons_cokri_blocks process
    class answer_quest,sample_avail1,sample_avail2,sample_avail3,sample_avail4 decision
    class from_sheet3 next

    %% Define main workflow
    from_sheet3 a1@--> answer_quest
    answer_quest a2@--N--> cons_sim
    answer_quest --Y--> cons_kriging
    cons_sim --> sim_points
    cons_sim ac1@--> sim_area
    cons_kriging --> est_points & est_area

    sim_points --> sample_avail1
    sample_avail1 --N--> cons_sim_points
    sample_avail1 --Y--> cons_cosim_points
    
    sim_area a3@--> sample_avail2
    sample_avail2 a4@--N--> cons_sim_blocks
    sample_avail2 --Y--> cons_cosim_blocks

    est_points --> sample_avail3
    sample_avail3 --N--> cons_kri_points
    sample_avail3 --Y--> cons_cokri_points
    
    est_area --> sample_avail4
    sample_avail4 --N--> cons_kri_blocks
    sample_avail4 --Y--> cons_cokri_blocks
    

    %% Define animation setup
    a1@{ animation: slow }
    a2@{ animation: fast }
    a3@{ animation: fast }
    a4@{ animation: fast }

    %% Class-based animation setup
    classDef animate stroke-dasharray: 9,5,stroke-dashoffset: 900,animation: dash 25s linear infinite;
    
    class ac1 animate
```

Chart inspiration source:
- [Flow Charts for Choosing Geospatial Methods](https://gro-1.itrcweb.org/flow-charts-for-choosing-geospatial-methods/)
- [Source full resolution chart image](https://gro-1.itrcweb.org/wp-content/uploads/2016/10/gro_flow_chart_3of4_10_26_16-1.png)
