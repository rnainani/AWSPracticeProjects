# Provisioning a Custom VPC with a public and a private subnet, with NAT Gateway, Security Groups, NACL, RouteTable & Internet Gateway

## Agenda - To download the security updates / patches in th DB Server in private subnet using NAT gateway

<img width="608" alt="1" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ef6f8824-a81b-47c1-b296-2fa7aa76daf0">


### Steps followed 

### 1) Create VPC 

<img width="463" alt="2" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2199ea02-20b9-43eb-b616-0aeaeb6134ef">

VPC created with main Route table & main NACL :

<img width="760" alt="3" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/25a492f2-0f5b-4c53-bcb2-845dcf8986a8">

New Security group is also created : 

<img width="759" alt="4" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2be9bd6e-73ab-4173-8fe9-962b80f7c39e">

### 2) Create Subnets

Public Subnet :

<img width="423" alt="5" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a0eb4ddd-3a19-4ee9-9820-089c6a0e8492">

<img width="758" alt="6" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e50b6ca6-86e5-405c-84cb-4bf23f553c42">

<img width="632" alt="7" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7e92bfc6-7462-48e6-8d33-3b026dbd0767">

<img width="647" alt="8" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/de6c4908-d754-41cf-a46f-06c8d68e7f07">

<img width="647" alt="9" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8c5b9067-a80f-49b6-8f39-5d1eaccf6634">


Private Subnet :

<img width="437" alt="10" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a7e927c7-8b4a-45b1-8ef5-b94aca4f3a98">

<img width="764" alt="11" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9ce17369-be1e-4052-8aa3-9adae233cf95">

### 3) Create Internet Gateway

<img width="478" alt="12" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/90ce4ce9-6551-4314-be34-fef3fedf2457">

<img width="759" alt="13" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/89600004-0c15-4891-88a5-1997b5d23149">

<img width="644" alt="14" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ed3ee560-d44c-44db-aeec-2279adfeed4a">

<img width="760" alt="15" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/838d66bf-7bde-47b3-b2cc-94f650aceb58">

### 4) Create a Route Table

<img width="572" alt="16" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/228c5e98-a9b1-4e20-89fb-57ff210c6255">

<img width="759" alt="17" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0a30b51f-7168-4377-9ab3-190d862aa93d">

Create a route out to the internet : 

<img width="768" alt="18" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7ab271d3-715a-4fd8-82e5-dd16f82e3fc4">

<img width="764" alt="19" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/67ba50ec-4bb3-4dfb-807c-83d1f613e8bf">

Associate public subnet :

<img width="761" alt="20" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c2fd4e93-27ab-42b5-ab5a-a552961111d4">

<img width="760" alt="21" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5c49a1b6-5d29-4a60-a6c8-618c29445f76">

<img width="570" alt="22" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/361c1f84-a2c9-4176-bdd1-2353801fadeb">

### 5) Create EC2 instance in both the subnets

Public Instance & Security Group : 

<img width="472" alt="23" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f5529074-10de-4a2a-b748-b085770ddd2d">

<img width="366" alt="24" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5a860897-6eab-4e20-bcb6-646061f5d41a">

<img width="748" alt="25" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f50d2367-7860-4435-985c-a5fcff6dd5a1">

Private Instance & Security Group :

<img width="365" alt="26" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/22902d65-1cc8-476c-90e7-5bb190b5a91b">

<img width="375" alt="27" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a8683ce4-4d4f-4273-a0a6-507730af36f3">

<img width="378" alt="28" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/889df212-ce8c-4f8a-a85b-01cb963e4ae0">

<img width="760" alt="29" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/fd5de388-6ff1-49c0-9b4e-22e66f0e6195">

### 6) Create NAT Gateway

<img width="423" alt="30" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c0e9d09a-b569-4f01-a60f-7576cd0b6eab">

<img width="759" alt="31" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f0e3c2bc-cb7c-475f-a87e-4b971d6686b9">

### 7) Create a route out to internet in the Main route table

<img width="759" alt="32" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b6a616c3-8ba4-4d3f-b043-d9176d87fbfa">

<img width="358" alt="33" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1bc35b39-34cf-4f0f-936f-7732100691b2">

<img width="755" alt="34" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/136e335d-6189-4c8b-a242-3331d3d57bf3">

### 8) SSH to DB Server from the Web Server & access the internet to download updates 

Connect the Web Server using the cludshell:

<img width="761" alt="35" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d54e22b1-ff9c-4494-82d5-3e0e64e711d6">

<img width="438" alt="36" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dd64998e-86b1-49f3-9bb1-1fc88d0a30a5">

<img width="454" alt="37" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4ae89dc1-197b-4657-b577-92f359364b02">

Grab the private IP of the DB Server & ping from the Web server : 

<img width="760" alt="38" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/46b59030-c336-42d9-917a-9c3c5d7f8279">

<img width="559" alt="39" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/53b086be-6046-4392-b2cf-97e6ea3659db">

create a key & use it to SSH to the DB Server :

<img width="306" alt="40" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/617c078a-243a-4c6c-ab09-facd5941dc29">

<img width="458" alt="41" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ce14ecc9-958d-4c55-a25d-c586d6173d4a">

<img width="315" alt="42" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/55938727-4177-442b-9cb3-6b523717c901">

<img width="560" alt="43" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c66f44bd-0df3-43f9-8558-cfb50b9d2998">

<img width="479" alt="44" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d3191371-be83-425c-a607-caf61cc737b7">

<img width="538" alt="45" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6d0d86e7-83ee-441c-8012-6e9bdb971de0">
