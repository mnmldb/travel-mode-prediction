# Travel Mode Prediction

## Overview

Understanding and predicting travel mode choices of citizens are essential in transportation planning and policy-making in cities. An accurate machine learning model to predict the travel mode with limited available information would be helpful for the public and private sectors. Also, understanding which features are important is useful because it could make our cost of future data collection less expensive. We framed this problem as a classification task of each trip’s travel mode in the latest national survey. We evaluated the prediction model by accuracy, precision, recall, and F-1 score.

## Report

Click [here](https://github.com/mnmldb/travel-mode-prediction/blob/main/Report.pdf) to see the report.

## Notebook
#### in  `eda `
- `Anomaly_Clustering.ipynb`: Data Preprossesing, Exploratory Data Analysis (PCA), Anomaly Detection, and Clustering (KMeans)
#### in  `model `
- `Interpretable_Models.ipynb`: Classification Models (Bayesian Networks, Random Forest) with Down Sampling and Feature Importances
- `NN_Model.ipynb`: Classification Model (Neural Network) with Down/Over Sampling (SMOTE) and Feature Importances (SHAP)

## Dataset

The dataset for this project is [National Household Travel Survey](https://nhts.ornl.gov/) conducted by the Federal Highway Administration (FHWA) in 2017. It includes 923,572 daily non-commercial travels by all modes, including characteristics of the people traveling, their household, and their vehicles. 
The data is separated into four files as below, and they can be merged with each file’s primary key. There are 244 unique features in total. The file name and major features are listed below. The files can be downloaded [here](https://nhts.ornl.gov/downloads).
   
1. Trip (`trippub.csv`): mode of transportation, trip purpose, date and time, origin and destination, distance
2. Household (`hhpub.csv`): income, number of workers, housing type, neighborhood characteristics
3. Vehicle (`vehpub.csv`): make, model, age (year)
4. Person (`perpub.csv`): gender, age, driver and worker status, annual miles

## Data Preprocessing
Our target variable (`TRPTRANS`) consists of the 24 travel modes in total, including walk, bicycle, motorcycles, car, SUV, van, amtrak, subway, boats, airplanes. We grouped the modes into two labels; 1 for environmentally friendly modes (walk, bicycle, bus, amtrak, and subway) and 0 for other motorized vehicles. 

## Result

### Classification Performances
The below table shows the classification performances of all approaches. Neural Network with the optimized loss function was the best model, and we could achieve more than 0.8 of the F1 score.

![classfication_performances](https://user-images.githubusercontent.com/47055092/138004876-d6697b50-8e22-4a30-b060-d78002d83183.png)

### Feature Importances
The below table shows the top feature importances from different approaches. In addition to Neural Network and Random Forest, we created 2 clusters of trips by KMeans except for the target variable and computed the difference of each cluster’s feature average. We thought the more significant difference could be a proxy for feature importances.

![feature_importances](https://user-images.githubusercontent.com/47055092/138005012-a2a43d5a-1b2f-4fe0-9ba6-b89b3c27651b.png)

The density of housing and population in origin and destination were commonly critical in all models. Loop trip, which indicates the trip has the same origin and destination, was significantly used by Random Forest and Kmeans. Compared to Random Forest and KMeans, Neural Network captured feature importances uniquely. Neural Network utilized age, home-base trip flag, and trip weight, which is essential for travel mode choice but is not well captured by Random Forest and KMeans.