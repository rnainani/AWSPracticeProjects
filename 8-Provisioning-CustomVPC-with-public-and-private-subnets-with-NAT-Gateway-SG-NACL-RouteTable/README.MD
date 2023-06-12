# Provisioning a Custom VPC with a public and a private subnet, with NAT Gateway, Security Groups, NACL, RouteTable & Internet Gateway

## Agenda - To download the security updates / patches in th DB Server in private subnet using NAT gateway

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3efeceff-d603-4b55-b14a-011deb4c722f)


### Steps followed 

### 1) Create VPC 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ab00ca25-8924-4c05-ba78-945ffdd02c05)

VPC created with main Route table & main NACL :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/978722ec-2f3e-4548-8208-035d0680817c)

New Security group is also created : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a9276b96-cc94-4512-a5c7-b4292c6e1484)

### 2) Create Subnets

Public Subnet :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/63a3ecd8-b837-403b-94ea-58d6dfc2b465)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c765bc43-ff4c-445b-be8c-22888f2e965a)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/02925ea0-4556-4f98-875b-14c557eae688)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e1219a1c-6ab5-42ea-b39c-0071b44c49c1)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cb6e94ed-aa20-4ab4-9cc3-7744074afc6b)


Private Subnet :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/77feb274-7d62-432b-8392-1abe0dd6e14a)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/71ca4bd7-590c-4f62-ae5b-1af29d23d3fb)

### 3) Create Internet Gateway

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dd845350-004e-4e79-8baa-606a774cd6a2)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e95fd995-f830-4125-b70b-d7b01ec9c489)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c6f8cf3c-2ff6-4269-af41-699dbb445c27)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/aa916954-8661-4958-a6b3-b2830b76ee61)

### 4) Create a Route Table

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/229492b1-1297-4871-8b35-8042b083617b)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cb6091db-c2c7-4aa0-84a1-cf02428daab7)

Create a route out to the internet : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0c9b3e57-2f8e-43ab-8138-539f436ae0e1)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4e0aca91-0f2a-4b7b-8cbd-649cf18b627f)

Associate public subnet :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a9209250-65a6-4aec-aef4-1a62f32346c3)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/93c8e98a-f9dd-428a-931b-4d83cc35603a)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/63ad9645-20bb-4060-9958-95b9dee33796)

### 5) Create EC2 instance in both the subnets

Public Instance & Security Group : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/094ba2d8-f948-473e-aaf4-5727484c8572)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6eeafebd-701d-4185-a0b1-ca873475831c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f6ae83ca-9567-4361-be4d-6b5b09028349)

Private Instance & Security Group :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6a4fb4d5-f1b2-46d4-9aeb-2a6232ff3169)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4df30b1f-ee03-49c0-af47-7b6046a59465)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/fec0126e-7b26-4035-9a7c-d0d2936c3e7f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/538ce60f-aa9b-4424-bf2b-b31cb10b2943)

### 6) Create NAT Gateway

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2294736c-d4e4-4d86-83da-969d24d9a769)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/fb5354e8-0156-4748-a9f3-36176bfa017c)

### 7) Create a route out to internet in the Main route table

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a05c9c11-d625-4642-80dd-4715f0db528e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d867817f-79c3-45d4-ae01-f4e8df52b41c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f48c5b4b-113a-4509-b1cf-57b9c074a995)

### 8) SSH to DB Server from the Web Server & access the internet to download updates 

Connect the Web Server using the cludshell:

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/01215321-4c3f-42e4-a644-1c9af7a9581d)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6e4a970e-9498-4fa6-898b-fa54ff673d26)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a4092a7d-cbfd-4832-96f3-486a4a4ac70e)

Grab the private IP of the DB Server & ping from the Web server : 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/70d6cf8b-f0cc-4626-a1f6-7e21687a209f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2e72db52-f172-4895-b396-021bb1b3fc23)

create a key & use it to SSH to the DB Server :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dc0f6790-7cbd-4781-a888-e710c43456f8)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f5bc8f24-805d-41b2-bebf-df0d099bd49f)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0cf84724-5f9a-4246-a39b-15aba5e563ba)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b8aeadae-d46a-4869-a897-23a68d2b86fb)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cfb29f44-20d3-4e34-aaa8-ec224705b3fd)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c06ee1b9-d2b6-42be-8612-18468dd5f3d3)

