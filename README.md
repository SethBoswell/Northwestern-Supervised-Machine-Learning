# Credit_Risk_Analysis

## Purpose of Analysis
This project folder contains two separate Jupyter Notebook files: credit_risk_resampling and credit_risk_ensemble. Credit_risk_resampling preprocesses information about a client's loan application, splits the data into training and testing data, and then performs several resampling techniques designed to address an imbalanced dataset, and runs a standard logistic regression machine learning model to analyze the performance of the different resampling techniques Note that the loan application dataset is imbalanced due to large number of "low-risk" loans and the low number of "high-risk" loans. The logistic regression attempts to predict whether a particular loan application is either low-risk or high-risk based on the myriad of training variables such as loan amount, annual income, the interest rate on the loan. 

First, I used both a naive random oversampling algorithm and then a synthetic minority oversampling technique (SMOTE) algorithm, running both through the logistic regression model. Then I tried using undersampling with a cluster centroid undersampling algorithm and used a combination of over and under sampling with a SMOTEEN (SMOTE + Edited Nearest Neighbors (ENN)) sampling algorithm, running both through the logistic regression model as well. For each sampling technique, I calculated a balanced accuracy score, a confusion matrix, and a imbalanced classification report to analyze the performance of each resampling technique. 

In the Credit_risk_ensemble file, I do the same preprocessing work on the data, split the data into training and test sets, and then run both a Balanced Random Forest Classifier model and a Easy Ensemble AdaBoost Classifier model to see which one performed better. Below, I will discuss the results of the different sampling techniques and the two machine learning models mentioned just above as well as provide a summary of the results and a recommendation on which model to use for predicting credit risk from loan application information.

## Results
### Naive Random Oversampling
* Balanced Accuracy Score

![Random Oversampling Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Random%20Oversampling%20Accuracy.png)

* Confusion Matrix

![Random Oversampling Confusion Matrix](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Random%20Oversampling%20Confusion%20Matrix.png)

* Imbalanced Classification Report

![Random Oversampling Classification Report](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Random%20Oversampling%20Classification%20Report.png)

* Summary Results

The accuracy score of a model depicts what percentage of predictions that are correct. With an accuracy score of 64.7%, random sampling improved the model’s predictive capability above random guessing, but it is still fairly low. 

Precision measures how likely a positive classification is to be true. It is defined as the number of True Positives divided by the sum of True Positives and False Positives, TP/(TP + FP). The random oversampling model was very precise when it comes to accurately predicting low-risk loans with a precision score of approximately 100%, 10,291/(10,291+31), however, it had very poor precision for predicting high-risk loans since it was approximately 1%, 70/(6,813 + 70). 

Sensitivity, or recall, measures the model’s ability to accurately predictive a positive outcome. For example, the ability of this model to correctly classify all low-risk loans as low-risk. It is defined as the number of True Positives divided by the sum of True Positives and False Negatives, TP/(TP + FN). For high-risk transactions, the random oversampling model was moderately sensitive at 69%, 70/(70+31). It was also moderately sensitive for low-risk transactions at 60%, 10,291/(10,291+6,813).

Finally, the F1 score, or harmonic mean, which combines both sensitivity and precision into a single metric, was 2% for high-risk loans and 75% for low-risk, also indicating that the model is good at classifying low-risk loans, but not high-risk. This makes sense since the loan dataset is imbalanced with many more low-risk than high-risk; however, we want the model to do a better job of predicting high-risk loans. Precision is the more important metric in this analysis since we want to be confident that when the model classifies a loan as high-risk, that it is actually high-risk. 

### SMOTE Oversampling
  * Balanced Accuracy Score

![SMOTE Oversampling Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/SMOTE%20Accuracy.png)

  * Confusion Matrix

![SMOTE Oversampling Confusion Matrix](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/SMOTE%20Confusion%20Matrix.png)

  * Imbalanced Classification Report

![SMOTE Oversampling Classification Report](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/SMOTE%20Classification%20Report.png)

* Summary Results

The SMOTE oversampling technique, which works by interpolating new instances of the minority class (instead of randomly selecting instances like in the naïve model), had a slightly higher accuracy score of 66.2%, however, the precision of high-risk loans is still only 1% and the recall of high-risk loans went down to 63% with the harmonic mean staying at 2%. This sampling algorithm did not improve much from the naïve model.

