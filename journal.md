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

4/14

Very busy with other classes this week.
Current status:
We have the dataset properly loaded.
We have code for our alternative models mainly outlined following the original release of the dataset paper.
We are working with python library PyWhy to implement our causal models. 

4/20
We have spent the week working to see how to implement causal model around the spread data set. The biggest challenge here is working with the geospatial nature of the data. The library we have been working with (and other possible alternatives we found) are based off of tabular (not image like) data. To attempt to solve this problem we tried and considered different ways to convert our image based data into tabular data. Becasue we could not just convert each pixel into a feature without having 12x64x64 predicitve features (too many for scms) we had to reduce the info we considered or map to more summary type data. For example considering information only about the current cell or neighboring cells. Or using convolution kernals to get larger summaries. However this ultimatley wasn't working well at prediciting pixel wise outputs (the t+1 fire mask), becasue the fires spread a lot from one day to the next and also what makes them spread is probably due to not only conditions of current region in t+1 (ie dryness of area) but also conditions in the prior step of where the fire was (ie wind) which may be several cells away. Other summary methods we considered like autoencoders reduce the interpretability of the ultimate model which was a major goal in our project being causal in the first place. 
For this reason we have decided to slightly pivot and change our prediction task to be not same day spread (1x1km prediction) but rather ultimate fire class classification (a measure of how big the fire ultimately burned) from data about the inital fire (fire event prediction). To do this we will be using https://www.kaggle.com/datasets/rtatman/188-million-us-wildfires dataset supplements with data from google earth engine. While our prediction task has changed slightly the implications and technical methods remain the same as our initial proposal. 
We currently are running scripts to augment our dataset with potential variables of interest and then we will use our new dataset with the causal models we were developing for the old prediction since many of the variables are the same. 
We will ultimately compare our causal model to existing ai models like the ones describe here https://www.sciencedirect.com/science/article/pii/S2666592122000373 


[filling since we forget committ our journal previously]

4/27
Conducted causal analysis on both the continuous wild fire size variable as well as the discrete wildfire size class variable which categorises wildfires into ordinal groupings based on their size. As of now we have done a lot of causal graph discovery but haven't found a great graph to describe our problem as yet. We have some graphs that are extremely complicated and make no sense. We also have simpler ones that we posit, however these seem to perform extremely badly with R^2 close to 0. We have only tested these models with linear SCMs at the moment and so it might be necessary to use a more expressive funcitonal model.

We also recorded our video for the presentation in class
We started writing the framework of our paper. 


5/4
We conducted extensive feature analysis and analysed class imbalances in our data to see if these statistics would help us with finding a better graphical model which we could finalise. We also evaluated these new graphs using Linear models, random forest models, XGBoost models and Histrogram Gradient Descent models. DoWhy doesn't seem to be working well with these models. Another limitation of doWhy that we discovered is that it keeps the model parameters private and there is no good way to access them that we have been able to find. 

We recorded our second video


5/11

We found an even better causal graph which we decided to use as our final graph. After retesting linear models, polynomial models, XGBoost and MORD to predict the ordinal fire size class labels and two models with a mix of the aforementioned relationships, we found that that using forms other than linear models usually reduced the model performance. The few methods that improved the model performance did so negligibly and so we decided to stick to using linear models which are significantly more interpretable. Maintaining interpretability was extremelty important for us since that was the main reason for conducting this analysis using causal models.

We conducted validation using a random test-train split. We also split the data based on the year. We found that splitting before vs after 2014 created an almost perfect 80-20 split in the data and so conducted future generalization validation based on this split. Interestingly we found that the model performed better on the generalization split than on the random split. Upon further evaluation, we note that while all fire categories per year increased post 2014, the class A fires saw the biggest increase which worsened our class imbalance in the data. This may explain the improved performance of our model.

After collating our findings we finished writing out our paper.
