# Create an Alarm Using CloudWatch


Agenda : To create an alarm using CloudWatch that will allow to monitor CPU Utilization (in CloudWatch metrics) with a given threshold and receive notifications when the metrics fall outside the configured threshold levels.

Steps followed :

1) Launch couple of Linux VMs & connect to them via SSH

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9244adba-beeb-475e-aa86-52afbb20493b)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6e4ecd54-cb6b-47bb-a4fb-e28a435c0ac2)



2) Perform some tasks on the VMs like, yum update
3) Open CloudWatch to select metrics for CPU utilization for all 3 VMs

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/83ec743c-a30f-44c7-9c9d-b2e7761a7b4e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/19018f59-4662-4986-bdc8-39f8137b63cb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9a359bf7-2ad1-4663-b9ca-fc769f7700be)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/66c2c42a-524a-4da8-9e66-2a8a2aa4b1d5)




5) Create an alarm and send a notification through SNS

