# Requirement   : Dataset is from a Tele-marketting campaign of a Portuguese banking institution for their different TERM deposite products.
#               The goal is --> To predict if a client will subscribe to their product. 

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
    5. Segrigated numerical & categorical features. Used standar scaling for numerical feature. 
    6. Check the number of unique values in each categorical feature. This will helped me to understand the cardinality of the categorical features and to decide which encoding technique to use for each categorical feature. Used OncHotEncoder for categorical feature.
    7. Current dataset does not have null/missing values and each feature has its own significance/ contribution. Hence no need to create additional dereived column for this UseCase.
    8. As the target variable is binary in nature, used LabelEncoding for the target variable transformation.

# **Phase Modelling**

    1. Used pipeline,column transformer, Target transformer & gridsearchCV to review performance and key hyper parameter values
    2. GridSearch indicates decisiontreeclassifier has better test score and performing (fit time )well 
        	                        train score	test score	average fit time
            model			
            KNN	                    0.925183	0.884788	15.790351
            logisticregression	    0.900416	0.899964	0.607916
            svc	                    0.897715	0.896686	498.780488
            decisiontreeclassifier	0.902935	0.900571	0.603124
    3. Recall score

                model	                recall_score
            0	KNN	                    0.303879
            1	logisticregression	    0.218750
            2	svc	                    0.201509
            3	decisiontreeclassifier	0.250000
    3.  GridSearch indicates best model is  {'decisiontreeclassifier__max_depth': 5} and max_depth =5. This indicates no overfitting. Still there is room to evaluate how we can improve recall score.
# **Phase Evaluation**

    1. Recall score is important for Bank Telemarketting campaign because the goal is to find every potential customer willing to buy a term deposit.
    2. Adjusting the threshold from 0.5, the default value, to 0.26 improves the recall score from 0.25 to 0.55 for decision tree classifier

        Optimal F1-score threshold: 0.2626
        Recall at optimal F1-score threshold: 0.5517
        Precision at optimal F1-score threshold: 0.4881

    3. As I see class imbalance, tried Synthetic Minority Over-sampling Technique (SMOTE). This helps in balancing the dataset and can lead to improved model performance, especially in terms of recall for the minority class.

                        --- Results with SMOTE ---
                                            train score	test score	fit time
                    model			
                    KNN	                    0.901478	0.784388	100.901024
                    logisticregression	    0.820894	0.828457	5.884878
                    svc	                    0.834826	0.838533	3233.937716
                    decisiontreeclassifier	0.876832	0.881874	9.267540

                    --- Recall scores with SMOTE ---
                    model	                    recall_score
                    0	KNN	                        0.574353
                    1	logisticregression	        0.657328
                    2	svc	                        0.619612
                    3	decisiontreeclassifier	    0.554957

# **Conclusion/NxtStep/Recommendation**

    1.  
    2. Further scope will be do more feature engineering as dataset has lot of data variation
    3. For now checked with few hyperparameter. There is scope to tune parameters for better performance , regularization and improved scores


