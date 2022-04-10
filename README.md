# Credit_Risk_Analysis

## Overview

Supplied with loan statistcs from first quarter 2019, I've been asked to utilize supervised machine learning methods to predict loan risks from variables as loan amount, incomes, verification status, etc.  Because the amount of defaulted or high risk loans is substantially less then low risk loans; resampling techniques are justified to make more meaningful predictions for the lower amount dataset (high risk loans).  Datasets with imbalanced result classes can lead to biased predictions towards the larger class.  This analysis utilizes 6 techniques to explore ways to limit that bias:

  1. **Naive Random Oversampling** - randomly selects instances of high risk loans until the data set used to train the model is equal to the number of low risks instances used to train.  Randomly resuses existing data can duplicate instances.  Instances used my not reflect the actual distruibution of those instances in reality.
  2. **Synthetic Minority Oversampling Technique (*SMOTE*) Oversampling** - size of high risk dataset  is increased by interpolating instances from nearby existing data.  This method uses all of the data and so can be suseptible to outliers, and again the generated data is not real data.
  3. **Undersampling - Cluster Centroids** - reverse of oversampling similar to SMOTE, the low risk loans are reduced to the same size of the high risk dataset by creating interpolated data sets that represent the clusters of actual datapoints for the majority class.  Downside is that the generated data is not real data and may not accurately represent the real distribution.
  4. **Combination (Over and Under) Sampling AKA SMOTEEN** - High risk instances are over sampled with smote, but drops the point if the two nearest nieghbors to the point are from high risk and low risk groups.  This technique limits the overlap from interpolations.  
  5. **Balanced Random Forest Classifier** - Runs like Random Forest that runs data through algorithm branches to increase overall prodiction from weak (typically small data quantity for variable) and strong learners; however, it balances classes by undersampling after each bootstrap iteration.   
  6. **Easy Ensemble AdaBoost Classifier** - Adaptive boosting runs multiple  models.  First it trains a model and then evaluates the models errors and weights the errors to minimize the errors effect for the next model and gain for subsequent models.  This versions balances classes by random under-sampling the majority class (low risk)

## Resources

1. **LoansStats_2019Q1.csv** - loan data for 2019 Q1, not included in repository due to size constraints.
2. **credit_risk_resampling.ipynb** - jupyter notebook contains script for Naive Random Oversampling,SMOTE, undersampling, and SMOTEEN
3. **credit_risk_ensemble.ipynb** - jupyter notebook contains script for Balanced Random Forest Classifier and Easy Ensemble AdaBoost Classifier

## Results

1.  **Naive Random Oversampling**
![image](https://user-images.githubusercontent.com/91850824/162634743-936d48c4-58ed-4c12-8d63-fa9d3ddc5579.png)

  *  Balance Accuracy Score - overall model accurately predicts low and high risk categories 64.4% of instances.
  *  Precision scores - high risk precision 0.01; low risk precision 0.997.  
  *  recall scores - high risk 0.69; low risk 0.59
  *  Result Summary - low precision for high risk categories and low recalls for bothhigh and low categories.  We are predicting around 70% the bad loans; however, we are also calling 41% of good loans high risk.  Low f1 scores for high risk also point to the imbalance of sensitivity and precision for high risk categories.

2.  **SMOTE**
![image](https://user-images.githubusercontent.com/91850824/162634747-6b071bb0-26dc-415a-8fd2-7e75a1549995.png)

  *  Balance Accuracy Score - overall model accurately predicts low and high risk categories 66.3% of instances.
  *  Precision scores - high risk precision 0.012; low risk precision 0.997.  
  *  recall scores - high risk 0.634; low risk 0.692
  *  Result Summary - Simialr results to Random Over Sampling.  Low precision for high risk categories and low recalls for bot hhigh and low categories.  We are predicting around 63% the bad loans; however, we are also calling 31% of good loans high risk.  Low f1 scores for high risk also point to the imbalance of sensitivity and precision for high risk categories.  This miscategorizes more bad loans (5.5%), but correctly identifies 

3.  **Cluster Centroid Undersampling**
![image](https://user-images.githubusercontent.com/91850824/162634751-e8eb9d3a-bdc4-4723-815c-7a2f498ab11c.png)

  *  Balance Accuracy Score - overall model accurately predicts low and high risk categories 54.4% of instances.
  *  Precision scores - high risk precision 0.007; low risk precision 0.995.  
  *  recall scores - high risk 0.693; low risk 0.395

4.  **SMOTEEN**
![image](https://user-images.githubusercontent.com/91850824/162634753-e0364ddd-c712-4ba1-ba22-3ed784509bba.png)

  *  Balance Accuracy Score - overall model accurately predicts low and high risk categories 63.9% of instances.
  *  Precision scores - high risk precision 0.01; low risk precision 0.997.    
  *  recall scores - high risk 0.703; low risk 0.574

5.  **Balanced Random Forest Classifier**
![image](https://user-images.githubusercontent.com/91850824/162634757-0c868998-a9a4-4ede-b469-8a253f8b5436.png)

  *  Balance Accuracy Score - overall model accurately predicts low and high risk categories 78.87% of instances.
  *  Precision scores - high risk precision 0.03; low risk precision 0.998.   
  *  recall scores - high risk 0.703; low risk 0.871
6.  **Easy Ensemble AdaBoost Classifier**
![image](https://user-images.githubusercontent.com/91850824/162634759-f77548fd-cc2b-431d-8064-39e618ae1102.png)

  *  Balance Accuracy Score - overall model accurately predicts low and high risk categories 93.2% of instances.
  *  Precision scores - high risk precision 0.09; low risk precision 0.9995.  
  *  recall scores - high risk 0.92.; low risk 0.94.
  
