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



* **Data Params**
```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "User",
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

* **Sample Request and Response:**

## Example Request

```
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

## Example Response

```json
{
	"statusCode": 200,
	"body": "Email ID: 010801842b266d23-0d9cf452-34b3-4718-a8e1-ea7cb2bd8b02-000000 sent from Lambda."
}

```
  

* **Notes:**

