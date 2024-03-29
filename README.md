# SF Bay Area Bike Share Kaggle Group Project

By Jeffrey Li, Shriya Karam, Sindhura Mente

Last Updated: December 12, 2022

![Map](/img/map.png)

Dataset: [SF Bay Area Bike Share](https://www.kaggle.com/datasets/benhamner/sf-bay-area-bike-share)

## Motivation

In this project, we leverage data analytics tools and machine learning algorithms to understand the San Francisco Bay Area Bike Share data provided by Kaggle. Since its launch in 2013, the Bay Wheels Bike Share Program has provided affordable and accessible transportation across the San Francisco Bay Area. The regional bicycle sharing system partners with local government agencies and corporations like Lyft and currently has over 7000 traditional and electric bicycles at 550 stations.

In this project, we want to extract insights from the data and produce reliable models that can aid Bay Wheels in making decisions regarding bike share network expansion. The ultimate objective is to predict bike share trip durations for a given day, based on features such as weather conditions, station characteristics, and time. We focus on trip duration as an indicator of trip intensity (i.e. how long a trip is is a measure of how intensely the individual used bike share on their given trip). Being knowledgeable about the factors involved in predicting intensity of usage is important for ensuring Bay Wheels’ system is accessible to all and serves as a resilient mode of tansportation. Ultimately, by determining key factors of trip intensity, we seek to advise Bay Wheels on particular areas for system expansion and enhancement.

Through our exploration, we study internal and external factors that impact bike share trip durations and uncover trends across both location, time, and weather-related factors. To understand relationships between stations and key trip factors, we first use k-means clustering as an unsupervised learning method. We consider both regression and classification-based models given we have real inputs and want to predict trip durations as a continuous variable or as a categorical binary variable (i.e., short and long trips). We employ grid search cross-validation for hyperparameter tuning in order to improve our classification model and also present our final models.

## Conclusion

### EDA
Our exploratory data analysis was able to uncover some key trends in our data among bike share trips, stations, and other weather and time related features.

First, from our plots comparing the distributions of trip durations between customers and subscribers, we found that trips taken by subscribers were taken at low intensity (shorter duration), while customers took much more intense trips (longer trip duration), which may indicate more leisure trips. This provides some insight into the fact that short trips may correspond to work commutes, while long trips may correspond to leisure travel.

From the k-means clustering results, we were able to find several groupings of stations that exhibit similar trends in total trip counts and average trip duration per station. Most notably, we found that the University and Emerson station in Palo Alto has the most intense usage (highest average trip duration) so further enhancements can be directed towards accomodating this trip intensity.

We were able to further explore this station and the trips in Palo Alto in our classification model. From our EDA, we also found the largest variation in weather events and time of day by trip duration for the city of Palo Alto, which was a good candidate to narrow our scope down for the classification models.

### Regression
As discussed in our Analysis of Models section under Regression, our regression models to predict bike share trip duration were underperforming. Despite conducting a variety of regression models, hyperparameter tuning to improve the model performance, and additional feature engineering, we attributed our underperforming models due to our models underfitting our data. One major challenge that we faced in training a regression model was the fact that we were using categorical features to predict a continuous variable, bike share trip duration. To deal with this issue, we had to do to 2 major things: 1) implement classification models and 2) focus on one specific city to implement our model with additional feature engineering for the specific location. We discussed this process in more detail in the Analysis of Models section under Regression.

### Classification
In our classification models, we wanted to predict whether a bike share trip would be classified as short vs. long, or in the multiclass class, short vs. long vs. intermediate in Palo Alto. We considered several types of models including binary logistic regression, support vector machines, random forest classifiers, neural networks, and multiclass logistic regression. We found that binary logistic regression and support vector machines were best suited to predict short vs. long trips with around an 81% accuracy and high F1 scores. Some of the challenges associated with our classification problem was that we had to determine the threshold based on our own understanding of the data, as trip duration was a continuous value. Additionally, we did not find any significant correlations between trip duration and the numerical feature data, so we only had categorical features. In the end, our model was able to predict whether trips can be classified as short vs. long in Palo Alto with a resonable degree of accuracy (81%) and good model robustness, as evidenced by the high F1 scores. With this information, we can inform Bay Wheels on potential characteristics that would impact trip intensity, thus providing them with the knowledge to expand their system and services using targeted enhancements within the Palo Alto area.

## Future Work
In our future work, there are several things we would plan to do to further address some of the limitations in our work.

Gather additional feature data: In the data set provided, we were provided with trip characteristics, weather, and station-level features. While these certainly provide an array of features to select from, we want to further pursue other options, including gathering individual-level data and variables as discussed in the Analysis of Models section under Regression. This could entail potential traveler characteristics, trip activity type (leisure vs. work), as well as origin-destination characteristics about each trip. Using these features, we could run additional models that could allow us to predict certain types of trips based on station, weather, individual, and trip-level characteristics.

Implement the model for multiple cities: While the classification model predicts short vs. long trip durations in Palo Alto only, we note that this model and pipeline can be generalized to any city in our data set. In future work, we would want to implement this model for more cities and increase the model's usefulness.

Perform threshold tuning: In generating the labels for the binary and multiclass classification, we used the median of our bike share trip durations to create the cutoff, as well as terciles to create cutoffs for the multiclass models. While the median seemed to perform okay, the multiclass model could benefit from additional threshold tuning. For the multiclass model, we could explore adding more categories of trips (for example, short, short-medium, medium-long, long) to further classify trip durations. While there is not a standard method to establish a treshold, we took the appropriate considerations to ensure class imbalance and model robustness.

More complex machine learning methods: As we suffered from underfitting, especially in the linear regression case, we could potentially consider more complex models such as feed-forward neural networks or boosting methods to improve model complexity and address underfitting. However, this may not be guaranteed to provide better results.