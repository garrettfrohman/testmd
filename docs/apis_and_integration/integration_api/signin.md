---
id: "signin"
---

# signin

This method is called by PaymentIQ send KYC data that it has received from 1-click provider. The merchant needs to decide if the user is allowed to sign in or not. For most identity providers the sign in notification is optional to implement.

`POST/paymentiq/signin`

## Example Request
```json
{
  "txRefId": "123",
  "name": "Test testsson",
  "identityProvider": "bankid-se",
  "iat": "1564065831",
  "rat": "1564065831"
}
```

## Request Parameters


| Name             | Locates In | Description                                                                                                                | Schema | Required |
|------------------|------------|----------------------------------------------------------------------------------------------------------------------------|--------|----------|
| txRefId          | body       | The unique id for the sign in request made<br/>_Example:_ `"123"`                                                          | string | Yes      |
| name             | body       | Full name<br/>_Example:_ `"Test testsson"`                                                                                 | string | Yes      |
| firstName        | body       | First name (we add this if we get a name with one space)<br/>_Example:_ `"Test"`                                           | string | No       |
| lastName         | body       | Last name (we add this if we get a name with one space)<br/>_Example:_ `"Testsson"`                                        | string | No       |
| personid         | body       | An ID that uniquely identifies the account holder (some countries does not allow personid)<br/>_Example:_ `"198001012020"` | string | No       |
| gender           | body       | One of: MALE, FEMALE, X, UNKNOWN<br/>_Example:_ `"male"`                                                                   | string | No       |
| street           | body       | Street address<br/>_Example:_ `"Testroad 1"`                                                                               | string | No       |
| City             | body       | City<br/>_Example:_ `"Stockholm"`                                                                                          | string | No       |
| zip              | body       | Postal zip code<br/>_Example:_ `"12345"`                                                                                   | string | No       |
| country          | body       | Country code, 3-letter ISO standard, e.g SWE<br/>_Example:_ `"SWE"`                                                        | string | No       |
| dob              | body       | Date of birth, formatted YYYY-MM-DD, e.g 1981-01-01<br/>_Example:_ `"1980-01-01"`                                          | string | No       |
| ip               | body       | User’s IP-address<br/>_Example:_ `""`                                                                                      | string | No       |
| picture          | body       | Base64 encoded picture of the user(only valid for identity providers that return pictures)<br/>_Example:_ `""`             | string | No       |
| identityProvider | body       | The name of the identity provider used by merchant/user<br/>_Example:_ `"bankid-se"`                                       | string | Yes      |
| iat              | body       | issued at -timestamp<br/>_Example:_ `"1564065831"`                                                                         | string | Yes      |
| rat              | body       | requested at -timestamp<br/>_Example:_ `"1564065831"`                                                                      | string | Yes      |
| attributes       | body       | The attributes provided during the initial sign in request made from the merchant<br/>_Example:_ `""`                      | Object | No       |


## Example Response

### Successful Response

```json
{
  "userId": "user_123",
  "success": true,
  "sessionId": "Example string",
  "balance": "100.50",
  "balanceCy": "SEK",
}
```

### Failed Response
```json
{
  "userId": "user_123",
  "success": false,
  "sessionId": "Example string",
  "balance": "100.50",
  "balanceCy": "SEK",
  "errCode": "210003",
  "errMsg": "Invalid user"
}
```

## Response Parameters

| Name      | Description                                                                                                                                                   | Schema  | Required |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| userId    | Unique user id mapped in the Operator Platform. Will be needed to provider better user experience for future subsequent requests.<br/>_Example:_ `"user_123"` | string  | Yes      |
| success   | True or false. If false then only the two last parameters will be appended                                                                                    | boolean | Yes      |
| sessionId | SessionId generated at operator platform. PIQ will include this when redirecting end user to operator redirect_uri.<br/>_Example:_ `""`                       | string  | No       |
| balance   | Current balance<br/>_Example:_ `100.5`                                                                                                                        | number  | No       |
| balanceCy | Balance currency. 3-letter code according to ISO 4217, e.g SEK. Note: This currency controls the user's currency in PaymentIQ.<br/>_Example:_ `"SEK"`         | string  | No       |
| errCode   | If success false: Custom error code<br/>_Example:_ `"210003"`                                                                                                 | number  | No       |
| errMsg    | If success false: Custom error message<br/>_Example:_ `"Invalid user"`                                                                                        | string  | No       |
