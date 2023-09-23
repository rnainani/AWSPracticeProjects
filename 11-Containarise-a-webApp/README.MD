# Containarise a webApp

## Pre-requisite : Docker Engine installed on AWS EC2

### Steps followed : 

1)	Create a directory 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b6765660-44b6-4b49-b734-e6bc88bc0fc5)

2)	Get a sample webApp, used tooplate.com in this example & get the downloadable url using inspect element :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3e21b777-ff9f-425c-bebe-7a29ac851ba4)

https://www.tooplate.com/zip-templates/2126_antique_cafe.zip

3)	Download the above zip file in the project directory created above & unzip it. Then archive it.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/416cf1ff-2428-41f7-bc1b-ef9554bb341c)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/870ff7ad-6290-416f-ae8e-ba8c0c5356f1)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/456cedce-6926-4b08-a660-28755aa8d059)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/867617f4-0b4a-4aad-adc8-302d196dc925)

Move tar file 1 level up & remove other zip file & unzipped folder :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/11b254e3-e53c-49e2-981f-c5966aba21b8)

Move the tar file (artifact) to the café project directory :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/95c50071-4578-47b4-9668-e4b55b7c8368)

4)	Write the docker file :

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/741718c3-d08d-471b-8896-909727129429)

FROM – will contain information of base image
LABEL – is just like giving tags in AWS 
ENV – this is to provide environment variable, in this case to avoid interactive run
RUN – instructions to perform some tasks like installation or update package, this can be doneon multiple lines or can be done on same line using ‘&&’. Its advisible to have multiple commands in single line as every RUN there will be a layer created.
CMD – this is to start the process, in this case as we cannot start the service, we need rely on binary, so we need to pass the location of the binary, along with some arguments required
EXPOSE – this is to tell which port will be used by the service.
WORKDIR – this will be directory where a user will be able to run commands after getting attached to the container.
VOLUME – required if want to preserve anything if container is deleted, in this case it will store the logs
ADD – untar the contents & copy
COPY – will simply copy  

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c5612351-5a03-4d54-8699-1bd5ace968ad)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/62d80d6b-1f3a-4560-9dbd-1a8ccb202579)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/71b839d0-978f-4046-bbd1-ce854a24387a)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d3c5b671-31cd-4c3d-a05b-3fc08d7ae8de)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/af4f54c6-3842-4fcc-8cdc-2de05f169d06)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/79af7399-a1b4-4590-bfc7-62fc5f5952a4)

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c7dbcf70-b662-4f72-a263-95b83a36b96a)
