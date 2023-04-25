---
id: "example_req_res"
---

# Example API Request And Response

Parameters that are optional can be ignored or set to null. All parameters, both in the request and response, are case sensitive. The order of the parameters does not matter.

Example of JSON POST request:

```json
POST /api/verifyuser HTTP/1.1
User-Agent: Wget/1.6
Host: www.example.com
Content-Type: application/json
Accept: application/json
{
"sessionId": "s9wefk2392masgp",
"userId": "1234567"
}
```

Example of JSON response:

```json
HTTP/1.1 200 OK
Connection: close
Content-Length: 23
Content-Type: application/json
Date: Sat, 08 Jan 2010 12:04:08 GMT
Server: Sun Java System Application Server 9.1_02
{
"userId": "1234567",
"success": false,
"errCode": "123",
"errMsg": "Unknown userId"
}
```
