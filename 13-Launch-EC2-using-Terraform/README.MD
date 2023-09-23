# Install Terraform locally & Launch AWS EC2 using Terraform

### Steps followed :

1)	Install Terraform on local Windows machine

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/65324e5a-cdad-4f8f-a45f-280f235a113e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f30e1e62-a946-4de4-bc51-6463dcdd0616)

Set the environment variable :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dbdac6ed-0128-426c-8155-32e4a8bb9e5d)

2)	Create an IAM user & get the access key ID & secret key, to be used by AWS CLI. 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/eb5b208e-d5f5-49db-9ef4-e917e782cc69)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a062a51d-bb0b-4e53-afe8-d96f7cf9e0ca)

3)	Create security group & a key-pair to be used by the tf file.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0b43eb31-1e13-4322-90ef-a561c7bc9b60)

4)	Write first_instance.tf file, using details from above

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/edf96f55-4af8-4db3-8447-21c20f035731)

5)	Run terraform init – this will check the provider (aws in this case) & will download the plugins for it

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/78871f96-85e5-45d3-bd0a-047ea979b238)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/99657bdc-7454-4e84-a079-bff63187bdd5)

6)	Run terraform validate to check the syntax of the tf file

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a7335e7e-1df8-4f78-86ba-f77c7bd08cf7)

7)	Run terraform fmt to format the tf file.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1302df62-23d7-4891-b8ed-a43d1a2ca9aa)

8)	Run terraform plan to preview the changes before applying them

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/88eae0db-b9b2-41be-80fe-bef5c1c25df4)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/fc355d46-bf99-47d0-ba16-5eca87bf3db4)

9)	Finally run terraform apply to apply the above changes & confirm yes

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c49a492e-c6a2-4a57-818e-3bcdfecf1d4c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c73d89af-d8e8-4697-9520-5d5b8d96834e)

10)	Check for the launched EC2 Instance & other details as provided above

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7c04485b-e359-455e-9c4c-a4d57dd83aaa)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/967ea176-27ec-4cbf-ac24-969ccb8f095e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/715836ab-5e1b-44ec-a474-bfbae8758ff7)

11)	Open the first_instance.tf file, add a new tag, apply changes & check if new tags is added to the ec2 instance

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8f49997a-d6e1-436f-acb5-c1e52570dd0a)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c3094ec3-0dbd-4309-ae37-b637f27a803f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8d5dd626-569e-44c2-94e8-9dbb00cf9488)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7a085b66-422a-42cf-becc-e48e24e9d6aa)

12)	Do a terraform destroy 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/25217a22-39df-48af-90aa-b00c2e507080)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/33648b2e-13e0-4264-938d-a8784cd8cf5c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0474ae9e-6327-4428-a1bc-aa89f74117ab)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/926cf345-f8ac-45d5-890a-e251b2b1fde7)
