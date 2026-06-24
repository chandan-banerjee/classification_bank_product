# Requirement   : Dataset is from a Tele-marketting campaign of a Portuguese banking institution for their different TERM deposite products.
#               : The goal is --> To predict if a client wil subscribe to their product. 

# ***GIT HUB REPO link***

Please use the following link to access my repository



# **Key observations/ Summary**

# **Phase EDA (Exploratory Data Analysis) & Feature Engg:**
    1. Call Duration has minimal impact on predictive modeling. Didn't consider this attribute and removed rows where 'duration' is ZERO and target is 'no'. 
    2. Used OrdinalEncoder for better correlation heatmap visualization. OneHotEncoder creates too many features which makes the heatmap unreadable. OrdinalEncoder creates less features which makes the heatmap more readable.
    3. Compared between bank-additional-full.csv and bank-additional.csv dataset to identify class imbalance, if any. Result indicates both have similar class imbalance. Used the full dataset as I need to evaluate models' performance. 
                        proportion
                    y	
                    no	0.887346
                    yes	0.112654
    4. Renamed few features  like ('cons.price.idx' to 'consumer_price_index') for better understanding and readability
    5. Segrigated numerical & categorical features for scaling and categorical data in numeric format
    6. Check the number of unique values in each categorical feature. This will helped me to understand the cardinality of the categorical features and to decide which encoding technique to use for each categorical feature.
    7. Ccurrent dataset does not have null values and each feature has its own significance/ contribution. Hence no need to additional dereived column for this usecase  modelling.
    8. As the target variable is binary in nature, we will use LabelEncoding for the target variable.

# **Phase Modelling**

    1. Used pipeline,column transformer & gridsearchCV to review performance and key hyper parameter values
    2.  Option 1:column selector = PCA. Used n_components=0.9 allowing model to decide the columns to generate 90% of the variance. Bcoz the PCA graph shows more feature needed to reach ~80% cut off value. 
            Best model : Ridge
            cross-validation R^2 score:  0.05499808231558767
            Mean Squared Error with PCA Feature Selection on training set:  30884010930336.04
            Mean Squared Error with PCA Feature Selection on test set:  325986526.57310754
       
        Option 2: colun selector = Polynomial degree 2
            Best model : Lasso
            Best cross-validation R^2 score for polynomial regression:  0.08375309252930645
            Mean Squared Error on training set for polynomial regression:  30883976278358.79
            Mean Squared Error on test set for polynomial regression:  318770548.042995 
        
        Option 3: column selector = Sequential feature selector, n_comonents = 5
            Best model : Ridge
            Best cross-validation R^2 score for sequential regression:  0.05014992530816287
            Mean Squared Error on training set for sequential regression:  30883944114726.297
            Mean Squared Error on test set for sequential regression:  332517267.61842513
    3.  Based on above facts Polynomial with degree 2 is best model as it gives best MSE and R^2 score is good. 

# **Phase Evaluation**

    1. Mocked up data from the original dataset that was given to me for analysis
    2. Used 3 cars data as to mimic a scenario where model never had seen the data before
    3. Used 3 models to predic prices and found polynoial feature selection using Lasso is predicting better. Details are in EVALUATION section of the notebook

# **Conclusion/NxtStep/Recommendation**

    1.  These are NOT the best models. I would say its average. The current state is much better than what I started with. The R^2 score has imporved a lot from negative to greter than ZERO.
    2. Further scope will be do more feature engineering as dataset has lot of data variation
    3. For now checked with few hyperparameter. There is scope to tune parameters for better performance , regularization and improved scores


