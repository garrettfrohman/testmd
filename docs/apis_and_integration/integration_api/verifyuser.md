---
id: "verifyuser"
---

# verifyuser

This method is called by PaymentIQ to verify that a user is properly authenticated and retrieve user data like name, address, birth-date etc. The user data is needed internally by PaymentIQ for various fraud checks and also to enrich the data sent to the Payment Provider. 

`POST/paymentiq/verifyuser`

## Example Request

```json
{
  "sessionId": "123",
  "userId": "user_123"
}
```

## Request Parameters

| Name      | Located In | Description                                                                                     | Schema | Required |
|-----------|------------|-------------------------------------------------------------------------------------------------|--------|----------|
| sessionId | body       | User's session-id, originating from merchant<br/>_Example:_ `"123"`                             | string | Yes      |
| userId    | body       | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"` | string | Yes      |

## Example Response

```json
{
  "userId": "user_123",
  "success": false,
  "userCat": "VIP_SE",
  "kycStatus": "Approved",
  "sex": "UNKNOWN",
  "firstName": "John",
  "lastName": "Jonsson",
  "street": "Exampel street 1",
  "city": "Stockholm",
  "state": "Stockholm or ISO 2 abbreviated state for countries where this is applicable",
  "zip": "177 32",
  "country": "SWE",
  "email": "test@example.com",
  "dob": "1981-01-01",
  "mobile": "+46733123123",
  "balance": 100.5,
  "balanceCy": "SEK",
  "locale": "sv_SE",
  "attributes": {
    "allow_manual_payout": "true"
  },
  "errCode": "210003",
  "errMsg": "Transaction failed"
}
```

## Response Parameters

| Name       | Description                                                                                                                                                                                                                                    | Schema  | Required |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| userId     | User-id should be unique and constant over time. It will be the same as the request parameter userId.<br/>_Example:_ `"user_123"`                                                                                                              | string  | Yes      |
| success    | True or false. If false then only the two last parameters will be appended                                                                                                                                                                     | boolean | Yes      |
| userCat    | Your user category. It can be any value, e.g VIP_SE, NEW_USER. The value will be displayed in the column 'User cat' in the transaction report. The value can also be used in the rule engine. <br/>_Example:_ `"VIP_SE"`                       | string  | No*      |
| kycStatus  | Your KYC status for the user. It can be any value, e.g. Reject, Approved, Unknown. The value will be displayed in the column KYC Status in the transaction report. The KYC status can also be used in rule engine.<br/>_Example:_ `"Approved"` | string  | No*      |
| sex        | Sex<br/>_Enum:_ `"MALE"`, `"FEMALE"`, `"UNKNOWN"`, `"X"`<br/>_Example:_ `"UNKNOWN"`                                                                                                                                                            | string  | No*      |
| firstName  | First name<br/>_Example:_ `"John"`                                                                                                                                                                                                             | string  | Yes      |
| lastName   | Last name<br/>_Example:_ `"Jonsson"`                                                                                                                                                                                                           | string  | Yes      |
| street     | Street<br/>_Example:_ `"Exampel street 1"`                                                                                                                                                                                                     | string  | No*      |
| city       | City<br/>_Example:_ `"Stockholm"`                                                                                                                                                                                                              | string  | No*      |
| state      | State<br/>_Example:_ `"Stockholm or ISO 2 abbreviated state for countries where this is applicable"`                                                                                                                                           | string  | No*      |
| zip        | Postal zip code<br/>_Example:_ `"177 32"`                                                                                                                                                                                                      | string  | No*      |
| country    | Country code, 3-letter ISO standard, e.g SWE<br/>_Example:_ `"SWE"`                                                                                                                                                                            | string  | No*      |
| email      | User's email<br/>_Example:_ `"test@example.com"`                                                                                                                                                                                               | string  | No*      |
| dob        | Date of birth, formatted YYYY-MM-DD<br/>_Example:_ `"1981-01-01"`                                                                                                                                                                              | string  | No*      |
| mobile     | Mobile number including country code<br/>_Example:_ `"+46733123123"`                                                                                                                                                                           | string  | No*      |
| balance    | Current balance<br/>_Example:_ `100.5`                                                                                                                                                                                                         | number  | No*      |
| balanceCy  | Balance currency. 3-letter code according to ISO 4217, e.g SEK. Note: This currency controls the user's currency in PaymentIQ.<br/>_Example:_ `"SEK"`                                                                                          | string  | No*      |
| locale     | User's preferred locale, according to http://en.wikipedia.org/wiki/Locale, e.g `sv_SE`<br/>_Example:_ `"sv_SE"`                                                                                                                                | string  | No*      |
| attributes | Additional non-standard user specific parameters<br/>_Example:_ `{"allow_manual_payout":"true"}`                                                                                                                                               | string  | No*      |
| errCode    | If success false: Custom error code<br/>_Example:_ `"210003"`                                                                                                                                                                                  | number  | No*      |
| errMsg     | If success false: Custom error message<br/>_Example:_ `"Transaction failed"`                                                                                                                                                                   | string  | No*      |

:::danger *
The minimum required response for verify user needs to contain Balance (can be zero), BalanceCy, UserId and Success. The other parameter requirements will depend on they type of transaction.

Most transaction types will require several other parameters and we **strongly** recommend you return all listed parameters in your verifyuser response. This way you can be certain that the transaction flow has been fully tested and should work.
:::