### Cluster Centroids Undersampling
* Balanced Accuracy Score

![Undersampling Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Undersampling%20Accuracy.png)

* Confusion Matrix

![Undersampling Confusion Matrix](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Undersampling%20Confusion%20Matrix.png)

* Imbalanced Classification Report

![Undersampling Classification Report](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Undersampling%20Classification%20Report.png)

* Summary Results

The Cluster Centroids Undersampling algorithm, which works by generating clusters of representative data from the majority class and then shrinking the rest of the majority class data, produced a similarly low precision for high-risk loans, a slightly higher sensitivity, and a lower F1 score. This sampling technique also did not improve on the naïve approach.

### SMOTEENN
* Balanced Accuracy Score

![SMOTEENN Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/SMOTEEN%20Accuracy.png)

* Confusion Matrix

![SMOTEENN Confusion Matrix](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/SMOTEEN%20Confusion%20Matrix.png)

* Imbalanced Classification Report

![SMOTEENN Classification Report](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/SMOTEEN%20Classification%20Report.png)

* Summary Results

The SMOTEENN sampling algorithm, which combines both an oversampling and undersampling strategy, did not improve the precision of the logistic regression at predicting high-risk loans, but it did increase the sensitivity to 78% and the F1 score is still 2%. Although none of the sampling techniques discussed so far lead to significantly improved results over the naïve technique, this one performed the best.

### Balanced Random Forest Classifier   
* Balanced Accuracy Score

![BRFC Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Balanced%20Random%20Forest%20Accuracy.png)

* Confusion Matrix

![BRFC Confusion Matrix](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Balanced%20Random%20Forest%20Confusion%20Matrix.png)

* Imbalanced Classification Report

![BRFC Classification Report](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Balanced%20Random%20Forest%20Classification%20Report.png)

* Summary Results

The Balanced Random Forest Classifier (BRFC) works by creating a number of small, simple decision tree built from a random subset of features. The idea behind this machine learning model is once you combine all of the smaller decision trees into one random forest model, it will produce a strong learning model from a number of weak learners. The BRFC model produced a much higher accuracy score at 78.8%, a higher precision for high-risk loans at 3%, a decent sensitivity at 70%, and a F1 score of 6%. Although still not very precise at predicting high-risk transactions, this model performed better than the logistic regression with the different sampling techniques mentioned previously. 

### Easy Ensemble AdaBoost Classifier
* Balanced Accuracy Score

![Easy Ensemble Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Easy%20Ensemble%20Accuracy.png)

* Confusion Matrix

![Easy Ensemble Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Easy%20Ensemble%20Confusion%20Matrix.png)

* Imbalanced Classification Report

![Easy Ensemble Accuracy](https://github.com/SethBoswell/Credit_Risk_Analysis/blob/main/Images/Easy%20Ensemble%20Classification%20Report.png)

* Summary of Results

The Easy Ensemble AdaBoost Classifier (EEAC) model works by fitting a classifier on the original dataset, and then fitting additional copies of the classifier where the weights of incorrectly classified instances are adjusted to focus on more difficult cases. This is a potentially good classifier since the high-risk loans are difficult to pick up on due to the imbalance in the dataset. 
With an accuracy score of 93.1%, a high-risk loan precision of 9%, sensitivity of 92%, and F1 of 16%, this model is by far the best classifier that we have seen. My main concern is that the precision of high-risk loans remains low – there’s only a 9% chance that a loan predicted to be high-risk is actually high-risk.



## Summary

### Summary of Results

The summary of each sampling algorithim and classifier in included above. Overall, all of the models had a low-level of precision for high-risk loans, which we care the most about. If there's less than a 10% chance that a loan predicted to be high-risk is actually high-risk, than our models fail to accurately classify them. None of the sampling techniques improved the results to a considerable degree, with only very slight improvements coming from the SMOTEENN sampling algorithm. The Easy Ensemble AdaBoost Classifier did by far the best job of modeling high-risk loans, however it still had a precision of 9%. 

### Recommendation

I would not recommend using any of these models to predict credit risk due to the inability to accurately predict high-risk loans. The number of False Positives is too high, meaning there's a good chance we could deny a loan to someone who is not high-risk. Because of the fallibility of the models tried here, I would recommend trying other machine learning models and sampling techniques to adjust for the imbalance in the dataset. That said, the EEAC model performed the best by far. 
