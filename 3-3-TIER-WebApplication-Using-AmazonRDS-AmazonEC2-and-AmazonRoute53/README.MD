# 3-TIER Web Application Using Amazon RDS (MYSQL DB), Amazon EC2(Apache Web Server) and Amazon Route 53 (Monitoring Health Checks)

## Agenda - Configure and Connect a MySQL Database Instance with a Web Server and Set up the Monitoring of the Solution

### Steps followed :

Create the EC2 instance

 ![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1b1ddfb8-284d-4cd7-a785-c50f94ae2b6d)

Create private key :
 
Convert private key to putty :
 

Launch Instance :
 


 
Convert private key to putty using putyygen :
 
 

Connect to the EC2 instance using putty :
 
 

 

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
