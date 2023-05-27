# Create an Alarm Using CloudWatch


Agenda : To create an alarm using CloudWatch that will allow to monitor CPU Utilization (in CloudWatch metrics) with a given threshold and receive notifications when the metrics fall outside the configured threshold levels.

Steps followed :

1) Launch couple of Linux VMs & connect to them via SSH

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9244adba-beeb-475e-aa86-52afbb20493b)



2) Perform some tasks on the VMs like, yum update
3) Work with CloudWatch services, to select metrics for CPU utilization for all 3 VMs
4) Create an alarm and send a notification through SNS

