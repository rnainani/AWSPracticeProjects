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

![1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/431593a4-2fac-48b7-8458-2fec9256eeae)

Create private key :

![2](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1b77b637-b435-422c-9b4f-364fb6397382)

Convert private key to putty :

![3](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1e46c54e-ec62-4fe2-a392-e302744f4ade)

Launch Instance : 

![4](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/314cdf09-b724-4278-b39e-11cae35b5442)
![5](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4c341875-8d37-4c4a-b1e4-c7a0068cdf18)
 
Convert private key to putty using putyygen :

![6](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dcc55224-8c59-493e-922b-b876ff3f8cad)
![7](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ffc5d88b-a580-46a0-840d-1e3db3274552)

Connect to the EC2 instance using putty : 

![8](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/746cfa66-306a-46b3-b3c0-47d047e73184)
![9](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/84ca3148-974e-4dab-8aa5-dad02dbe4134)
![10](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d3acf560-aaa0-4e18-b7e3-d4e066e638c6)

Get the latest updates on EC2 instance :

![11](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f9609753-a620-402f-98b2-d8ffb671fbd0)
![12](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a99dffc1-c789-4fa4-a0ac-7d8c5d613ce0)
 
After the updates complete, install the PHP software :  

![13](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/681b66f8-6e01-4a98-ac85-132770a61ab6)
![14](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a79e8627-057f-4379-adc5-8ba634f1bef5)

Install the Apache web server :

![15](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/777980c1-70d1-4d11-a08c-42604602c330)

Start the web server :

![16](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/151817cc-1067-418e-86b3-3b12feb1e90a)

Test page can be seen at the public dns for ec2 showing apache installed successfully - http://ec2-3-82-153-125.compute-1.amazonaws.com/ :

![17](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3dda0b4b-f808-4461-8639-a4e1346212d6)

### Set file permissions for the Apache web server

1.	Add the ec2-user user to the apache group: 

![18](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b41fcb35-be84-4c4c-b114-20a63a898e2e)
 
Log out to refresh your permissions and include the new apache group
Exit
Log back in again and verify that the apache group exists :

![19](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b9f15777-66ac-40ef-bf01-38aff16265d2)

Change the group ownership of the /var/www directory and its contents to the apache group :

![20](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f93321a0-4297-4c1d-9a2d-e1e15648bc0a)

Change the directory permissions of /var/www and its subdirectories to add group write permissions and set the group ID on subdirectories created in the future :

![21](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/236fad4d-f28a-4e07-b205-dd2b6ef449f3)

Recursively change the permissions for files in the /var/www directory and its subdirectories to add group write permissions :

<img width="543" alt="22" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/acd14d3d-bdcc-4781-a86a-6633a2f7f54f">

### Connecting Apache web server to DB instance

1.	change the directory to /var/www and create a new subdirectory named inc

<img width="299" alt="23" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/293706d7-ebc7-4b2f-af43-2e8b2e4d3604">
 
2.	Create a new file in the inc directory named dbinfo.inc, and then edit the file by calling nano (or the editor of your choice).
>dbinfo.inc
nano dbinfo.inc

<img width="436" alt="24" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8d9ebc2d-96f5-418e-b2c2-24497a03e002">
<img width="375" alt="25" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8b821a17-97b7-45fd-913e-d07379c493a4">
 
Change the directory to /var/www/html.
create a new file in the html directory named SamplePage.php, and then edit the file : 

<img width="381" alt="26" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/07fe5481-a3c8-42f5-92f1-ac7cf32dde10">
 
Adding contents to the SamplePage.php file:

<img width="543" alt="27" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ad40aa81-7d89-4cd3-afb2-a868b7600514">

Create db instance & connect with ec2 instance :

<img width="399" alt="28" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d08b822f-0ad9-4988-bb0c-d512481e9965">
<img width="394" alt="29" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a41eb6e9-0545-4bbe-9300-9d29ae04a4de">
<img width="330" alt="30" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/24661f99-9c0e-414a-ad88-442e3558f077">
<img width="548" alt="31" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0ea1fb58-71db-4fea-86b7-5a5dc5e9c4cc">

Install the MySQL : 

<img width="417" alt="32" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/56c10f7d-e612-407f-9414-5a9b895910d5">
<img width="550" alt="33" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0df17c0a-dbbd-47b8-8a9c-627c58345a79">
<img width="537" alt="34" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0f4681e7-b7f5-4754-9156-ca877d46a17e">

### Setup & Monitor the health check for the endpoint (http://ec2-3-82-153-125.compute-1.amazonaws.com/SamplePage.php) using Route 53 : 

<img width="546" alt="35" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4a6ab8a5-b1bc-4740-a8ae-0ea30f4faa6a">
