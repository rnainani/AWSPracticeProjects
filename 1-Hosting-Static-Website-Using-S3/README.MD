# Hosting a Static Website Using S3

## Agenda : To host a very basic static webiste using S3 bucket

### Steps followed :

1) Create an S3 bucket & upload the index.html & error.html file to it.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ecaa8332-b388-43fa-9442-606ce469d196)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/77218933-2cf3-4bdc-bcaf-f7ab5db5eb89)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6452b9cf-5478-456c-afcc-5c85ecdd78d7)

2) For the bucket, go to properties, make sure static website hosting is enabled & provide the index & error document uploaded above.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/61137559-7867-4292-9aa6-b9f497119757)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cd156a50-6779-4887-94cf-2fcd8bfd39da)

3) Go to permissions & make the block public access Off.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e3a3e901-9541-44cb-82a2-c02df20b11d1)

4) Again inside permissions, edit bucket policy & add bucket persmission in JSON to make the bucket public.
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/bdea4730-b749-4ca4-870d-d8a969647232)

5) Under properties, go to static website hostic section & grab the bucket website hosting endpoint url & paste it in browser 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c3725ab4-7006-4a2a-ba99-196ae03b87a4)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a2008b40-1b75-4879-a012-70940169b93c)

6) Add some invalid character in the url to test for the error page

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/abe9608a-817a-4808-8823-81cd7e065dc5)

