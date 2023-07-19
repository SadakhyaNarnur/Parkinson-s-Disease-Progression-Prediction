# Parkinson's-Disease-Progression-Prediction
Predicting the progression of the disease using protein and peptide data using CNN-LSTM.

It is estimated that over 1.6 million people in the United States will be living with
Parkinson’s disease (PD) by 2037, with an associated economic cost of nearly $80 billion. PD is
a debilitating neurological disorder that interferes with bodily functions such as movement,
cognition, and even sleep. Worst of all, there is no cure for this progressive disease. Studies point
to abnormal proteins or peptides as the key players in the onset and advancement of PD. While
the entire list of proteins responsible for PD is yet unknown, those proteins having predictive
significance are worthy of further investigation (Parkinson's Foundation. (n.d.)). The goal of this
research is to forecast the trajectory of PD in patients using protein abundance values obtained
from cerebrospinal fluid (CSF) samples gathered from PD patients over several years; each
sample is accompanied by a PD severity evaluation that was taken at the time of the CSF sample.
Ultimately, this research aims to predict MDS-UPDRS scores, a metric used to track the
development of PD in patients by monitoring motor and nonmotor symptoms. Leveraging a
combination of strategic data preprocessing techniques and deep-learning modeling technologies
like CNN-LSTM and MLP, this research predicts the progression of PD using patient protein and
peptide-level time-series data. The models are evaluated using MSE, MAE and SMAPE scores.
This study may assist in landing a breakthrough cure for PD, relieving the physical, emotional,
and financial suffering associated with the condition.

Dataset Description:
The data provided is a sequence of measurements collected over several years from
cerebrospinal fluid (CSF) samples of Parkinson's disease (PD) patients. The measurements
represent the quantity of proteins present in the CSF samples, and each sample is linked to an
evaluation of PD severity at the time the CSF measurement was taken. The dataset has four data
files namely: train_peptides, train_proteins, train_clinical_data and supplemental_clinical_data.
All these have three common columns visit_id, patient_id and visit_month that can be used to
merge these together. The train_peptides dataset has six columns which can be seen in Table 1
data from mass spectrometry at the peptide level.

Data Preprocessing and Cleaning:
Standard Scalar
StandardScaler is useful in data preprocessing because it aids in data normalization,
making it easier for prediction. Scaling the data ensures that features with big values do not
dominate over characteristics with small values, perhaps resulting in bias towards such features.
StandardScaler also aids in reducing the impact of data outliers.StandardScaler is a data
preparation method for standardizing numerical values in a dataset. It scales and centers the data,
resulting in a mean of 0 and a standard deviation of 1. To accomplish this, subtract the mean
from each data point and divide by the standard deviation. In the MLP model, we chose the
target variables to normalize for the better prediction.
KNN Imputation
KNN imputation uses the K-Nearest Neighbors technique to fill in missing values in a
dataset. KNN imputation estimates missing values by looking at the K nearest neighbors of the
observation with missing values. The approach computes the distance between the missing-value
observation and other non-missing-value observations in the dataset. The K nearest neighbors are
then used to estimate the missing value by taking the average, median, or mode of their
values.When there are missing values in a dataset, it is preferable to impute those missing values
rather than deleting the entire observation.The dataset retains more information and can be used
for additional analysis when missing values are imputed. Because it is non-parametric and does
not require any assumptions about the distribution of the data, KNN imputation is frequently
favoured over other imputation methods. KNN imputation can also be utilized with mixed data
types (continuous and categorical variables). The code applies KNN imputation to the train_df
DataFrame's target columns. The n_neighbors parameter is set to 15, indicating that missing
values are filled in by the 15 closest neighbors.After filling in the blanks, the code applies a
maximum function to the imputed values and sets negative values to zero. This is followed by
the np.expm1 function, which returns the data's natural logarithmic transformation to its original
scale. Finally, the modified and imputed values are appended to the target columns in the train_df
DataFrame.

Data Transformation:
Principal Component Analysis (PCA)
Principal Component Analysis (PCA) is a popular dimensionality reduction technique
that converts a high-dimensional dataset into a lower-dimensional space while keeping the
majority of the original dataset's information. It is an unsupervised machine learning technique
that produces a set of new variables (referred to as principal components) that are linear
combinations of the original characteristics.PCA is essential because it can assist in simplifying
data complexity, lowering dimensionality, and thereby minimizing noise and redundancy in the
data. This makes the data easier to perceive, comprehend, and manipulate. It can also aid in the
identification of the most essential features or variables in the dataset, which can be beneficial in
feature selection for machine learning models. Furthermore, PCA can aid in the identification of
correlations and patterns in data, which can aid in the identification of linkages between distinct
aspects and the prediction of outcomes based on these associations. We had 286 columns for the
training dataset. However, to build a predictive model will make it complicated. Thus, by trial
and error method we chose and narrowed down to 10 principal components to help identify the
progression of the disease.
Min-Max Scaling
MinMax scaling is a method of adjusting the range of independent variables or features in
a dataset, known as feature scaling. It is a process of normalizing feature values to a
predetermined range, which is usually between 0 and 1. To achieve this, the method subtracts the
minimum value of the feature from each value and divides by the range of the feature. It is
beneficial because it maintains the original feature distribution shape while keeping the feature
values within a fixed range. This feature scaling method is useful for machine learning models
that are sensitive to the input feature scale, like K-nearest neighbors and neural networks.
Min-max scaler is used for transforming the train, validation and test data before applying the
model.

Conclusion:
To the best of our knowledge, this is the first study to investigate the usefulness of a
hybrid CNN-LSTM model in predicting PD disease progression in patients using protein and
peptide abundance data. The model’s performance was compared to a baseline MLP model
enhanced with preprocessing techniques. The contributions of this study were the following:
First, the study proposed a CNN-LSTM model that can predict a patient’s UPDRS scores for a
given future visit by taking the inputs of previous visits, leveraging temporal patterns in
historical peptide abundance data. Second, the model is adaptive over time, as it has been trained
using varying visit time intervals and different number of visits. Third, the feature-extracting
mechanism of the CNN-LSTM model was compared to a baseline MLP model enhanced with
PCA feature extraction. Overall, the proposed hybrid CNN-LSTM model showed promising
results. These findings suggest the potential of using protein and peptide abundance data in
predicting PD disease progression, which can ultimately lead to more personalized and effective
treatments for patients.
