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
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7fb226ca-ac99-4977-9494-4964e9be987d)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/df0c3532-739f-4a60-9948-c7714733a40c)

(Make sure to provide admin access or required access, before submitting for app creation.)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4f6519a5-1f48-4133-a292-38c81d01eac1)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e6019e8d-fb17-4c4d-84da-66212766c4a5)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/64e6f00b-52ef-42a2-9d3f-421adf90c0b8)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/85af9c28-77b4-40f9-9f5d-fee39de68b42)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dfb4615c-38a3-4737-aee3-58ac0a7f3ae3)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5c9c8f1e-e010-493e-b9af-10c911f077e2)

### Configure security groups and environment properties

Add the security group of your DB instance to your running environment. This procedure causes Elastic Beanstalk to reprovision all instances in your environment with the additional security group attached.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/de4948b0-9a98-43c7-ade4-854a987835fb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/415496aa-103d-47d9-a953-badbf92177f8)

### To configure environment properties for an Amazon RDS DB instance

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ca1c8bc3-329a-4322-a688-43ca63fa9455)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/01497814-b30c-4b1d-93f4-d7b124e01e58)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4719509a-49c2-40e2-9ea9-51352b0a5aaf)

### Configure and deploy your application

Verify that the structure of your wordpress-beanstalk folder is correct, as shown.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/81af51bc-f429-48c8-9f44-ddf6d2074684)

### To update configuration files and create a source bundle

Modify the configuration files as follows.

.ebextensions/dev.config – Restricts access to your environment to protect it during the WordPress installation process. Replace the placeholder IP address near the top of the file with the public IP address of the computer you'll use to access your environment's website to complete your WordPress installation.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4c1a093c-dd50-4250-97fb-cb900a9d3a8c)

.ebextensions/efs-create.config – Creates an EFS file system and mount points in each Availability Zone/subnet in your VPC. Identify your default VPC and subnet IDs in the Amazon VPC console.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/60662d4d-f8f9-4b5b-af6d-8f8fbbf4ec29)

Create a source bundle containing the files in your project folder. The following command creates a source bundle named wordpress-beanstalk.zip.

~/eb-wordpress$ zip ../wordpress-beanstalk.zip -r * .[^.]*

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/98bdd3fb-e396-412a-a41c-65800cb81489)

Upload the source bundle to Elastic Beanstalk to deploy WordPress to your environment.

### To deploy a source bundle

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3b0ffbf8-db50-459d-ac4e-912ebf27c878)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/56659797-94e2-4913-91f6-959721aa9304)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a6220a30-2728-4f6e-bf0b-15181ecc118e)

Install WordPress
To complete your WordPress installation
Open the Elastic Beanstalk console, and in the Regions list, select your AWS Region.

In the navigation pane, choose Environments, and then choose the name of your environment from the list.

Note
If you have many environments, use the search bar to filter the environment list.

Choose the environment URL to open your site in a browser. You are redirected to a WordPress installation wizard because you haven't configured the site yet.

Perform a standard installation. The wp-config.php file is already present in the source code and configured to read the database connection information from the environment. You shouldn't be prompted to configure the connection.

Installation takes about a minute to complete.

Update keys and salts
The WordPress configuration file wp-config.php also reads values for keys and salts from environment properties. Currently, these properties are all set to test by the wordpress.config file in the .ebextensions folder.

The hash salt can be any value that meets the environment property requirements, but you should not store it in source control. Use the Elastic Beanstalk console to set these properties directly on the environment.

To update environment properties
Open the Elastic Beanstalk console, and in the Regions list, select your AWS Region.

In the navigation pane, choose Environments, and then choose the name of your environment from the list.

Note
If you have many environments, use the search bar to filter the environment list.

On the navigation pane, choose Configuration.

Under Software, choose Edit.

For Environment properties, modify the following properties:

AUTH_KEY – The value chosen for AUTH_KEY.

SECURE_AUTH_KEY – The value chosen for SECURE_AUTH_KEY.

LOGGED_IN_KEY – The value chosen for LOGGED_IN_KEY.

NONCE_KEY – The value chosen for NONCE_KEY.

AUTH_SALT – The value chosen for AUTH_SALT.

