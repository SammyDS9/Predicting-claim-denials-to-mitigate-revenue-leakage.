# Predicting-claim-denials-to-mitigate-revenue-leakage.

**Step 1: Data gatherin **

Patient Age: The age of the patient.
Procedure Code: Code representing the medical procedure performed.
Claim Amount: The amount claimed by the provider.
Provider Type: Type of the medical provider, e.g., 'Hospital', 'Clinic', 'Individual'.
Pre-existing Condition: Whether the patient had a pre-existing condition (0 for No, 1 for Yes).
Claim Denied: Whether the claim was denied (0 for No, 1 for Yes).
We'll create a dataset with 10,000 records. (to avoid miss use of actual data)

**Step 2: Exploratory Data Analysis (EDA): **
From the exploratory data analysis, we can observe:
Patient Age: Age appears to be uniformly distributed across all ages.
Claim Amount: The claim amount has a fairly uniform distribution ranging from a little over $100 to nearly $10,000.
Provider Type: The claims are fairly evenly distributed across the three provider types: Hospital, Clinic, and Individual.
Claim Denied: Most of the claims are approved, with a smaller portion being denied. Specifically, 13.65% of claims are denied.

**Step 3: Preprocessing**
Encoding categorical features.
Splitting the data into training and testing sets.
Scaling numerical features.

Numerical features like "Patient Age" and "Claim Amount" have been standardized.
The categorical feature "Provider Type" has been one-hot encoded, resulting in two additional columns (since we dropped the first category). These columns represent whether the provider is an "Individual" or a "Clinic" (with "Hospital" being the dropped category).


**Step 4: Model Training**
For predicting claim denials, we will use a logistic regression model, which is a commonly used algorithm for binary classification tasks. Let's train the model using the training data.
Accuracy: 87.55%

Classification Report:

Precision for Denied Claims (1): 0.00 (The model never predicted a claim to be denied.)
Recall for Denied Claims (1): 0.00 (Of the actual denied claims, none were correctly predicted by the model.)
F1-Score for Denied Claims (1): 0.00
Confusion Matrix: 1751  0
                  249  0
 
This result indicates that the model is struggling to predict denied claims and is favoring the dominant class (approved claims). There's a class imbalance in our dataset (most of the claims are approved, and fewer are denied), which is causing the model to be biased towards predicting claims as approved.

**Step 5: Addressing Class Imbalance**

Resampling: This involves either oversampling the minority class or undersampling the majority class.
Using Different Algorithms: Some algorithms can handle imbalanced data better than others.
Using Different Evaluation Metrics: Instead of accuracy, we can use metrics like the F1-score, precision, recall, or the area under the ROC curve, which give more importance to the minority class.
For simplicity, let's try the first approach: oversampling the minority class using the Synthetic Minority Over-sampling Technique (SMOTE). We'll then train our model again and evaluate its performance.

The performance of the logistic regression model with adjusted class weights on the test data is as follows:

Accuracy: 51.05%

Classification Report:

Precision for Denied Claims (1): 0.13 (Of the claims predicted as denied, only 13% were actually denied.)
Recall for Denied Claims (1): 0.53 (Of the actual denied claims, 53% were correctly predicted by the model.)
F1-Score for Denied Claims (1): 0.21
Confusion Matrix: 889 862
                  117      132

By adjusting the class weights, we have managed to increase the recall for denied claims from 0% to 53%. However, this has come at the expense of precision, which is now quite low at 13%. Additionally, the overall accuracy has decreased. This is a trade-off we often face when dealing with imbalanced datasets, and the optimal balance depends on the specific business contex
