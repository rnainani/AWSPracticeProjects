# Build a Serverless application using Amazon API Gateway, Amazon Lambda & Amazon DynamoDB 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/553bf8e6-3165-4d02-aa42-0573e3da91c2)

Create an API, hosted on API Gateway, with backen on Lambda, & database on DynamoDB. 4 Operations done on microservices :

1) Insert some data
2) Read that data
3) Update that data
4) Delete that data

Create a resource (DynamoDBManager) and define a method (POST) on it. The method is backed by a Lambda function (LambdaFunctionOverHttps). That is, when you call the API through an HTTPS endpoint, Amazon API Gateway invokes the Lambda function.

The method on the DynamoDBManager resource will support DynamoDB operations. The request payload sent in the POST request identifies the DynamoDB operation and provides necessary data.

### Steps followed :

1) Create Lambda IAM Role. Create the execution role that gives the function permission to access AWS resources.

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/028155e8-ad27-4962-a9e7-be113f6d333e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3e2c07fd-38b9-4bc0-b564-b2b006aef980)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/cefe5e90-c187-42f5-b968-a841510990e2)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1d3826fe-912d-4266-8eec-4c6062f36260)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7b445e93-9b3e-419c-88d7-325e499086d3)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0bde0558-d053-457c-b54e-7c4c770e4558)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ffb4a048-1a66-4c7a-9886-e9ea8fc54ddc)

2) Create Lambda Function & add the code 

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d6a2a530-0b64-4c5b-a3d6-119f1fd58bb6)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/bc5d6a97-2f1f-4a43-a46b-d6638c729cf1)

3) Test Lambda Function

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6c3158fd-f531-4b81-8168-a62790c68e0d)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/52b06785-2661-417c-a6ab-fba7911f1af1)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9283b34f-0bda-4940-a101-a9240600d9f4)

4) Create DynamoDB Table

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3e92e3d0-41ed-4650-be21-fb379b7689c1)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/78ca05ca-81cf-45e2-8a11-a666e15c8726)

5) Create API

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1a020542-0ac4-4017-a765-dc7a5a8389f9)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/deeb2c8b-9009-4efe-a84a-c685ed354e51)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8e10a2e5-dde9-47c6-90bf-5b99968bd729)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f77a805a-c33d-4b4d-8312-50c7a350b9f7)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/8c28aaeb-d255-494b-a4e6-8ddd14ba0056)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/2b7fc9b6-200d-4246-92f3-bfed579dbb3c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/487a2809-03f6-4997-9158-65df12ef4266)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/9964539c-49fc-4240-8dfe-3bed5c6caa19)

With above step API integration is done.

6) Deploy the API

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6cb4402f-78ad-4284-8552-a5dc299996dc)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/567d6171-2759-4fdd-9f4b-8da7af10bd00)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6a409966-435c-41e2-a37a-fc1802afa8fd)

### Running our solution - using Postman

The Lambda function supports using the create operation to create an item in your DynamoDB table. To request this operation, use the following JSON:

```json
{
    "operation": "create",
    "tableName": "lambda-apigateway",
    "payload": {
        "Item": {
            "id": "1234ABCD",
            "number": 5
        }
    }
}
```
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/6aa27a16-00f4-425f-9ff9-439165367c3c)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0ff80a1c-029e-42d3-b012-e04c6c83f5f6)

To get all the inserted items from the table, we can use the "list" operation of Lambda using the same API. Pass the following JSON to the API, and it will return all the items from the Dynamo table

```json
{
    "operation": "list",
    "tableName": "lambda-apigateway",
    "payload": {
    }
}
```
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/dbba6eff-9314-49b3-8358-109c9915330e)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d41ec4cf-687c-4ccd-8aae-ac6a35301fd8)

### Cleanup

1) Dynamo DB

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1eb83fd7-8cd0-42d0-aa7f-1cc646c325b9)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/eeb92673-dd4e-43f5-9db5-e26f687cf506)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/00fbdda2-c998-47a5-a8b4-8f29ffb64c43)

2) Lambda

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/387a6aeb-fb6f-4ef5-952c-b2dabb6a2821)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/12e864b1-e8bf-42e0-b420-dd37dec2122a)

3) API Gateway

![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c9359514-80cf-4963-94e5-7e35350c3e74)
![image](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/097dec33-ac53-44c4-b8c0-b472392a77bb)