SECURE_AUTH_SALT – The value chosen for SECURE_AUTH_SALT.

LOGGED_IN_SALT – The value chosen for LOGGED_IN_SALT.

NONCE_SALT — The value chosen for NONCE_SALT.

Choose Apply at the bottom of the page.

Note
Setting the properties on the environment directly overrides the values in wordpress.config.

Remove access restrictions
The sample project includes the configuration file loadbalancer-sg.config. It creates a security group and assigns it to the environment's load balancer, using the IP address that you configured in dev.config. It restricts HTTP access on port 80 to connections from your network. Otherwise, an outside party could potentially connect to your site before you have installed WordPress and configured your admin account.

Now that you've installed WordPress, remove the configuration file to open the site to the world.

To remove the restriction and update your environment
Delete the .ebextensions/loadbalancer-sg.config file from your project directory.

~/wordpress-beanstalk$ rm .ebextensions/loadbalancer-sg.config
Create a source bundle.

~/eb-wordpress$ zip ../wordpress-beanstalk-v2.zip -r * .[^.]*
Upload the source bundle to Elastic Beanstalk to deploy WordPress to your environment.

To deploy a source bundle
Open the Elastic Beanstalk console, and in the Regions list, select your AWS Region.

In the navigation pane, choose Environments, and then choose the name of your environment from the list.

Note
If you have many environments, use the search bar to filter the environment list.

On the environment overview page, choose Upload and deploy.

Use the on-screen dialog box to upload the source bundle.

Choose Deploy.

When the deployment completes, you can choose the site URL to open your website in a new tab.

Configure your Auto Scaling group
Finally, configure your environment's Auto Scaling group with a higher minimum instance count. Run at least two instances at all times to prevent the web servers in your environment from being a single point of failure. This also allows you to deploy changes without taking your site out of service.

To configure your environment's Auto Scaling group for high availability
Open the Elastic Beanstalk console, and in the Regions list, select your AWS Region.

In the navigation pane, choose Environments, and then choose the name of your environment from the list.

Note
If you have many environments, use the search bar to filter the environment list.

In the navigation pane, choose Configuration.

In the Capacity configuration category, choose Edit.

In the Auto Scaling group section, set Min instances to 2.

Choose Apply at the bottom of the page.

To support content uploads across multiple instances, the sample project uses Amazon EFS to create a shared file system. Create a post on the site and upload content to store it on the shared file system. View the post and refresh the page multiple times to hit both instances and verify that the shared file system is working.

### Upgrade WordPress

To upgrade to a new version of WordPress, back up your site and deploy it to a new environment.

In the WordPress admin console, use the export tool to export your posts to an XML file.

Deploy and install the new version of WordPress to Elastic Beanstalk with the same steps that you used to install the previous version. To avoid downtime, you can create an environment with the new version.

On the new version, install the WordPress Importer tool in the admin console and use it to import the XML file containing your posts. If the posts were created by the admin user on the old version, assign them to the admin user on the new site instead of trying to import the admin user.

If you deployed the new version to a separate environment, do a CNAME swap to redirect users from the old site to the new site.

### Clean up

When you finish working with Elastic Beanstalk, you can terminate your environment. Elastic Beanstalk terminates all AWS resources associated with your environment, such as Amazon EC2 instances, database instances, load balancers, security groups, and alarms.

To terminate your Elastic Beanstalk environment
Open the Elastic Beanstalk console, and in the Regions list, select your AWS Region.

In the navigation pane, choose Environments, and then choose the name of your environment from the list.

Note
If you have many environments, use the search bar to filter the environment list.

Choose Actions, and then choose Terminate environment.

Use the on-screen dialog box to confirm environment termination.

With Elastic Beanstalk, you can easily create a new environment for your application at any time.

In addition, you can terminate database resources that you created outside of your Elastic Beanstalk environment. When you terminate an Amazon RDS DB instance, you can take a snapshot and restore the data to another instance later.

To terminate your RDS DB instance
Open the Amazon RDS console.

Choose Databases.

Choose your DB instance.

Choose Actions, and then choose Delete.

Choose whether to create a snapshot, and then choose Delete.
