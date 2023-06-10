# Backup one S3 Bucket Content to Another S3 Bucket Using Lambda Function

## Agenda - Create a highly available architecture to automatically replicate the contents of one S3 bucket to another S3 bucket in another region.

### Steps followed :

### 1)	Create an S3 source Bucket & a destination bucket in 2 different region

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c618dba4-6b76-498c-aff6-c31ef9207156)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/00b89f4c-a028-495d-b2f9-e37a9101cd08)

### 2)	Create the Lambda Function & add the code for copying

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ff9255eb-2f12-4504-8766-d24652025a14)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8dc17543-72cd-4c62-8ce5-2a00ef863cec)

### 3)	Add Trigger

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f712ba52-abcb-4bc6-8a89-10b47958d0c5)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3cd257a3-4925-4b0a-bbac-62b196c87df7)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2c035454-4242-4986-a4ba-a13b6e28dc52)

### 4) Provide AWS Identity and Access Management (IAM) permissions for the Lambda function's execution role

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c56427ba-2979-40f0-a29f-b6e20abf768f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dcf38f18-5811-4027-b23b-9f0329085153)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/60b64b6b-a26a-44bd-b36f-ea88111f52d9)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e5c94dfb-43f6-4cd0-8de5-5cf33a8b76b4)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5f91690f-de9b-464a-a7ac-f20d07534be4)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/14673658-d7fa-4c32-b32e-bb5999df6121)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cb8fdd43-f9ae-4f27-b7ea-ad3f054b13d9)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/72e152c0-ae6c-4e90-9c5d-733b4c143d44)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/616d256d-3f43-4db5-aea2-b3c163b919de)


### 5) Upload file in source folder & obsreve that its replicated to destination folder
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a4da77fc-a6aa-491b-9da7-486346a9c2ce)






### 4)	Add Destination
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/623fbdd6-e880-4f3c-9a7c-8f90cc95b336)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/39b65072-ea6e-48a9-813c-1bd53d0affe1)
