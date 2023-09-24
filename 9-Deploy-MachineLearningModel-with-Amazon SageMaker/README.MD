# Deploy-MachineLearningModel-with-Amazon SageMaker

## Steps followed :

### 1) Create a new Notebook Instance 
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/556bab21-0964-47da-b015-679d8c3db80f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/99d8a8f2-1def-46d6-add4-4a3c7661ba20)

Create a new role needed for this new Notebook Instance creation :
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b41100c0-c65c-498e-b7f5-1352e8c9d71a)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/42143aec-0997-44a2-bc39-be170beeacd5)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d25d6703-eb34-4e68-99d2-b6c16697e44a)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5d3e112a-6620-4cff-be20-56bc5f746640)

### 2) Click on Open Jupyter & choose python3, rename it

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4b65d859-d29e-40e0-a5bf-a86dd2bf5d93)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/406a5c54-a0fb-4af2-a354-cd41ac600083)

Install SHAP library by running the following conda command:

%conda install -c conda-forge shap

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0472711b-1902-4c70-ba4d-62d8e4c21886)

### 3) Download, Explore, and Transform a Dataset

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

Split the Dataset into Train, Validation, and Test Datasets
Using Sklearn, split the dataset into a training set and a test set. The training set is used to train the model, while the test set is used to evaluate the performance of the final trained model. The dataset is randomly sorted with the fixed random seed: 80 percent of the dataset for training set and 20 percent of it for a test set.

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1)
X_train_display = X_display.loc[X_train.index]

Split the training set to separate out a validation set. The validation set is used to evaluate the performance of the trained model while tuning the model's hyperparameters. 75 percent of the training set becomes the final training set, and the rest is the validation set.

X_train, X_val, y_train, y_val = train_test_split(X_train, y_train, test_size=0.25, random_state=1)
X_train_display = X_display.loc[X_train.index]
X_val_display = X_display.loc[X_val.index]

Using the pandas package, explicitly align each dataset by concatenating the numeric features with the true labels.

import pandas as pd
train = pd.concat([pd.Series(y_train, index=X_train.index,
                             name='Income>50K', dtype=int), X_train], axis=1)
validation = pd.concat([pd.Series(y_val, index=X_val.index,
                            name='Income>50K', dtype=int), X_val], axis=1)
test = pd.concat([pd.Series(y_test, index=X_test.index,
                            name='Income>50K', dtype=int), X_test], axis=1)


Check if the dataset is split and structured as expected:

train

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2d298fd1-0664-479d-aa71-ea11b72b2c3a)

validation

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6fd49c32-67b1-4d2d-88b5-4c16b55df7c8)

Convert the train and validation dataframe objects to CSV files to match the input file format for the XGBoost algorithm.


# Use 'csv' format to store the data
# The first column is expected to be the output column
train.to_csv('train.csv', index=False, header=False)
validation.to_csv('validation.csv', index=False, header=False)

Upload the Datasets to Amazon S3
Using the SageMaker and Boto3, upload the training and validation datasets to the default Amazon S3 bucket. The datasets in the S3 bucket will be used by a compute-optimized SageMaker instance on Amazon EC2 for training.

The following code sets up the default S3 bucket URI for your current SageMaker session, creates a new demo-sagemaker-xgboost-adult-income-prediction folder, and uploads the training and validation datasets to the data subfolder.


import sagemaker, boto3, os
bucket = sagemaker.Session().default_bucket()
prefix = "demo-sagemaker-xgboost-adult-income-prediction"

boto3.Session().resource('s3').Bucket(bucket).Object(
    os.path.join(prefix, 'data/train.csv')).upload_file('train.csv')
boto3.Session().resource('s3').Bucket(bucket).Object(
    os.path.join(prefix, 'data/validation.csv')).upload_file('validation.csv')
Run the following AWS CLI to check if the CSV files are successfully uploaded to the S3 bucket.


! aws s3 ls {bucket}/{prefix}/data --recursive

This should return the following output:

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dce8ef09-117c-459a-a703-7d6321e7d88f)

### 4) Train a Model

Create and Run a Training Job

Import the Amazon SageMaker Python SDK and start by retrieving the basic information from your current SageMaker session.

import sagemaker
region = sagemaker.Session().boto_region_name
print("AWS Region: {}".format(region))
role = sagemaker.get_execution_role()
print("RoleArn: {}".format(role))

This returns the following information:

region – The current AWS Region where the SageMaker notebook instance is running.
role – The IAM role used by the notebook instance.


Create an XGBoost estimator using the sagemaker.estimator.Estimator class. In the following example code, the XGBoost estimator is named xgb_model.


from sagemaker.debugger import Rule, ProfilerRule, rule_configs
from sagemaker.session import TrainingInput

s3_output_location='s3://{}/{}/{}'.format(bucket, prefix, 'xgboost_model')

container=sagemaker.image_uris.retrieve("xgboost", region, "1.2-1")
print(container)

xgb_model=sagemaker.estimator.Estimator(
    image_uri=container,
    role=role,
    instance_count=1,
    instance_type='ml.m4.xlarge',
    volume_size=5,
    output_path=s3_output_location,
    sagemaker_session=sagemaker.Session(),
    rules=[
        Rule.sagemaker(rule_configs.create_xgboost_report()),
        ProfilerRule.sagemaker(rule_configs.ProfilerReport())
    ]
)


Set the hyperparameters for the XGBoost algorithm by calling the set_hyperparameters method of the estimator.

xgb_model.set_hyperparameters(
    max_depth = 5,
    eta = 0.2,
    gamma = 4,
    min_child_weight = 6,
    subsample = 0.7,
    objective = "binary:logistic",
    num_round = 1000
)

Use the TrainingInput class to configure a data input flow for training. 

from sagemaker.session import TrainingInput

train_input = TrainingInput(
    "s3://{}/{}/{}".format(bucket, prefix, "data/train.csv"), content_type="csv"
)
validation_input = TrainingInput(
    "s3://{}/{}/{}".format(bucket, prefix, "data/validation.csv"), content_type="csv"
)

To start model training, call the estimator's fit method with the training and validation datasets. By setting wait=True, the fit method displays progress logs and waits until training is complete.

xgb_model.fit({"train": train_input, "validation": validation_input}, wait=True)


<<< Project needs further updates. >>>
