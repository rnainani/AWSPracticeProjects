# Deploy a Cloudformation stack that creates the resources needed to run a stand-alone Wordpress website

## Steps followed :

### 1. Create CloudFormation template in JSON format

Open a text or code editor and create a plain-text file named wordpress_cloudformation_template.json. This document will hold the CloudFormation template in JSON format.

Document will begin by entering a left bracket, the template format version, and the template description. 
```json
{
  "AWSTemplateFormatVersion" : "2010-09-09",

 "Description" : "CloudFormation Template for a Stand Alone Wordpress Site",
```

Next, add the parameters to the document. Parameters will be added for:

- An SSH key that developers can user to connect to their server.

- The type of instance they need to run, including a default selection of “t2.small.”

- A name, password, username, and root password for the MySQL database that will be installed on the server.  Defaults need to be included for these as well.

```json
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
```

With the parameters in place, now add a mappings section that will allow the template to dynamically select the correct AMI when creating an EC2 instance. The mapping should be based on the instance type and the region where the stack is being created :

```json
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
```

After the mappings section, next add a section for resources. Template needs to include resources for an EC2 Instance and Security Group. The Security Group needs to allow SSH access on port 22 and HTTP access on port 80.  

```json
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
```

Next is a resource for an EC2 Instance.  This resource will configure all aspects of the server, including:

- Setting instance properties like SSH key and security group.

- Installing PHP, Apache, and MySQL.

- Creating a database for the Wordpress site using the parameters passed into the template.

- Installing Wordpress and configuring it to use the database.

```json
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
```

The final section of the template is used to generate outputs using references to the resources that were created.  The PublicDNS property of the WebServer resource will be used to add an output that prints a URL for the Wordpress website:

```json
  "Outputs" : {
    "WebsiteURL" : {
      "Value" : { "Fn::Join" : ["", ["http://", { "Fn::GetAtt" : [ "WebServer", "PublicDnsName" ]}, "/wordpress" ]]},
      "Description" : "WordPress Website"
    }
  }
}
```

Save the document. Now we've a JSON document containing a CloudFormation template. 


### 2) Open CloudFormation & create a new stack using the file created in last step 

![1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/053fbcea-e879-4cba-a5ec-b97a61f5d03f)

![2](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2e859409-79b3-48ad-8144-7f3111b3f795)

![3](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b9c8e980-26e4-42b1-92ed-b5404f49dd93)

![4](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7bd28565-61f9-441c-8948-a224c4c196f0)

![5](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/262fddc7-4c6c-41ae-a4c5-5b4b6b23ff08)

![6](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4e5f2dbc-c35a-4780-b2c4-b93c853b4bde)

![7](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/44899658-d0fd-4ba6-8df0-cfc53c156cad)

![8](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/91ce7550-4779-40a3-ab01-d9c2a20a734e)

<img width="599" alt="9" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2fbd123e-0433-4a5f-9951-14b767704d77">

<img width="598" alt="10" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/12e23d34-5603-44b1-9488-a1c7c3d49a28">

<img width="593" alt="11" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/121fe38f-874c-4dc4-8367-a746f0c2f007">

<img width="595" alt="12" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d8e776cc-b07e-43ad-9d5f-3a052e5794bf">

<img width="595" alt="13" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/835b2d89-8b3e-4280-84b5-0188c0a4cd55">

### 3) Install Wordpress

<img width="602" alt="14" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7cf5d867-e20d-4ce2-9e6e-e6547170b004">

<img width="608" alt="15" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4117a212-5b3d-4871-99c8-5ffad58250b7">

<img width="608" alt="16" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/178f69b2-790d-4afb-a381-76aecaceabd7">

<img width="604" alt="17" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c21a6239-8c28-4536-a954-5d01e0aedc0c">

### 4) Delete the CloudFormation Stack

<img width="611" alt="18" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/850461c7-70d3-40c7-bbe8-5a75aa449ffb">

<img width="603" alt="19" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/be6dae07-7a22-4005-bbe2-142cfac813ee">

<img width="610" alt="20" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4abd4c94-6cfc-40f6-96b2-ef2cf4e2f22d">

<img width="601" alt="21" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5ea31d07-0f2c-4a06-b067-dee2a18ab461">

<img width="619" alt="22" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9b39e25c-e9c7-45e7-97cc-d1971b9f12f2">

<img width="613" alt="23" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f16def2c-fae3-4f1c-91de-35bb2ba223f4">
