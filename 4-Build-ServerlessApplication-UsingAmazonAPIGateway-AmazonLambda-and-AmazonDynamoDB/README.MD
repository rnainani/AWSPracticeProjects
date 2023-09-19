# Build a Serverless application using Amazon API Gateway, Amazon Lambda & Amazon DynamoDB 

![1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/eb26abcc-9d52-457a-aea8-e8217e6e0ef6)

Create an API, hosted on API Gateway, with backen on Lambda, & database on DynamoDB. 4 Operations done on microservices :

1) Insert some data
2) Read that data
3) Update that data
4) Delete that data

Create a resource (DynamoDBManager) and define a method (POST) on it. The method is backed by a Lambda function (LambdaFunctionOverHttps). That is, when you call the API through an HTTPS endpoint, Amazon API Gateway invokes the Lambda function.

The method on the DynamoDBManager resource will support DynamoDB operations. The request payload sent in the POST request identifies the DynamoDB operation and provides necessary data.

### Steps followed :

1) Create Lambda IAM Role. Create the execution role that gives the function permission to access AWS resources.

![2](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3fd33e5a-8cdf-434f-a2a4-99e47546dd8f)
![3](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0c7889a1-d408-42a2-a49a-7c82aa3530b7)
![4](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0d0fb1ce-43f4-4d6b-a384-af8dc3bd9f8b)
![5](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c0881d5d-8c46-482a-b26c-2a3eeb36db2a)
![6](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/d0912dc6-33f2-4873-a4fb-f96b59468c2f)
![7](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ecfa189a-d5d9-4337-bbc3-e8c1f58e1f1a)
![8](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e81260cf-2d2e-4dc6-b625-c5ad64b86906)

2) Create Lambda Function & add the code 

![9](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ddf90f7b-f277-427d-9cbe-c244e8de97ab)
![10](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/5b786e78-9ae3-4db7-be7a-68be4ade8ad1)

3) Test Lambda Function

![11](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7fd22b06-d647-43d5-a75c-f66b1cbb1202)
![12](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/b5cb8620-e564-4e3e-a2be-2167c25bb000)
![13](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ab9d3810-21af-4d1a-bd90-c7694e7cae45)

4) Create DynamoDB Table

![14](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/29c89b5b-4c63-4c0c-a3e7-e8b2e1b66cf3)
![15](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a7c0fae2-11ed-49ce-ae55-3bba4d039378)

5) Create API

![16](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ddb382a4-2d84-478e-9647-f0fa46aaba36)
![17](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3cd4d8f4-8a19-425a-8834-3a3ce4c82108)
![18](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e1f7854c-d5f2-4be7-8501-f53de151e134)
![19](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/3feda34f-b2a2-410d-874c-a477476cbf81)
![20](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/e1757a88-d65b-4160-b249-bebcb755a416)
![21](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/689a5d27-ecd4-48d7-a0cc-9c0242a4b91b)
![22](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/abd9ad84-eb05-4a34-ae5e-c35dc307926c)
![23](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/989e1808-fedc-4014-92d5-abca58999296)

With above step API integration is done.

6) Deploy the API

![23_1](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f618d3ab-0563-4ce2-b00d-8e3c41dde653)
![24](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/0990b0f5-a7f9-4914-b7d6-0cfe77a342b0)
![25](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/a19625ac-778c-48a4-a109-b6746f4110c9)

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
![26](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f3e3739c-2326-4c15-b423-e9110bf9badb)
![27](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/7a4a65ed-802d-45c1-8380-80861ab27625)

To get all the inserted items from the table, we can use the "list" operation of Lambda using the same API. Pass the following JSON to the API, and it will return all the items from the Dynamo table

```json
{
    "operation": "list",
    "tableName": "lambda-apigateway",
    "payload": {
    }
}
```
![28](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/68d2085d-9f19-44c2-a84b-ef055e6e8a7b)
![29](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/4e9b6c14-25c0-4cc8-a3ea-47e8e9c99c60)

### Cleanup

1) Dynamo DB

![30](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/63e8f0d6-e839-4210-a840-95f383d176ff)
![31](https://github.com/rnainani/AWSPracticeProjects/assets/25031921/64be1824-2a7c-4fcb-9219-454d90646fec)
<img width="570" alt="32" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/c9a0da8e-b7f8-4e17-8767-84fb4b9f8ede">

2) Lambda

<img width="571" alt="33" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/87260401-13e3-4e02-825c-3310786bb636">

<img width="465" alt="34" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/f5493ae7-ef98-42ed-8379-bcb4502fcb38">


3) API Gateway

<img width="568" alt="35" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/ae3aaffa-56d2-4ba1-a149-aa00a547ab98">

<img width="351" alt="36" src="https://github.com/rnainani/AWSPracticeProjects/assets/25031921/1a4c4261-ee47-4805-9c61-ecfbec3589a3">





