# Hosting a Static Website Using Amazon S3 (and Amazon Route 53)

## Agenda : To host a very basic static webiste using S3 bucket

### Steps followed :

1) Create an S3 bucket & upload the index.html & error.html file to it.

![image1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ecaa8332-b388-43fa-9442-606ce469d196)

![image4](https://private-user-images.githubusercontent.com/25031921/241382419-ecaa8332-b388-43fa-9442-606ce469d196.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTEiLCJleHAiOjE2OTQ1Mjg5MTcsIm5iZiI6MTY5NDUyODYxNywicGF0aCI6Ii8yNTAzMTkyMS8yNDEzODI0MTktZWNhYTgzMzItYjM4OC00M2ZhLTk0NDItNjA2Y2U0NjlkMTk2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFJV05KWUFYNENTVkVINTNBJTJGMjAyMzA5MTIlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjMwOTEyVDE0MjMzN1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTRjNDI4N2U0OTNkNTA3NzFmNGM3ZGVlNDE4OTUyMjI2OTcyZWE4ZmJhZTFkYWJjYjEyOGYwOGQ5NTQyZWNjYzUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.2-C618wPPZ2XihaCHzCluk_8RHiHhwOxaVut3iyVujU)

![image2](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/77218933-2cf3-4bdc-bcaf-f7ab5db5eb89)

![image3](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6452b9cf-5478-456c-afcc-5c85ecdd78d7)

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

### Note - In addition to above steps, under Route 53 we can create an A record against an hosted domain (any website, like example .com etc.) & can Route its traffic to the bucket created above by selecting the "Alias to S3 website endpoint" 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d0086ded-5277-4c44-a5a2-daca91f7cfb9)
