# Deploying a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk

## Agenda - Deploying a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk

An Amazon RDS DB instance will be launched that is completely independent to AWS Elastic Beanstalk, then configure a high-availability environment running a WordPress website to connect to it. The website will use Amazon Elastic File System (Amazon EFS) as the shared storage for uploading files.

Running a DB instance external to Elastic Beanstalk decouples the database from the lifecycle of the environment. This will let us connect to the same database from multiple environments, swap out one database for another, or perform a blue/green deployment without affecting the database.

### Steps followed :

1) Launch a DB instance in Amazon RDS (MySQL, Multi-AZ deployment) completely independent of Elastic Beanstalk and Elastic Beanstalk environments, and will not be terminated or monitored by Elastic Beanstalk.

![1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f32726db-2ea4-42af-b425-cbaa82310844)
![2](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/917212fb-e775-4eea-b55b-c72af14e1331)
![3](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c2c490c6-d1d0-4aca-9365-86648d6682ee)
![4](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1eb57402-8b9b-4e15-a361-6e91383b7ac2)
![5](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d8a75f4d-7774-4f69-a661-a9c4fc75788f)
![6](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a6332118-da03-470c-b158-b92624ea8bdd)

After your DB instance is created, modify the security group attached to it in order to allow inbound traffic on the appropriate port..

<img width="823" alt="7" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/433dce99-598c-4fac-a91b-f70cf4a8643b">

<img width="808" alt="8" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/67da4904-ac82-4b31-b96e-831f5920811d">

### Download WordPress

<img width="823" alt="9" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f903ef53-bd76-40dc-b765-9b0256f95c9f">

<img width="819" alt="10" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d4eff8cd-5654-40bd-9001-3c693dfe8bef">

<img width="820" alt="11" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3023e234-6dba-4c43-8e9c-10e70f81f3a8">

### Launch an Elastic Beanstalk environment

<img width="824" alt="12" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e03399e3-3f4c-488b-91f6-99a0fbaba999">

<img width="811" alt="13" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f94373ce-c103-473e-8532-577955061d88">

<img width="820" alt="14" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7214e1e7-26bb-4da8-abc6-89e7149349cc">

(Make sure to provide admin access or required access, before submitting for app creation.)

<img width="821" alt="15" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/313a7f86-c7b5-44d6-b6e3-f4d2b89cdcc3">

<img width="822" alt="16" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2da00be4-78e2-4bc1-aab9-4117bf60e24d">

<img width="821" alt="17" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/60fddb05-c097-4b54-9e19-3f057899812b">

<img width="820" alt="18" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/15def81f-eb8d-4f58-b875-864a3c51e85d">

<img width="820" alt="19" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c8233787-f051-40d1-b5fd-7e4e76568b00">

<img width="822" alt="20" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2beae7aa-4220-4911-b0fe-0388f74c5974">

### Configure security groups and environment properties

Add the security group of your DB instance to your running environment. This procedure causes Elastic Beanstalk to reprovision all instances in your environment with the additional security group attached.

<img width="337" alt="21" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ec17e1c5-088f-44c5-8aa1-0ecf18266000">

<img width="333" alt="22" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/77b49592-2a4b-411f-9308-daa02fe30c7e">

### To configure environment properties for an Amazon RDS DB instance

<img width="332" alt="23" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2cc6fd22-93eb-4a87-8a4d-0cf4b6c576e8">

<img width="336" alt="24" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/18ce1800-07c0-43c1-aff9-0e1c9dec427b">

<img width="327" alt="25" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9af7214b-9eca-47b6-b4ca-0dfdf6e95902">

### Configure and deploy your application

Verify that the structure of your wordpress-beanstalk folder is correct, as shown.

<img width="760" alt="26" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b2641870-499b-430a-a4f6-22220545fe6f">

### To update configuration files and create a source bundle

Modify the configuration files as follows.

.ebextensions/dev.config – Restricts access to your environment to protect it during the WordPress installation process. Replace the placeholder IP address near the top of the file with the public IP address of the computer you'll use to access your environment's website to complete your WordPress installation.

<img width="761" alt="27" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e41769e3-d152-4f7f-8fcf-59ee6a83eea7">

.ebextensions/efs-create.config – Creates an EFS file system and mount points in each Availability Zone/subnet in your VPC. Identify your default VPC and subnet IDs in the Amazon VPC console.

<img width="756" alt="28" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0c3d57bb-0325-457c-ae55-1cfebb28efd4">

Create a source bundle containing the files in your project folder. The following command creates a source bundle named wordpress-beanstalk.zip.

~/eb-wordpress$ zip ../wordpress-beanstalk.zip -r * .[^.]*

<img width="732" alt="29" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/54739f12-0570-4523-9402-e9ea89e21040">

Upload the source bundle to Elastic Beanstalk to deploy WordPress to your environment.

### To deploy a source bundle

<img width="754" alt="30" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ac573ab9-2dce-482b-8b52-ca69a6573b2a">

<img width="757" alt="31" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/326a05f4-8647-4af0-8276-41c8cd2641c5">

<img width="754" alt="32" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6b3a819d-d01a-466a-a139-9f8b080bb9be">

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
