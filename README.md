# final_capstone_project
README code has the clear summary and major findings from the analysis and link to the Python code file.

#### Business understanding of problem
A company wants to create a predictive maintenance solution to reduce costs.
The solution will use machine learning to predict device failures.
The goal is to minimize false positives and false negatives.

Main Objective
The data set aims to precisely predict the RUL of a filter. The data set contains training and test data, each with 50 life tests. The test data contains randomly right-censored run-to-failure measurements and the respective RUL. The main challenge is how to make the most use of the right-censored life data.

Business Impact
The company benefits from making most use of the filters to avoid frequent replacements. 

Data set Creator:
Hochschule Esslingen - University of Applied Sciences
Research Department Reliability Engineering and Prognostics and Health Management
Robert-Bosch-Straße 1
73037 Göppingen
Germany

Kaggle link:
https://www.kaggle.com/datasets/prognosticshse/preventive-to-predicitve-maintenance/data

Dataset Citation:
Hagmeyer, S., Mauthe, F., & Zeiler, P. (2021). Creation of Publicly Available Data Sets for Prognostics and Diagnostics Addressing Data Scenarios Relevant to Industrial Applications. International Journal of Prognostics and Health Management, Volume 12, Issue 2, DOI: 10.36001/ijphm.2021.v12i2.3087

Summary of the findings:

1. The filter failure occurs when the differential pressure across the filter exceeds 600 Pa. Looks like there are 5 readings in the dataset where differential pressure exceeds 600 Pa. 

2. The flow rate appears to remain constant overtime. There are 2 different flow rates observed - about 60 m^3/s and ~80 m^3/s.

3. The dust feed in both train and test data contains a distribition with various particles sizes. 

4. The correlation matrix indicates there is a weak correlation between flow rate and remaining useful life. There a negative correlation between dust feed and the remaining useful life and differential pressure & RUL. 

5. For selecting the best ML model, 4 different models (Linear Regression, Support Vector, Random Forest, and KNN) were explored and the mean absolute error was estimate. The Random forest algorirm has the lowest (~1.0062).

6. A parameter grid consisting of bootstrap, max_depth, n_estimators and max_features was build to select the best hyperparameters for the random forest model. The gridsearchCV on random forest result in following best parameters:
RandomForestRegressor(max_depth=10, max_features='sqrt', n_estimators=200)

7. The tuned model has the train MAE: 2.58 and test MAE: 4.66. The actual and predicted values of differential pressure overtime appear to match well. 

8. A confusion matrix was build to estimate the number of false positive and false negative for the tuned model. The model has the recall score of 94 % and precision of 85% for predicting the near failures accurately. 

9. The ROC-AUC curve for the tuned random forest model has AUC of 98%.

10. A RNN model with 28146 parameters was built, it consist's of 4 LSTM layers with dropout after each and a single dense layer of 26 parameters. The activation is linear and the mae and mse are used as metrics. The main purpose of the model is to predict the remaining useful life of the sensors using the last 'n' observations as inputs. The model is fitted on the training data and tested on the validation dataset. 

11.The RNN model achieved a mse = 934 and mae = 16.85 (on training data) and mse=247, mae=13.9 (on the validation data).

Conclusion: 
The random forest model appears to make a better prediction of differential pressur then RNN model (using LSTM). Both Random Forest and RNN models could be used predict the RUL of a filter and plan pro-active maintenence event before the filter reaches end of life. 

Next steps and recommendations:
Improve the accuracy of RNN model by adding more epochs and with multiple dense layers at the output. Use techniques learned in the course such as data augumentation and drop out with better fine tuning of the layers and number of parameters to achieve lower loss and error in prediction of remaining useful life (RUL) of the filter.


Link to jupyter notebook:
/capstone_project/CapstoneProject_Predictive_Maintenance.ipynb

Link to the dataset:
/capstone_project/data
