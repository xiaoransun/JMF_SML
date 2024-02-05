# Supervised Machine Learning for Exploratory Analysis in Family Research

Documentation of programming scripts for the empirical example on adolescents' family experiences as predictors of young adult educational attainment with machine learning, based on Add Health data. <br>
Paper <i>in press</i> at <i>Journal of Marriage and Family</i>. <br>
Author: Xiaoran Sun, at University of Minnesota, Twin Cities
<br>

The purpose of this GitHub repository is:
* To share the codes for data pre-processing, machine learning models training and testing, and visualization for the paper, thereby other researchers can replicate this study.
* To provide pedagogical explanations, step by step, for how we conducted the analyses for this paper. Researchers should be able to use our codes to conduct machine learning research with their own substantive research interests and research questions.
* To facilitate post-publication communication. If you have any questions regarding our paper, analysis or codes, feel free to post in the 'Issues' section of this repository and we will try our best to answer your questions.

### Step 0: Getting prepared for data processing.
This paper uses public dataset (Wave I and Wave IV) of National Longitudinal Study of Adolescent Health (Add Health). To conduct analyses with the data, please first download the data following their instructions at: https://www.cpc.unc.edu/projects/addhealth/documentation/publicdata
<br>
I followed the instructions to download data from [ICPSR](https://www.icpsr.umich.edu/icpsrweb/ICPSR/studies/21600?archive=ICPSR&q=21600).
<br>
<br>
The particular datasets used in this study are listed below. You can find the 'Download' option under the 'Data & Documentation' tab at the ICPSR data repository.
* DS1 Wave I: In-Home Questionnaire, Public Use Sample
  * I used both the R and SPSS versions of the data because the SPSS version has more information regarding the missing data pattern.
* DS22 Wave IV: In-Home Questionnaire, Public Use Sample
  * I used the R version for this data.
* DS31 Wave IV: Public Use Weights
  * I used the R version for this data.

For a detailed description of this sample, please refer to the **Sample** section in the manuscript.
<br>

### Step 1: Pre-processing the data.
This step includes:
* Selecting and creating the identified family variables from the raw data
* Missing data imputation, with
  * mean imputation for the legitimate skips
  * single imputation based on `missForest` for the remaining missingness.
* Selecting and creating the educational attainment variable.
* Preliminary analysis for descriptives (weighted).
* Preliminary analysis for the OLS regression.

See `01_DataPreProcessing.rmd` for detailed instructions, codes and annotations. <br>

Descriptions of this procedure can also be found in the **Measures**, **Data preparation**, and **Preliminary Analyses** sections in the manuscript.
<br>

### Step 2: ML analysis
This step includes:
* Tuning, training, and testing lasso regression, decision tree regressor, random forest regressor, and XGBoost models in predicting educational attainment with the family experience variables.
  * Tuning uses 5-fold cross-validation within the training set; uses the random search strategy to search for optimal hyperparameters for each algorithm.
  * Calculating MSE and R^2 for each algorithm predicting each outcome.
* Compute feature importance of all the predictors in the random forests mdoels (i.e., the best performing model).
* Conduct backward feature selection to identify the set of predictors that remained in models with model performance equivalent to the original model that included all predictors.
* Use the SHAP method to interpret the random forests model.
  * Calculate SHAP values;
  * Visualize single predictor patterns;
  * Visualize force plots for individual cases;
  * Visualize interactions.
 

See `02_ML_analysis.ipynb` for the code (python code; in Jupyter markdown).

This step corresponds to the **Method--Supervised ML Analyses** section in the manuscript.
<br>






