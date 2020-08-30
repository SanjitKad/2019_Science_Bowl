# 2019 Science Bowl
This Kaggle hackathon aims to forecast the number of attempts a child would take to clear a particular assesment. These assesments are a part of the PBS KIDS Measure Up app where children of ages 3-5 are taught some basic STEM concepts and evaluated on various levels and acitivities. The forecasting is done on the game analytics data that has been anonymously recorded from the past.


# Stages of the Submission :
## 1. Data loading and pre-processing:
The data provided by the competition is a collection of game analytics of features containing the details about the activities being played and how long each individual had taken for each activity. As a result of unpacking the JSONs of event data and args from the specs.csv of each avitivity, the initial dataframe has over 900 features. At this stage manually going through each of the features to find the most important/relevant ones for the predictor would be nearly impossible. This rules out using visualizations like pair plots to eliminate correlated or redundant features. It would also be really difficult to gain information by individually going through each of the numeric features and their distributions due to the sheer number of them.

To deal with this problem, first the columns with high corelations are analysed and removed. This helps remove a lot of redundant features which could cause the problems for model as it would give more importance that required to a feature due to the presence of multiple redundant columns. Columns with more than 95% correlation are reduced to a single column. 

Additionally, if the distribution of columns vary drastically in the train and test splits (the means of the the features in the train and test sets) they would negatively contribute towards the performance of the model. So they are removed. In this case the performance on the hackathon is prioritized. However in the real world in this type of a situation the data would be actually have to be strengthened using techniques like data augmentation to make the predictions generalized based on that particular column further. 
The features are reduced down to about 600 after these stages.

The next stage of feature engineering involves Permutation Importance. This is a technique where the model is trained on all the existing features and each feature is tweaked a little to determine the impact of this on the model. The existing features are then listed in order of importance in this scenario. After this, a threshold was manually set to consider the number of features (trial and error) for the final training. The number of features can be chosen based on the tradeoff between fit and performance that is required.

## 2. Model Training and evaluation

