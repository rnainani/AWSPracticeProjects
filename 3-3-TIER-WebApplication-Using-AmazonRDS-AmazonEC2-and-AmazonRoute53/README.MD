# 3-TIER Web Application Using Amazon RDS (MYSQL DB), Amazon EC2(Apache Web Server) and Amazon Route 53 (Monitoring Health Checks)

## Agenda - Configure and Connect a MySQL Database Instance with a Web Server and Set up the Monitoring of the Solution

### Steps followed at a high level: 

1. Create the Database in the AWS Console
2. Launch an EC2 Instance
3. Convert a Private Key to PuTTY using PuTTYgen
4. Install an Apache Web Server with PHP
5. Set File Permissions for the Apache Web Server
6. Connect your Apache Web Server to Your Database Instance
7. Monitor the Portal Using Route 53

### Detailed Steps with screenshots :

Create the EC2 instance

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1b1ddfb8-284d-4cd7-a785-c50f94ae2b6d)

Create private key :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f8f78ecb-9407-4b9a-9742-6a3ffa8caa16)

Convert private key to putty :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3184cc2f-291f-4420-8146-ef84e6c99649)

Launch Instance : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0b5bf8b2-c648-4e42-8cd7-91c1a76829ff)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d60e1d70-36d1-4751-9f34-66591ac19a73)
 
Convert private key to putty using putyygen :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6256550f-1d34-406d-9e16-d77db63dd139)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/319487fa-bded-46c2-a312-c2b8b775b160)

Connect to the EC2 instance using putty : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a022ed3f-2883-413c-8bd9-ca98a854f020)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6e408ec3-7549-44a2-9ccf-76235039c051)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b8817b07-8c47-40af-ae5b-7d4ce1823472)

Get the latest updates on EC2 instance :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1a94cd4b-0936-4bb0-8c17-401650466b44)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7e2abdbd-9526-4c58-9c33-e552c8e5cae0)
 
After the updates complete, install the PHP software :  

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/42c0df61-27b0-47ea-b44c-919a37a68c8d)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4766ef80-7d32-47f9-a224-b0dff9d99357)

Install the Apache web server :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/756a3872-6852-49de-8d86-2dfbc7465e21)

Start the web server :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/23997beb-7b2f-43f0-b3ff-4cc22c139098)

Test page can be seen at the public dns for ec2 showing apache installed successfully - http://ec2-3-82-153-125.compute-1.amazonaws.com/ :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/373b46fe-cc61-4f1e-b596-0f9c370f71d1)

### Set file permissions for the Apache web server

1.	Add the ec2-user user to the apache group: 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1239aed6-1f0d-4f64-a943-28530c3b90ce)
 
Log out to refresh your permissions and include the new apache group
Exit
Log back in again and verify that the apache group exists :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4931dadd-db1d-4a46-8207-20c27312a164)

Change the group ownership of the /var/www directory and its contents to the apache group :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/188ef350-80f7-4810-96da-b1a35ff9f664)

Change the directory permissions of /var/www and its subdirectories to add group write permissions and set the group ID on subdirectories created in the future :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/bc118ede-5835-4257-a975-9b9ac90b1bc8)

Recursively change the permissions for files in the /var/www directory and its subdirectories to add group write permissions :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7172befe-c69d-44bc-9f39-fbd6d62e2fdb)

### Connecting Apache web server to DB instance

1.	change the directory to /var/www and create a new subdirectory named inc

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e21ef3cd-a4f6-4d57-86f0-0bcecc916d83)
 
2.	Create a new file in the inc directory named dbinfo.inc, and then edit the file by calling nano (or the editor of your choice).
>dbinfo.inc
nano dbinfo.inc

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3cbbd6ec-b1ea-4591-9cff-14dd40bd0208)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0452e669-9a46-48f2-9300-2df5b2ebbd39)
 
Change the directory to /var/www/html.
create a new file in the html directory named SamplePage.php, and then edit the file : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/081b1a4c-0f3f-4018-82d1-b4282f9e9e44)
 
Adding contents to the SamplePage.php file:

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5a2e3e2e-4876-4c65-85e1-caef1840a214)

Create db instance & connect with ec2 instance :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e12e8d4f-318a-42ce-8484-c6c3d510bba4)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3ca2f15d-bca4-42f6-bcd7-a53f9a24db04)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c1810f0d-0996-4300-af48-9d8bf1031179)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/39ac638a-99db-4f5e-9c9b-33ed1227ee22)

Install the MySQL : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/97a41f3b-4486-40b9-bc5f-1045bde5bb30)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6ff6aa3a-005c-489e-b379-8875ca399d77)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1cd71dfd-262b-442f-a172-9dc092c03909)

### Setup & Monitor the health check for the endpoint (http://ec2-3-82-153-125.compute-1.amazonaws.com/SamplePage.php) using Route 53 : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/040eb338-1801-490d-8e19-08a7f59800b9)
