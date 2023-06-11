# Deploying a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk

## Agenda - Deploying a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk

An Amazon RDS DB instance will be launched that is completely independent to AWS Elastic Beanstalk, then configure a high-availability environment running a WordPress website to connect to it. The website will use Amazon Elastic File System (Amazon EFS) as the shared storage for uploading files.

Running a DB instance external to Elastic Beanstalk decouples the database from the lifecycle of the environment. This will let us connect to the same database from multiple environments, swap out one database for another, or perform a blue/green deployment without affecting the database.

### Steps followed :

1) Launch a DB instance in Amazon RDS (MySQL, Multi-AZ deployment) completely independent of Elastic Beanstalk and Elastic Beanstalk environments, and will not be terminated or monitored by Elastic Beanstalk.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a6ee4c0e-c7f6-49af-8f11-9d7e9fd569e2)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b3299e9e-69b4-4359-aff0-555eeb0d71fb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2f64267e-1a04-4bba-b549-abe05c62fd2d)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c153772a-d142-41b3-bbfb-c34989db403c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/176d1c7e-cce9-4530-9e52-053c28be15a1)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/42bfa3e9-803d-4b31-9ec2-d6fe920dcaa2)

After your DB instance is created, modify the security group attached to it in order to allow inbound traffic on the appropriate port..

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2d63b1bd-6f31-4f15-9261-3d404013620b)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/15b36831-f7d5-4616-ac62-ea6a94e3ba4a)

### Download WordPress

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1cae6df1-9d71-4086-9114-76d57709268b)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/de0f8bfb-ed34-40ee-a5d0-207ee408facf)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f9b184ef-27fd-4430-8285-9a61befd8dc2)

### Launch an Elastic Beanstalk environment

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b315baf1-a8ba-4365-8d72-bb7fa8be2891)


