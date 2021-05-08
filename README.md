# Dissertation
The Comparative study of Machine Learning model prediction using COVID-19 Dataset from “NovelCorona Virus 2019 Dataset” that can be found in
Kaggle(https://www.kaggle.com/sudalairajkumar/novel-corona-virus-2019-dataset).
This experiment performed the testing of three classification algorithms: Ensemble of a subset of
kNN classifiers (ESkNN), Ensemble of optimal trees (OTE), and Support Vector Machine and focus
on the prediction output which is the death or survived in COVID-19 patients data. We wish
to apply each method by integrating it with the visualization technique to find the best classifier
that can predict the death of COVID-19 patients using R program.

1) Data preprocessing
As we know that the COVID-19 data contains numeric and string variables, those categorical variables
needed label-encoding or in other words, transformed from text to a number. This procedure was performed in the Python program, using sklearn.preprocessing package to responsible for the encoding step. With “LabelEncoder”, the string variables location, country, symptom1,
symptom 2, and symptom 3 are replaced by a number. This is applied to gender variable similarly, the number 1 represents “male” while 0 represents “female”. Then export encoded data as a .csv file to use in the next step. 

2) Missing value
After encoding the categorical data into numbers, we check our data for the missing value. The missing data map created by using ggplot function in R represents the three variables that contain missing values or NA. The variable with the most missing data is a number of days before going to the hospital (46.39 %) while gender and ages lost not much information. Even the missing valuenof variable days before going to the hospital quite large but it is one of our interesting features with
the amount of missing not exceed 50 % we handle it with the imputation method. The technique we use for our missing data is in the Amelia package. This package uses a ‘multiple imputation’ technique to impute the missing values. This function works when the data is a numerical factor, this is why the encoding procedure is needed in the previous step.
The amelia function imputes all missing data with m runs. For this experiment we choose m equal to 5, each runs creating an imputed set. Thus we got 5 imputed data sets as a .csv file contained different impute data that are going to be tested to find the most reasonable one. Then perform analysis models for each data set by passing the imputed data sets through Zelig function. From the output, compare 5 analysis models to find the one that contained the lowest standard deviation in predicted value. 

3) Model experiment
Pperform an analysis using three machine learning algorithms with COVID-19 patient data. The reason for cross-validation is to tuning the parameters to be optimal and give the most effective prediction. One of our models which is ESkNN is associated with kNN classification. Finding the appropriate number of parameter k is important since it can
easily affect the model’s performance. The estimation of the proper value k is performing by ten-fold cross-validation. The “trainControl” function from caret
package is used to control the computational variation of the train function. The trainControl function uses to perform cross-validation by setting the method as “cv” and also set a number of folds equal to 10. With function “train”, it sets up a framework of tuning parameters for both classification and regression. In our case we select the method to be “knn”, the function will fit the kNN model using our train fold from trainControl function and calculates a resampling based performance measure. For ESkNN and OTE we create a cross-validation function for them and splitting dependent and independent features. For Support Vector Machine, we perform cross-validation by “svm” function from e1071 package.

4) evaluation and confusion matrix
The model’s efficient estimation can be measure by accuracy and evaluation metrics. For ESkNN and EOT the function generate an output of error rate which we can estimate as an accuracy rate by subtracting the error rate from 1. Another usage of error rate is to compute the standard deviation of our set of errors using sd function. Standard deviation can be used as a measurement of uncertainty. We also considered the confusion matrix which is used to estimate the efficiency of prediction. The confusion matrix allows observing three evaluation metrics which are precision, recall, and F1 score. These scores use to describe the performance of a classification model.

5) Result
The result provided an accuracy of prediction and confusion matrix, below is the confusion matrix of the best prediction from each model which we used to calculate precision, recall, and F1 score. All scores are plot into the bar chart which is easy to observe the difference of values between models.
OTE achieves the most accuracy with 95.65 % followed by 92.34 % for SVM and 90.45 % for ESkNN. For precision which is the ratio of correctly predicted death observations
to the total predicted death observations the model that achieves the highest score is SVM with value 1. The ratio of correctly predicted death observations to all observations in the actual death class of death is Recall wich ESkNN and OTE achieve the highest ratio of 1. The F1 score is a weighted average between Precision and Recall, it takes both false positives and false negatives into account. The highest F1 score is OTE with 0.933.
