# Ardius ToS Signup Convertion Rate Prediction model
This model consists of three sub-models: 

  1. Random Forest Model for providing conversion prediction for companies who answer survey but didn't sign
  
  2. Random Forest Model for providing conversion prediction for companies before answering survey
  
  3. Logistic Regression Model for Causal Inference using the companies 
  
For questions, contact @phi.nguyen@gusto.com
  
## 0. Data Process
For a more detailed summary of the collected features (across 8 categories), please refer to https://docs.google.com/spreadsheets/d/1Gar1z0Nm9rp_fiYAsj6Ib2u8veq75fGeAa4pT6LER1I/edit#gid=0 or https://redash.zp-int.com/queries/49248

Important notes: Job title related features - currently we are using an open source job title classifier to classify the job titles into 4 categories 0: Business, 1: Other, 2:Sales-Marketing, 3:Technical, and the features we created are job_title_perc_x (percentage of the x type job titles for the company among all the job titles, i.e. the composition of the firm structure). Use test_functions.py for the classification. In the future need better classification models. 

Please refer to the 'transformation' function defined under best_models.ipynb for details how we dealt with the missing data case by case. 

'feature_final_select' are the top 25 features that we eventually focus for model 1 and 3. For model 2, delete features like 'created_at','is_consulting_True', 'qualification_status_highly_qualified', and 'source_lead_gen', which come from survey questions. 

## 1. Model Experimentation and Feature Selections

Some preliminary explanation about model experimentation and feature selection:

For Steps and methodology used: 

EDA: Correlation Matrix (deleted features of high correlation); Variance Check (Deleted features with low variance, ex. constant values); Distribution Check (Check whether the distribution for features is imbalanced) 

Transformation: Imputing Missing Values by different cases; OneHotEncoder (or get dummy) for categorical variables; Further variable transformation such as normalization of features based on length of time. 

Feature Selection: By Actionability; by RFE or SelectKBest; By Robustness Check (due to limited data, model or features selected change over different random split), such as Cross Validation; frequency of the features the selected using different random splits of Training/Testing; Bootstrapping Method; SHAP values; adding Randomized Gaussian variable as benchmark). 

Models used for Experimentation: SVM, Random Forest, Naive Bayes, XGBC, first-order and second-order Logistic Regression. 

Hyper-parameter tuning using GridSearchCV

## 2. Simple version of the model: 

Use logistic_implementation function defined in best_models for Model 3. 

Use rfc_implementation function defined in best_models for Model 1. 

Use rfc_implementation_before function defined in best_models for Model 2. 
  
  
