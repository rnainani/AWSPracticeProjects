# Deploy a Cloudformation stack that creates the resources needed to run a stand-alone Wordpress website

### Steps followed :

1. Open a text or code editor on your local system and create a plain-text file named wordpress_cloudformation_template.json. This document will hold the CloudFormation template in JSON format.  While creating the document, pay special attention to punctuation including commas, colons, quotes, and brackets.

You'll begin the document by entering a left bracket, the template format version, and the template description. Paste the following code into the document:

{

  "AWSTemplateFormatVersion" : "2010-09-09",

 "Description" : "CloudFormation Template for a Stand Alone Wordpress Site",

Next, you'll continue the document by adding the parameters.  Particularly, this template will need parameters for:

An SSH key that developers can user to connect to their server.

The type of instance they need to run, including a default selection of “t2.small.”

A name, password, username, and root password for the MySQL database that will be installed on the server.  Defaults need to be included for these as well.

Paste the following code into the document, on the line immediately following the previous entry:

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

With the parameters in place, you'll now add a mappings section that will allow the template to dynamically select the correct AMI when creating an EC2 instance.  The mapping should be based on the  instance type and the region where the stack is being created.  

Paste the following code into your document, again after the previously entered code:

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

After the mappings section you'll next add a section for resources.  Your template needs to include resources for an EC2 Instance and Security Group.  The Security Group needs to allow SSH access on port 22 and HTTP access on port 80.  

Paste the following code into your document:

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

Setting instance properties like SSH key and security group.

Installing PHP, Apache, and MySQL.

Creating a database for the Wordpress site using the parameters passed into the template.

Installing Wordpress and configuring it to use the database.

Paste the following code into your document:

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

The final section of the template is used to generate outputs using references to the resources that were created.  You'll use the PublicDNS property of the WebServer resource to add an output that prints a URL for the Wordpress website.

Paste the following code into the document.  Note that this code includes right-side curly brackets that close the Resource section as well as the left-side curly bracket that opened the JSON document:

  "Outputs" : {

    "WebsiteURL" : {

      "Value" : { "Fn::Join" : ["", ["http://", { "Fn::GetAtt" : [ "WebServer", "PublicDnsName" ]}, "/wordpress" ]]},

      "Description" : "WordPress Website"

    }

  }

}

Save your document.

You now have a JSON document containing a CloudFormation template. Move on to the next challenge where you will create a stack in AWS and test the template.
