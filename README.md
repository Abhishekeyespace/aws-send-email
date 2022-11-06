# aws-send-email

**Overview**
----
Send-contact-email is a cloud-based internal API developed to support developers for the task of sending automated Emails with Amazon Simple Email Service (AWS SES).

This API belong to the Representational State Transfer (REST) category. The API also supports Cross-Origin Resource Sharing (CORS).

* **Authentication**

	The API uses a Bearer authentication (also called token authentication).The client must send this token in the Authorization header  	(authorizationToken) when making requests to resources.

* **URL**

  https://3mhd6g2pwg.execute-api.ap-southeast-2.amazonaws.com/test/contact

* **Method:**
  
  `POST`


```
* **Success Response:**
  
```json
{
	"statusCode": 200,
	"body": "Email ID: 0108018426760091-4fd1f131-7def-4258-9013-e2df47d5a5d2-000000 sent from Lambda."
}
```

 
* **Error Response:**

```json
{ 
  	"statusCode": 500,
	"Message": ""\"Failed to send email: An error occurred (InvalidParameterValue) when calling the SendEmail operation: Invalid email address .\"""
}
```
OR
  
```json
{ 
  	"statusCode": 403,
	"Message": "User is not authorized to access this resource with an explicit deny"
}
```
OR
  
```json
{ 
  	"statusCode": 400,
	"Message": "Invalid request body"
}
```

* **Send email to a single contact with cc and bcc**

```
https://81qv40h5n6.execute-api.ap-southeast-2.amazonaws.com/test/sendEmail
```


#### JSON body schema

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "email addresses",
    "type": "object",
    "properties": {
        "email-recipient": {
            "type": "string"
        },
        "email-recipient-cc": {
            "type": "string"
        },
        "email-recipient-bcc": {
            "type": "string"
        },
        "email-sender":{
            "type":"string"
        }
        
    },
    "required": ["email-recipient","email-sender"]
}

#### Example Request

```json
POST test/contact HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 35

{
	"email-recipient" : "",
	"email-recipient-cc" : "abhishek+ses1@eye.space",
	"email-recipient-bcc" : "abhishek+ses2@eye.space",
	"email-sender":"abhishek@eye.space"
}
```

#### Example Response

```json
{
	"statusCode": 200,
	"body": "Email ID: 010801842b266d23-0d9cf452-34b3-4718-a8e1-ea7cb2bd8b02-000000 sent from Lambda."
}

```

* **Send email to a multiple contacts**

```
https://81qv40h5n6.execute-api.ap-southeast-2.amazonaws.com/test/send-email-bulk
```

#### JSON body schema

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "email addresses",
    "type": "array",
    "properties": {
        "email-recipient": {
            "type": "string"
        },
        "email-sender":{
            "type":"string"
        }
        
    },
    "required": ["email-recipient","email-sender"]
}


#### Example Request

```json
POST test/contact HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 35

{
	"email-sender":"abhishek@eye.space",
	"email-recipient":["das.abhishek15@gmail.com","abhishek+ses2@eye.space","abhishek+ses1@eye.space"]

}

```

#### Example Response

```json
{
	"statusCode": 200,
	"body": "Email ID: 010801842b266d23-0d9cf452-34b3-4718-a8e1-ea7cb2bd8b02-000000 sent from Lambda."
}

```

* **Send templated email to a multiple contacts**

```
https://81qv40h5n6.execute-api.ap-southeast-2.amazonaws.com/test/send-bulk-templated-email
```
	
#### JSON body schema

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "email addresses",
    "type": "array",
    "properties": {
        "email-recipient": {
            "type": "string"
        },
        "email-sender":{
            "type":"string"
        }
        
    },
    "required": ["email-recipient","email-sender"]
}
  
#### Example Request

```json
POST test/contact HTTP/1.1
Content-Type: application/json
Accept: application/json
Content-Length: 35

{
	"email-sender":"abhishek@eye.space",
	"email-recipient":["das.abhishek15@gmail.com","abhishek+ses2@eye.space","abhishek+ses1@eye.space"]

}

```

#### Example Respone

```json
{
	"Status": [
		{
			"Status": "Success",
			"MessageId": "010801844bd48c02-f47cb54e-7d52-4ab9-bde6-a9ef8aa9a28c-000000"
		}
	],
	"ResponseMetadata": {
		"RequestId": "c153bb1c-be68-44c2-811c-0e31174aec4f",
		"HTTPStatusCode": 200,
		"HTTPHeaders": {
			"date": "Sun, 06 Nov 2022 07:25:31 GMT",
			"content-type": "text/xml",
			"content-length": "473",
			"connection": "keep-alive",
			"x-amzn-requestid": "c153bb1c-be68-44c2-811c-0e31174aec4f"
		},
		"RetryAttempts": 0
	}
}
```



* **Notes:**

AWS SES allows you to send 50 recipients at a time. For e.g if you have 200k recipients you would have to make 4k API calls.

