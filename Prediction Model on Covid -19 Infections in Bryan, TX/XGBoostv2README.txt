XGBoost Model Version 2
Filename: RunXGBoostv2.ipynb		(Jupyter Notebook)
Model File: xgboostModelv2.pkl		(XGBoost Model)
Training File: trainDataXGBoost.csv	(csv file) (Same as original)
Test File: finalTestData.csv		(csv file) (data manipulated like trainDataXGBoost.csv)

=====Required Packages=====
xgboost
scikit-learn
pandas
numpy
matplotlib
joblib

========CHANGE LOG=========
-More intensive hyperparameter tuning. No existing hyperparameters have been changed or removed.
	-Added the following hyperparameters
		-subsample
		-colsample_bytree
		-colsample_bylevel
		-gamma
-Added early_stopping_rounds (and set it to 25)
-Split training data set to training, validation, and testing data sets to use 
 early_stopping_rounds

=====Brief Description=====
XGBoost, or "Extreme Gradient Boosting", is a ML algorithm that uses gradient boost trees.
It has become popular amongst the ML algorithms due to its speed and robust feature-selecting
methods. It is a supervised learning algorithm and is useful for both regression and 
classification. In this case, we used it for the purpose of regression.

======Important Note=======
The data file format must be in ".csv" format. The data set has also been transformed. The
Date column has been deleted, removing the time series aspect of the data set. The empty slots
with "NA" have been filled with the respective columns' mean value. Lag columns have also 
been added to every influx column in the original data set.

=====Parts of the code=====
--Load Model and Test--
This section allows the user to load the existing XGBoost Model to analyze the COVID-19
Hospitalization data set. The first cell has to be run to import all the required packages
to run the entire code. (SOME PACKAGES MAY NEED TO BE INSTALLED VIA "!pip" COMMAND)

There is a segment where it mentions where you can run your own data through the ML model.
To do this, in the second cell, replace "trainDataXGBoost.csv" with your own csv file.
After this, the dataset will split the predictors from the response variable (separating
"Hospitalizations" from the other columns).

After this, a model will be loaded, and it will show its coefficient values through a plot.

Finally, using RMSE, MSE, and MAE, it will display the model's performance.

------Build Model-------
This section shows the model building process. As mentioned before, XGBoost was used to 
create the model.

The dataset is first taken in and split into a training data set and a validation data set
(8:2 ratio). A d matrix is also created for xgb.

After this, we first fit the XGBoost model with the training data. Afterward, we tune the
hyperparameter using RandomizedSearchCV. This function allows us to automatically and 
intensively search through every possible combination of the listed hyperparameters.

After this, the code shows a plot of the coefficient values, showing the importance of
features in order (from greatest to least). 

The code then shows the results on the training and the validation data sets, measuring
their performance with RMSE, MSE, and MAE.

In the end, the code outputs the model in a (.pkl) format.