# 3-TIER Web Application Using Amazon RDS (MYSQL DB), Amazon EC2(Apache Web Server) and Amazon Route 53 (Monitoring Health Checks)

## Agenda - Configure and Connect a MySQL Database Instance with a Web Server and Set up the Monitoring of the Solution

### Steps followed :

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
 
 
After the updates complete, install the PHP software :  
 

Install the Apache web server :
 
Start the web server :
 




Test page can be seen at the public dns for ec2 showing apache installed successfully - http://ec2-3-82-153-125.compute-1.amazonaws.com/ :
 

Set file permissions for the Apache web server
1.	Add the ec2-user user to the apache group: 

 
Log out to refresh your permissions and include the new apache group
Exit
Log back in again and verify that the apache group exists :
 
Change the group ownership of the /var/www directory and its contents to the apache group :
 

Change the directory permissions of /var/www and its subdirectories to add group write permissions and set the group ID on subdirectories created in the future :
 
Recursively change the permissions for files in the /var/www directory and its subdirectories to add group write permissions :
 
Connecting Apache web server to DB instance
1.	change the directory to /var/www and create a new subdirectory named inc
 
2.	Create a new file in the inc directory named dbinfo.inc, and then edit the file by calling nano (or the editor of your choice).
>dbinfo.inc
nano dbinfo.inc
 
 
Change the directory to /var/www/html.
create a new file in the html directory named SamplePage.php, and then edit the file : 
 
Adding contents to the SamplePage.php file:
 







Create db instance & connect with ec2 instance :
 
 
 
 

Install the MySQL : 
 
 
 

Setup & Monitor the health check for the endpoint (http://ec2-3-82-153-125.compute-1.amazonaws.com/SamplePage.php) using Route 53 : 
