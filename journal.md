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


3/14
We've started working on accessing our data. The dataset is in the form of .trecords which makes it convenient to load with tensorflow. The variables we have available are elevation, wind direction, windspeed, max temp, min temp, humidity, precipitation, drought index, vegetation, population density, energy release component and previous fire mask for different points in space at different times. our hope is to use this data set to create a causal model of where the fire will spread on the next day. By iteratively repeating this process the hope is to create a prediction for how the fire spreads over the course of several days and determine patterns that lead to the fire dying. Since we will probably need a linearity assumption in determining the causal relationship strength between variables, we will have a first order prediction which is likely to get significantly more and more inaccurate as one uses it repeatedly to look farther in the future.

We are considering using TensorFlow Causal Impact to conduct our analysis and test interventions in the form of different average (we will change min and max temperature by the assumed change in average) temperatures, precipitation, humidity, vegetation cover (we can estimate the effects of fire lines, etc.), and population density.

We are currently evaluating a priority order for the different sources of input from the data to determine which ones we will use for our final model and which ones we may exclude. The next step is to implement and train a basic SCM and test its performance.


3/25

We had a long conversation about how we would tackle the next steps of our project. We determined that the bottleneck we were facing was coming up with a meaningful DAG that was backed by literature. We came up with the following plan:

Aryaman will comb through the dataset and format the data using pandas in an accessible manner. Additionally, he will build a regression based predictor for wildfire spread. Jenny will conduct research on the best Python libraries/techniques to create DAGs and SCMs. We have identified that tensorflow is a good baseline to use, especially since our data is already in .tfrecord but we want to keep an eye out for better libraries. Jenny will also look into whether there is anymore literature to find more causal assumptions backed by literature.

Finally we discussed using conditional independencies in the data columns to create one or more skeleton(s) of DAG model(s). We could use all the assumptions we've found from the literature (we have already found a small set from one paper, we will look for more) to orient these skeletons. The result will be a few DAG models (we are aiming for 3-5). We will use the validation set to construct a benchmark. We will also compare these DAG models with the regression model as another benchmark. 

We beleieve we have a suitable path to complete this project, the big missing piece is the construction of the DAGs which we have a plan to acheive.


4/1

Created a google colab notebook with the necessary code to load the dataset (derived from the database creator's code). the creator of the dataset included some handy code to select random samples of the data as well as to crop out random samples of the given dataset. There are still some issues such as the fact that it doesn't seem like the previous fire mask variable is loading correctly but this may only appear to be the case due to the random croppings taken.

Adendum: After some further testing it seems the issue with loading the previos firemask was caused by randomly selecting and cropping out a subset of the whole sample area. This may be rectified by discarding samples that do not have any fires in the previous fire mask or by not cropping any of the samples before using them.

