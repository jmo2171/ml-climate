2/14
Discussed possible project ideas. 
Some Ideas:
- Mumbai particulate matter (Testing different CNN models/Finetuning to predict PM2.5 and PM10 in Mumbai and other cities in India)
- coral reefs
- forest fires

technical topics in syllabus:
cnn
predictive vs causal models
conterfactual analysis using data
structural causal discovery
non convex optimatiztion w constraints
bayesian optimation
reinforcement learning
diffusion models
carbon footprint quantification
large language models

2/22
Our idea for project. 
Wild fire next day burn area prediction using casual models. 
We found this dataset https://ieeexplore.ieee.org/abstract/document/9840400 
https://www.kaggle.com/datasets/fantineh/next-day-wildfire-spread/data 
description of dataset from paper
        This “Next Day Wildfire Spread” dataset is a curated, largescale, multivariate dataset of historical wildfires over nearly
        a decade across the United States, aggregated using Google
        Earth Engine (GEE) [16]. This dataset takes advantage of the
        increasing availability and capability of remote-sensing technologies, resulting in extensive spatial and temporal coverage
        from a wide range of sensors (e.g., the Moderate Resolution
        Imaging Spectroradiometer (MODIS) [17], the Visible Infrared
        Imaging Radiometer Suite (VIIRS) [18], and the Shuttle Radar
        Topography Mission (SRTM) [19]). Our dataset combines
        historical wildfires with 11 observational variables overlaid
        over 2-D regions at 1 km resolution: elevation, wind direction,
        wind speed, minimum temperature, maximum temperature,
        humidity, precipitation, drought index, vegetation, population
        density, and energy release component (ERC). The resulting
        dataset has 18 545 fire events, for which we provide two
        snapshots of the fire spreading pattern, at time t and t +1 day

possible extension:
    comparing prediction of burn data with historical weather/earth conditions with the same data for predicted future earth models

Next steps:
    confirm scope of our project with teaching staff
    find literature to learn more about forest fire causes and influences and background
    revist biodiversity paper to get an idea for how to set up scm

3/10

Looked extensively for causal model link assumptions. Found the following paper:https://arxiv.org/html/2403.08414v1 which includes candidate causal graphs for he meditteranean region but nothing for the US. This paper includes causal effects of OCI factors such as el nino etc. which will be completely differnt for out case. We can maybe assume that such factors are unobserved for the US use case and use the candidate graphs for the remaining factors in the paper.
