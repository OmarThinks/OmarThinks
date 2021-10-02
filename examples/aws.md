# AWS-Full-Stack-Project

Releases: https://github.com/OmarThinks/AWS-Full-Stack-Project/tags








# A) Table of Deployments Links:


## Note:

**I will shut these links down when I am done with the application.  
I will turn every thing off so that I do not get out of AWS Free Tier.  
Keeping these links alive might get me out of AWS Free Tier.**



<table>
	<tr>
		<th></th>
		<th>Link</th>
	</tr>
	<tr>
		<th>Amplify Frontend (With React)</th>
		<td>
			<a href="https://dev9463.d1pi9xfkfb20dm.amplifyapp.com">
				https://dev9463.d1pi9xfkfb20dm.amplifyapp.com
			</a>
		</td>
	</tr>
	<tr>
		<th>AWS API Gateway (Backend)</th>
		<td>
			<a href="https://67nbvuy3t1.execute-api.us-east-2.amazonaws.com/dev/">
				https://67nbvuy3t1.execute-api.us-east-2.amazonaws.com/dev/
			</a>
		</td>
	</tr>
</table>











# B) Technologies Used:


<b>

1. AWS
	1. Amazon API Gateway
	2. Amazon DynamoDB (NoSQL DB)
	3. AWS Lambda (Serverless)
	4. IAM (Identity)
	5. AWS Amplify (Frontend) (With React Application)
2. JavaScript
	1. NodeJS
		1. React
3. Python
4. Postman

</b>






# C) Architicture:




<img src="images/arch.gif">






## C-1) AWS Amplify (With React):

**https://dev9463.d1pi9xfkfb20dm.amplifyapp.com/**  

This is the link of the Frontend Application with **React**.  
You can input first name and last name.

<img src="images/amplify.gif">





## C-2) AWS-Lambda Function:


This is a very basic lambda function.  
- Inputs (JSON):
	- firstName (String)
	- lastName (String)
- Output:
	- "Hello from Lambda, " + firstname + lastName
- Example:
	- Input:
```json
{
  "firstName": "Omar",
  "lastName": "Magdy"
}
```
	- Output:
```json
{
  "statusCode": 200,
  "body": "\"Hello from Lambda, Omar Magdy\""
}
```





## C-3) Amazon API Gateway:


<img src="images/gateway.gif">




- https://67nbvuy3t1.execute-api.us-east-2.amazonaws.com/dev  
	- Method: POST
	- Reuest Body: JSON
	- Inputs:
		- firstName (String)
		- lastName (String)

Example:  

Input:

```bash
curl --location --request POST 'https://67nbvuy3t1.execute-api.us-east-2.amazonaws.com/dev' \
--header 'Content-Type: application/json' \
--data-raw '{
    "firstName":"Omar",
    "lastName":"Magdy"
}'
```
I have also used a Postman collection to test the request.  

Output:


```bash
{
    "statusCode": 200,
    "body": "\"Hello from Lambda, Omar Magdy\""
}
```








<img src="images/postman.gif">







## C-4) DynamoDB and IAM:


I have made the permissions that anyone can access and delete 
the data in the DynamoDB Database.  
This is the permissions JSON.

```JSON
{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "<Database ARN>"
    }
    ]
}
```

<img src="images/iam.gif">

And this is the New python code:


```python
import json
import boto3
from time import gmtime, strftime

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('HelloWorldDatabase')
now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())

def lambda_handler(event, context):
    name = event['firstName'] +' '+ event['lastName']
    response = table.put_item(
        Item={
            'ID': name,
            'LatestGreetingTime':now
            })
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda, ' + name)
    }
```


<img src="images/lambda.gif">


There is a unique ID to each record.




<img src="images/dynamo.gif">

























# D) Reference:

I used these guides to help me develop an aoolication by myself.
1. https://aws.amazon.com/getting-started/learning-path-full-stack-developer/
2. https://aws.amazon.com/getting-started/hands-on/build-react-app-amplify-graphql/











