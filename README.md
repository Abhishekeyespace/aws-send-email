# aws-send-email

**Overview**
----
Send-contact-email is a cloud-based internal API developed to support developers for the task of sending automated Emails with Amazon Simple Email Service (AWS SES).

This API belong to the Representational State Transfer (REST) category. The API also supports Cross-Origin Resource Sharing (CORS).

**Authentication**
----
The API uses a Bearer authentication (also called token authentication).The client must send this token in the Authorization header (authorizationToken) when making requests to resources.

* **URL**

  https://3mhd6g2pwg.execute-api.ap-southeast-2.amazonaws.com/test/contact

* **Method:**
  
  `POST`

  `GET` | `POST` | `DELETE` | `PUT`
  
*  **URL Params**

   <_If URL params exist, specify them in accordance with name mentioned in URL section. Separate into optional and required. Document data constraints._> 

   **Required:**
 
   `id=[integer]`

   **Optional:**
 
   `photo_id=[alphanumeric]`

* **Data Params**
```
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
```
* **Success Response:**
  


  * **Code:** 200 <br />
    **Content:** 
    ```
    {
	"body": "Email ID: 0108018426760091-4fd1f131-7def-4258-9013-e2df47d5a5d2-000000 sent from Lambda."
  }
```
 
* **Error Response:**

  <_Most endpoints will have many ways they can fail. From unauthorized access, to wrongful parameters etc. All of those should be liste d here. It might seem repetitive, but it helps prevent assumptions from being made where they should be._>

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{ error : "Log in" }`

  OR

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `{ error : "Email Invalid" }`

* **Sample Call:**

  <_Just a sample call to your endpoint in a runnable format ($.ajax call or a curl request) - this makes life easier and more predictable._> 

* **Notes:**

  <_This is where all uncertainties, commentary, discussion etc. can go. I recommend timestamping and identifying oneself when leaving comments here._> 
