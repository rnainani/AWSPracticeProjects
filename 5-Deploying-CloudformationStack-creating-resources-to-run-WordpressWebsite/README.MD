# Deploy a Cloudformation stack that creates the resources needed to run a stand-alone Wordpress website

## Steps followed :

### 1. Create CloudFormation template in JSON format

Open a text or code editor and create a plain-text file named wordpress_cloudformation_template.json. This document will hold the CloudFormation template in JSON format.

Document will begin by entering a left bracket, the template format version, and the template description. 

{

  "AWSTemplateFormatVersion" : "2010-09-09",

 "Description" : "CloudFormation Template for a Stand Alone Wordpress Site",


Next, add the parameters to the document. Parameters will be added for:

- An SSH key that developers can user to connect to their server.

- The type of instance they need to run, including a default selection of “t2.small.”

- A name, password, username, and root password for the MySQL database that will be installed on the server.  Defaults need to be included for these as well.


  "Parameters" : {

    "KeyName": {

      "Description" : "Name of an existing EC2 KeyPair to enable SSH access to the instances",

      "Type": "AWS::EC2::KeyPair::KeyName",

      "ConstraintDescription" : "must be the name of an existing EC2 KeyPair."

    },

    "InstanceType" : {

      "Description" : "WebServer EC2 instance type",

      "Type" : "String",

      "Default" : "t2.small",

      "AllowedValues" : [ "t2.small" ],

      "ConstraintDescription" : "must be a valid EC2 instance type."

    },

    "DBName" : {

      "Default": "wordpressdb",

      "Description" : "The WordPress database name",

      "Type": "String",

      "MinLength": "1",

      "MaxLength": "64",

      "AllowedPattern" : "[a-zA-Z][a-zA-Z0-9]*",

      "ConstraintDescription" : "must begin with a letter and contain only alphanumeric characters."

    },

    "DBUser" : {

      "Default": "wordpress",

      "Description" : "The WordPress database admin account username",

      "Type": "String",

      "MinLength": "1",

      "MaxLength": "16",

      "AllowedPattern" : "[a-zA-Z][a-zA-Z0-9]*",

      "ConstraintDescription" : "must begin with a letter and contain only alphanumeric characters."

    },

    "DBPassword" : {

      "Default": "wordpress",

      "Description" : "The WordPress database admin account password",

      "Type": "String",

      "MinLength": "8",

      "MaxLength": "41",

      "AllowedPattern" : "[a-zA-Z0-9]*",

      "ConstraintDescription" : "must contain only alphanumeric characters."

    },

    "DBRootPassword" : {

      "Default": "wordpress",

      "Description" : "MySQL root password",

      "Type": "String",

      "MinLength": "8",

      "MaxLength": "41",

      "AllowedPattern" : "[a-zA-Z0-9]*",

      "ConstraintDescription" : "must contain only alphanumeric characters."

    }

  },

With the parameters in place, now add a mappings section that will allow the template to dynamically select the correct AMI when creating an EC2 instance. The mapping should be based on the instance type and the region where the stack is being created :


  "Mappings" : {

    "AWSInstanceType2Arch" : {

      "t2.small" : { "Arch" : "HVM64"  }

    },

          "AWSRegionArch2AMI" : {

            "us-east-1" : {"HVM64" : "ami-032930428bf1abbff"},

            "us-east-2" : {"HVM64" : "ami-027cab9a7bf0155df"},

            "us-west-1" : {"HVM64" : "ami-088c153f74339f34c"},

            "us-west-2" : {"HVM64" : "ami-01fee56b22f308154"}

          }

   },

After the mappings section, next add a section for resources. Template needs to include resources for an EC2 Instance and Security Group. The Security Group needs to allow SSH access on port 22 and HTTP access on port 80.  


      "Resources" : {

"WebServerSecurityGroup" : {

      "Type" : "AWS::EC2::SecurityGroup",

      "Properties" : {

        "GroupDescription" : "Enable HTTP access via port 80, SSH access via port 22",

        "SecurityGroupIngress" : [

          {"IpProtocol" : "tcp", "FromPort" : "80", "ToPort" : "80", "CidrIp" : "0.0.0.0/0"},

          {"IpProtocol" : "tcp", "FromPort" : "22", "ToPort" : "22", "CidrIp" : "0.0.0.0/0"}

        ]

      }

    },


Next is a resource for an EC2 Instance.  This resource will configure all aspects of the server, including:

- Setting instance properties like SSH key and security group.

- Installing PHP, Apache, and MySQL.

- Creating a database for the Wordpress site using the parameters passed into the template.

- Installing Wordpress and configuring it to use the database.


   "WebServer": {

      "Type" : "AWS::EC2::Instance",

      "Metadata" : {

        "AWS::CloudFormation::Init" : {

          "configSets" : {

            "wordpress_install" : ["install_cfn",  "install_wordpress", "configure_wordpress" ]

          },

          "install_cfn" : {

            "files": {

              "/etc/cfn/cfn-hup.conf": {

                "content": { "Fn::Join": [ "", [

                  "[main]\n",

                  "stack=", { "Ref": "AWS::StackId" }, "\n",

                  "region=", { "Ref": "AWS::Region" }, "\n"

                ]]},

                "mode"  : "000400",

                "owner" : "root",

                "group" : "root"

              },

              "/etc/cfn/hooks.d/cfn-auto-reloader.conf": {

                "content": { "Fn::Join": [ "", [

                  "[cfn-auto-reloader-hook]\n",

                  "triggers=post.update\n",

                  "path=Resources.WebServer.Metadata.AWS::CloudFormation::Init\n",

                  "action=/opt/aws/bin/cfn-init -v ",

                          "         --stack ", { "Ref" : "AWS::StackName" },

                          "         --resource WebServer ",

                          "         --configsets wordpress_install ",

                          "         --region ", { "Ref" : "AWS::Region" }, "\n"

                ]]},

                "mode"  : "000400",

                "owner" : "root",

                "group" : "root"

              }

            },

            "services" : {

              "sysvinit" : {

                "cfn-hup" : { "enabled" : "true", "ensureRunning" : "true",

                              "files" : ["/etc/cfn/cfn-hup.conf", "/etc/cfn/hooks.d/cfn-auto-reloader.conf"] }

              }

            }

          },

          "install_wordpress" : {

            "packages" : {

              "yum" : {

                "php73"          : [],

                "php73-mysqlnd"  : [],

                "mysql57"        : [],

                "mysql57-server" : [],

                "mysql57-devel"  : [],

                "mysql57-libs"   : [],

                "httpd24"        : []

              }

            },

            "sources" : {

              "/var/www/html" : "http://wordpress.org/latest.tar.gz"

            },

            "files" : {

              "/tmp/setup.mysql" : {

                "content" : { "Fn::Join" : ["", [

                  "CREATE DATABASE ", { "Ref" : "DBName" }, ";\n",

                  "CREATE USER '", { "Ref" : "DBUser" }, "'@'localhost' IDENTIFIED BY '", { "Ref" : "DBPassword" }, "';\n",

                  "GRANT ALL ON ", { "Ref" : "DBName" }, ".* TO '", { "Ref" : "DBUser" }, "'@'localhost';\n",

                  "FLUSH PRIVILEGES;\n"

                ]]},

                "mode"  : "000400",

                "owner" : "root",

                "group" : "root"

              },

              "/tmp/create-wp-config" : {

                "content" : { "Fn::Join" : [ "", [

                  "#!/bin/bash -xe\n",

                  "cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php\n",

                  "sed -i \"s/'database_name_here'/'",{ "Ref" : "DBName" }, "'/g\" wp-config.php\n",

                  "sed -i \"s/'username_here'/'",{ "Ref" : "DBUser" }, "'/g\" wp-config.php\n",

                  "sed -i \"s/'password_here'/'",{ "Ref" : "DBPassword" }, "'/g\" wp-config.php\n"

                ]]},

                "mode" : "000500",

                "owner" : "root",

                "group" : "root"

              }

            },

            "services" : {

              "sysvinit" : {

                "httpd"  : { "enabled" : "true", "ensureRunning" : "true" },

                "mysqld" : { "enabled" : "true", "ensureRunning" : "true" }

              }

            }

          },

          "configure_wordpress" : {

            "commands" : {

              "01_set_mysql_root_password" : {

                "command" : { "Fn::Join" : ["", ["mysqladmin -u root password '", { "Ref" : "DBRootPassword" }, "'"]]},

                "test" : { "Fn::Join" : ["", ["$(mysql ", { "Ref" : "DBName" }, " -u root --password='", { "Ref" : "DBRootPassword" }, "' >/dev/null 2>&1 </dev/null); (( $? != 0 ))"]]}

              },

              "02_create_database" : {

                "command" : { "Fn::Join" : ["", ["mysql -u root --password='", { "Ref" : "DBRootPassword" }, "' < /tmp/setup.mysql"]]},

                "test" : { "Fn::Join" : ["", ["$(mysql ", { "Ref" : "DBName" }, " -u root --password='", { "Ref" : "DBRootPassword" }, "' >/dev/null 2>&1 </dev/null); (( $? != 0 ))"]]}

              },

              "03_configure_wordpress" : {

                "command" : "/tmp/create-wp-config",

                "cwd" : "/var/www/html/wordpress"

              }

            }

          }

        }

      },

      "Properties": {

        "ImageId" : { "Fn::FindInMap" : [ "AWSRegionArch2AMI", { "Ref" : "AWS::Region" },

                          { "Fn::FindInMap" : [ "AWSInstanceType2Arch", { "Ref" : "InstanceType" }, "Arch" ] } ] },

        "InstanceType"   : { "Ref" : "InstanceType" },

        "SecurityGroups" : [ {"Ref" : "WebServerSecurityGroup"} ],

        "KeyName"        : { "Ref" : "KeyName" },

        "UserData" : { "Fn::Base64" : { "Fn::Join" : ["", [

                       "#!/bin/bash -xe\n",

                       "yum update -y aws-cfn-bootstrap\n",

                       "/opt/aws/bin/cfn-init -v ",

                       "         --stack ", { "Ref" : "AWS::StackName" },

                       "         --resource WebServer ",

                       "         --configsets wordpress_install ",

                       "         --region ", { "Ref" : "AWS::Region" }, "\n",

                       "/opt/aws/bin/cfn-signal -e $? ",

                       "         --stack ", { "Ref" : "AWS::StackName" },

                       "         --resource WebServer ",

                       "         --region ", { "Ref" : "AWS::Region" }, "\n"

        ]]}}

      },

      "CreationPolicy" : {

        "ResourceSignal" : {

          "Timeout" : "PT15M"

        }

     }

    }

  },

The final section of the template is used to generate outputs using references to the resources that were created.  The PublicDNS property of the WebServer resource will be used to add an output that prints a URL for the Wordpress website:


  "Outputs" : {

    "WebsiteURL" : {

      "Value" : { "Fn::Join" : ["", ["http://", { "Fn::GetAtt" : [ "WebServer", "PublicDnsName" ]}, "/wordpress" ]]},

      "Description" : "WordPress Website"

    }

  }

}

