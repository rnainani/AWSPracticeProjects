# Create an Alarm Using CloudWatch


## Agenda : To create an alarm using CloudWatch that will allow to monitor CPU Utilization (in CloudWatch metrics) with a given threshold and receive notifications when the metrics fall outside the configured threshold levels.

### Steps followed :

### 1) Launch couple of Linux VMs & connect to them via SSH

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9244adba-beeb-475e-aa86-52afbb20493b)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6e4ecd54-cb6b-47bb-a4fb-e28a435c0ac2)

### 2) Open CloudWatch to select metrics for CPU utilization for all 3 VMs

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/da40ae3b-9974-409d-a69c-2727a3b31ced)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e8877d05-181a-49b8-a28b-0dc38cdfe5bf)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/952a493c-358d-406c-bde9-7930eff44a1d)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6ca23b80-9b90-446d-886e-22aff5482cb5)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/562c6047-64de-4d65-a3ba-b0a9fd713bc0)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1de7576a-24de-42d2-a31c-c7330fa4a58c)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6a72e483-819a-4ddc-b2e5-9fec53828782)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/da0badf1-ac0d-4647-9f23-6f3c60d89bb3)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4b430d3c-6cd5-4906-8f99-1568eb46ab6d)

### 3) Create an alarm and send a notification through SNS

Following step for all VMs one-by-one :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0eac60a1-bed1-4569-8749-7f1c9faaca89)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2f1a4e39-a569-4aaa-943d-ef793ea2ddc5)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/aa3eeec3-3bdc-429a-b03c-7e7b6b9c46b7)

Click on Create new topic and add an email address then click on Create topic :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/001244a4-e597-488e-a53c-8a9e17b90c8e)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/eb21c880-090c-4ead-8029-e1f414023391)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d486e783-c0d4-4934-9688-742cf8e14094)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/47dd9354-0be3-4725-897d-ce42f12b39cc)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6a15f1d9-04f2-4d8a-9be9-63a52d96f0bc)
