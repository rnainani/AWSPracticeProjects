# Hosting a Static Website Using Amazon S3 (and Amazon Route 53)

## Agenda : To host a very basic static webiste using S3 bucket

### Steps followed :

1) Create an S3 bucket & upload the index.html & error.html file to it.

![1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/591fcea4-b2d0-4f29-9e50-826819132832)

![2](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2b834136-b7a4-4ea8-9a93-8b2ada3979fa)

![3](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b5c28c30-cfa9-4d1b-a045-f1e9de75f348)

2) For the bucket, go to properties, make sure static website hosting is enabled & provide the index & error document uploaded above.

![4](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/19503984-7271-45d1-8576-4b14b72511fb)

![5](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6c04aeaf-b91c-45a3-956a-d5043564abb8)

3) Go to permissions & make the block public access Off.

![6](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5c3e4cf2-ebbd-4563-a1b7-148f32ded54b)

4) Again inside permissions, edit bucket policy & add bucket persmission in JSON to make the bucket public.
![7](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2c7c38d7-1fc1-4c1b-988a-4380741c227c)

5) Under properties, go to static website hostic section & grab the bucket website hosting endpoint url & paste it in browser 

![8](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d168b5e9-e793-46bb-b073-02b4d8cf6214)
![9](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8e59b21c-7ffa-4352-80ee-7b9fc7622172)

6) Add some invalid character in the url to test for the error page

![10](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9948551e-7958-4bad-ac52-7a7e094bb4ba)

### Note - In addition to above steps, under Route 53 we can create an A record against an hosted domain (any website, like example .com etc.) & can Route its traffic to the bucket created above by selecting the "Alias to S3 website endpoint" 

![11](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2e68848e-04d5-4ed1-9162-b5731e4dcb77)
