## Hospital IQ Data Science Take Home Exercise

## 1. Instructions for running your Python script locally.
<pre>
(a) Fit a new regression model 
    - command to fit a model: <b>python regression.py 0 directory_path/b_data.json</b>
    
(b) Run previously fitted model and get prediction
    - command to run previously fitted model : <b>python regression.py 1</b>
    - provide input values for Service ID and surgeries in last month for prediction
    - The predicted surgeries in this month will be displayed
</pre> 


## 2. What you would have done prior to fitting the regression model if we didn't assure you that the data were already clean?
<pre>
 Below pre-processing would have been followed in case of raw data:
    - Checking missing data and imputing as per data in specific column and domain
    - Converting categorical data into numerical if the feature is significant
    - Visualization  for outlier data points and removal
    - Checking distribution of data in all columns
    - Checking correlation between feature columns to avoid multicollinearity 
</pre>


## 3. How did you decide on the covariates in your model?
<pre>
    - Plotted the pairplot to visualise the distribution of data and how input features relate with target variable
    - Checked the correlation of between features and target variable to decide which features to keep or remove if multicollinear
    - Built base model using statesmodel library was built to on which feature to keep based on its summary. 
</pre>


## 4. What is your interpretation of the coefficients of the variables in your model?
<pre>
 Checking significance of individual feature for Target variable with T-Test for co-efficient values:
    - age_in_yrs : p-value > 0.05 (not in 95% confidence interval) and T-test score is +ve hence it is not significant for target variable with co-effiticent 0.053
    - service_id : p-value < 0.05 but T-test score -ve hence this feature is giving little significance for target prediction with co-efficient -7.95
    - surgeries_last_month : p-value < 0.05 and T-test score is large (41.41) hence this feature does not have 0 coeffitient. It has good significance for target variable prediction

From above analysis, using only feature 'surgeries_last_month' and 'service_id' for building final model
</pre>


## 5. How well does this model fit the data overall?
<pre>    
  (a) R-squared is close enough to Adjused R-square:
      - Implyies that the model is well fitted
  
  (b) Checking significance of overall regression model i.e. cosidering all features togather for Target variable with F-Test:
      - p-value for F-Test is < 0.05 (withon 95% confidence interval)
      - F-Test score (=577.4) is very high Hence the features used for model building has linear relationship with target variable considering all of them togather
</pre>

## 6. What is the output of RegressionResults.summary? (Nothing other than the raw output of that method is needed.)
 
                                             OLS Regression Results
              ================================================================================
              Dep. Variable:     surgeries_this_month   R-squared:                       0.898
              Model:                              OLS   Adj. R-squared:                  0.897
              Method:                   Least Squares   F-statistic:                     870.1
              Date:                  Sun, 23 Aug 2020   Prob (F-statistic):           1.66e-98
              Time:                          19:40:09   Log-Likelihood:                -949.43
              No. Observations:                   200   AIC:                             1905.
              Df Residuals:                       197   BIC:                             1915.
              Df Model:                             2
              Covariance Type:              nonrobust
              ========================================================================================
                                         coef    std err          t      P>|t|      [0.025      0.975]
              ----------------------------------------------------------------------------------------
              const                   23.1333      6.470      3.575      0.000      10.373      35.894
              service_id              -8.0030      2.504     -3.196      0.002     -12.942      -3.064
              surgeries_last_month     1.2109      0.029     41.663      0.000       1.154       1.268
              ==============================================================================
              Omnibus:                        4.346   Durbin-Watson:                   1.997
              Prob(Omnibus):                  0.114   Jarque-Bera (JB):                2.681
              Skew:                          -0.033   Prob(JB):                        0.262
              Kurtosis:                       2.437   Cond. No.                         494.
              ==============================================================================

              Warnings:
              [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
