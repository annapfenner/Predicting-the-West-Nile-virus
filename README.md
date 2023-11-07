# capstone-project-2

![cover_photo](./Capstone Project2/Images and Plots/west_nile_virus_mosquito.jpeg)

# Predicting West Nile Virus in Chicago

## 1. Data
This Kaggle datasets comes from the comprehensive program the City of Chicago and Chicago Department of Public Health 
have to track the West Nile virus from late spring through fall. 

The datasets used were:
(1) The train dataset contains dates, trap names, locations, number of mosquitoes, if West Nile Virus was present or not, etc. 
(2) This dataset has two weather stations situated at two airports. It includes dates, temperatures, precipitation levels, sunrise and sunset times, and other relevant weather-related metrics.

> * [Kaggle Dataset](https://www.kaggle.com/c/predict-west-nile-virus/)

## 2. Data Wrangling
[Data Wrangling Notebook](https://github.com/annapfenner/capstone-project-2/blob/main/Jupyter%20Notebooks/Capstone%20Project%202%20-%20Data%20Wrangling.ipynb)

**The training dataset:**
1. Converted the date object column to datetime format. 
2. Collapsed the species categorical column to a binary numeric column to species that do not carry the virus (0) and species that do carry the virus (1). 
3. Kept the latitude and longitude columns of the trap location and dropped the other address columns.
4. Dropped trap names. 
5. Assigned each trap location to one of the two stations in the weather dataset based upon which one was closer in distance. 

**The weather dataset:**
1. Imputed values for the missing values in various columns. 
2. Dropped columns that had half to all missing values. 
3. Replaced values that represented trace amounts, ‘T’, to 0.005. 
4. Changed the numeric columns that were categorized as objects to either ‘int’ or ‘float’.

Merged the two datasets on date and station column. 

## 3. EDA
[EDA Notebook](https://github.com/annapfenner/capstone-project-2/blob/main/Jupyter%20Notebooks/Project%202%20-%20EDA.ipynb)

During the exploratory data analysis step, different relationships were explored in temperature, precipitation, and humidity across the weeks to identify potential patterns connected with the presence or absence of the West Nile virus.

**Insights found during EDA:**
1. Observed a trend of mosquitoes carrying the West Nile virus exhibited an upsurge beginning around week 32 and reaching their peak between weeks 33-36 
2. Discernible pattern emerged when plotting a 14-day average temperature shift across the weeks. Showed a pattern for the rise of mosquitoes (with and without the West Nile Virus) when temperatures ranged between 23 to 26 degrees Celsius.
3. In the training data, 120,520 observations did show the presense of the West Nile Virus whereas 14,519 observations showed the presense of the West Nile Virus. 

## 4. Feature Engineering
[Feature Engineering Notebook](https://github.com/annapfenner/capstone-project-2/blob/main/Jupyter%20Notebooks/Project%202%20-%20EDA.ipynb)

Mosquitoes thrive in drought-like weather. This makes the water in the standing water become richer with organic matter which contains mosquitoes eggs. Mosquitoes are active at night. 

**New columns added to the dataset:**
1. Created a binary column if it had not rained that day (0) or if it had rained that day (1). 
2. Created a relative humidity column. 
3. Shifted three columns (average temperature in Celsius, precipitation, and relative humidity) by 7, 14, 21 days to see how previous weather affected the number of mosquitoes with the West Nile virus. 
4. Two columns were added based upon how much daylight and nighttime there were for each day. 

## 5. Modeling
[Pre-processing, Training, and Modeling Notebook](https://github.com/annapfenner/capstone-project-2/blob/main/Jupyter%20Notebooks/Project%202-%20Pre-processing%2C%20Training%20%26%20Modeling.ipynb)

**Maching Learning Algorithms used:** XGBoost Classification and Random Forest Classification. 

**Hyperparamter Tuning used:** GridSearchCV from Scikit Learn package and Hyperopt pacakge. 

**Metrics used to find best model:** ROC AUC score and ROC Curve. 

**Analysis:** SHAP package used to extract best features from the best model.  

## 6 Best Model
[Best Model found in Pre-processing, Training, and Modeling Notebook](https://github.com/annapfenner/capstone-project-2/blob/main/Jupyter%20Notebooks/Project%202-%20Pre-processing%2C%20Training%20%26%20Modeling.ipynb)

**Best Model:** The XGBoostClassifier with HyperOpt for hyperparameter tuning.

**ROC AUC score:** 0.8180. 

**SHAP Analysis:**  The top features for the predicting the model were number of mosquitoes, sunrise, amount of daylight time, sunset, week, year and average temperature.

## 7. Future Improvements
Future work could include the following:
1. Remove the "number of mosquitoes" feature as could significantly streamline the West Nile Virus prediction process for the City of Chicago and Department of Public Health. 
2. Manipulate the existing dataset features by shifting them over various days, such as sunrise, sunset times, and daylight duration. 
3. Include additional data from other years. 

