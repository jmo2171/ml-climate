We are trying to predict next day wildfire spread using stuctural causal models to compare its preformance to previously used ml methods like deep neural nets, random forests, and logistic regression.

Ary's Editted version (Discuss and replace the above):

Most literature on wildfire risk assessment centers around using correlative models to predict regions with high risk of wildfire spread. We develop a set of causal models to predict wildfire spread in the Western half of continental united states. First we compare our causal models (used along with the latest climate models) to the state of the art correlation based models to understand how well our models performs. Next we select the models with the best performance to understand how different environmental variables affect the risk of wildfire spread. Finally, we conduct various interventions on the system to estimate the ways in which corrective actions affect wildfire risk amongst all the top performing causal models to derive both upper and lower bounds on how intervention of different kinds relate to the risk of wildfire spread. With reference to data on project costs, we determine the most cost effective ways to reduce the risk of wildfire spread.

Our paper only models risk as a linear function of the variables. Further research can be used along with domain knowledge to determine which variables have non-linear effects on the risk of wildfires. To this effect, our model is intended to provide a first order estimate of the effect of interventions on the risk of wildfires. Our model should not be used to predict the effect of interventions in the long run, only for the near future.

Data: Next Day Wildfire Spread: https://ieeexplore.ieee.org/abstract/document/9840400
    "This “Next Day Wildfire Spread” dataset is a curated, largescale, multivariate dataset of historical wildfires over nearly a decade across the United States"