Save the document. Now we've a JSON document containing a CloudFormation template. 


### 2) Open CloudFormation & create a new stack using the file created in last step 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/006e6be2-c39d-423c-885e-93091c056c57)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/01d78cf3-548e-4992-8584-b1b30c814dcb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0f72d3f3-1d11-4577-9703-28f4968c5374)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6035dd41-2d8c-4fb3-991c-863c1eaebd24)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/98e45e0d-64bf-44ac-be49-87fb446e79cd)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6651518c-f23c-4dce-8ca2-40f816c921ca)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1432a87f-af74-4603-8bb0-ca1564706adf)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8f519bbc-9f3b-4aaa-8686-5641bb5069a3)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/060b49b3-8d96-49a4-a936-643570495b38)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b50ac805-62af-467a-ab4c-ce3679627bfb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4402738f-21ad-45cf-90e0-da5fc47ffd4c)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5f864186-2457-414f-b7e2-a094556fac19)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/42115f96-0161-4cce-b6ec-653a330a7ac2)

### 3) Install Wordpress

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3c45f5d5-c399-4421-a1d5-10f2f707b881)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/15959b9d-6c77-4f85-97a0-6f5cc1bd0ba7)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/94e4f4fa-87ae-4203-84cd-ed592ac09ecb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7a79f108-818e-4428-81e4-748d5b096fc0)

### 4) Delete the CloudFormation Stack

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cedc64e5-7e05-4820-bb0d-0100a6f7275e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/11ebefc2-4b32-459e-bf98-aa6b6f1cfdf4)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/aa70a8d7-cb33-4727-82b4-15a0d3c6bf93)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a2d79b23-cc5c-4894-800b-88726702ef68)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dadaa9ed-e108-46d6-aa39-b600ff695972)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/45d3122a-dd6c-4b5b-9940-10f69aaff3f3)
