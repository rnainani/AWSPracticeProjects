# Deploy-MachineLearningModel-with-Amazon SageMaker

### Steps followed :

1) Create a new Notebook Instance 
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/556bab21-0964-47da-b015-679d8c3db80f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/99d8a8f2-1def-46d6-add4-4a3c7661ba20)

Create a new role needed for this new Notebook Instance creation :
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b41100c0-c65c-498e-b7f5-1352e8c9d71a)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/42143aec-0997-44a2-bc39-be170beeacd5)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d25d6703-eb34-4e68-99d2-b6c16697e44a)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5d3e112a-6620-4cff-be20-56bc5f746640)

2) Click on Open Jupyter & choose python3, rename it

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4b65d859-d29e-40e0-a5bf-a86dd2bf5d93)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/406a5c54-a0fb-4af2-a354-cd41ac600083)

Install SHAP library by running the following conda command:

%conda install -c conda-forge shap

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0472711b-1902-4c70-ba4d-62d8e4c21886)

Load Adult Census Dataset Using SHAP
Using the SHAP library, import the Adult Census dataset as shown following:

import shap
X, y = shap.datasets.adult()
X_display, y_display = shap.datasets.adult(display=True)
feature_names = list(X.columns)
feature_names

The feature_names list object should return the following list of features:

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/abcd1cdc-05c1-4fa4-b0da-ba0967a2616e)

Overview the Dataset
Run the following script to display the statistical overview of the dataset and histograms of the numeric features.

display(X.describe())
hist = X.hist(bins=30, sharey=True, figsize=(20, 10))

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b3fdeedb-f1cc-4aac-a6dd-3115a530ca28)
