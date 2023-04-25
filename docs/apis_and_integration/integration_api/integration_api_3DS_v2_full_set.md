---
id: "integration_api_3DS_v2_full_set"
---

# Full Set

This is the full list of parameters which you can provide for Verify User in regards to 3DS 2. It is not required to provide these but if they are submitted they will override what is provided by PaymentIQ.

## Example Object Structure with full set of parameter objects.

```json
{
   "threeDS2":{  
      "deviceChannel": "",
      "messageCategory": "",
      "threeDSCompIn": "",
      "threeDSRequestor": {},
      "threeDSRequestorURL": "",
      "cardholderAccount": {},
      "cardholder": {},
      "purchase": {},
      "acquirer": {},
      "merchant": {},
      "browserInformation": {}
   }
}
```



## deviceChannel - Parameters

| Parameter           | Required | DataType | Description                              |
|---------------------|----------|----------|------------------------------------------|
| deviceChannel       | Optional | String   | Indicates the type of channel interface being used to initiate the transaction. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/>**• 01 = App-based (APP)**<br/>**• 02 = Browser (BRW)**<br/>**• 03 = 3DS Requestor Initiated (3RI)**<br/>**• 04–79 = Reserved for EMVCo future use (values invalid until defined by EMVCo)**<br/>**• 80–99 = Reserved for DS use** |

<details><summary>Click to view deviceChannel Example</summary>
<p>

```json
{
   "threeDS2": {
      "deviceChannel": "02",
     // ...
   }
}
```
</p>
</details>

## messageCategory - Parameters

| Parameter           | Required | DataType | Description                              |
|---------------------|----------|----------|------------------------------------------|
| messageCategory     | Optional | String   | Identifies the category of the message for a specific use case. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/>**• 01 = PA**<br/>**• 02 = NPA**<br/>**• 03–79 = Reserved for EMVCo future use (values invalid until defined by EMVCo)**<br/>**• 80–99 = Reserved for DS use** |

<details><summary>Click to view messageCategory Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "messageCategory": "01",
      // ...
   }
}
```
</p>
</details>

## threeDSRequestor - Parameters

| Parameter                                | Required | DataType | Description                              |
|------------------------------------------|----------|----------|------------------------------------------|
| threeDSRequestorAuthenticationInd        | Optional | String   | Indicates the type of Authentication request. <br/>This data element provides additional information to the ACS to determine the best approach for handing an authentication request. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/>**• 01 = Payment transaction**<br/>**• 02 = Recurring transaction**<br/>**• 03 = Instalment transaction**<br/>**• 04 = Add card**<br/>**• 05 = Maintain card**<br/>**• 06 = Cardholder verification as part of EMV token ID&V**<br/>**• 07–79 = Reserved for EMVCo future use (values invalid until defined by EMVCo)**<br/>**• 80–99 = Reserved for DS use** |
| threeDSReqAuthMethod                     | Optional | String   | Mechanism used by the Cardholder to authenticate to the 3DS Requestor. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No 3DS Requestor authentication occurred (i.e. cardholder “logged in” as guest)** <br/>**• 02 = Login to the cardholder account at the 3DS Requestor system using 3DS Requestor’s own credentials** <br/>**• 03 = Login to the cardholder account at the 3DS Requestor system using federated ID** <br/>**• 04 = Login to the cardholder account at the 3DS Requestor system using issuer credentials** <br/>**• 05 = Login to the cardholder account at the 3DS Requestor system using third-party authentication** <br/>**• 06 = Login to the cardholder account at the 3DS Requestor system using FIDO Authenticator** <br/>**• 07 = Login to the cardholder account at the 3DS Requestor system using FIDO Authenticator (FIDO** <br/>**assurance data signed)** <br/>**• 08 = SRC Assurance Data** <br/>**• 09–79 = Reserved for EMVCo future use (values invalid until defined by EMVCo)** <br/>**• 80–99 = Reserved for DS use**   |
| threeDSReqAuthTimestamp                  | Optional | String   | Date and time in UTC of the cardholder authentication. <br/><br/>**Length: 12 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDDHHMM**  |
| threeDSReqAuthData                       | Optional | String   | Data that documents and supports a specific authentication process. <br/> In the current version of the specification, this data element is not defined in detail, however the intention is that for each 3DS Requestor Authentication Method, this field carry data that the ACS can use to verify the authentication process. <br/> For example, if the 3DS Requestor Authentication Method is:<br/>- 03, then this element can carry information about the provider of the federated ID and related information. <br/>- 06, then this element can carry the FIDO attestation data (including the signature). <br/>- 07, then this element can carry FIDO Attestation data with the FIDO assurance data signed. <br/>- 08, then this element can carry the SRC assurance data. <br/><br/>**Length: maximum 20,000 characters** |
| threeDSRequestorChallengeInd             | Optional | String   | Indicates whether a challenge is requested for this transaction. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No preference** <br/>**• 02 = No challenge requested** <br/>**• 03 = Challenge requested (3DS Requestor preference)** <br/>**• 04 = Challenge requested (Mandate)** <br/>**• 05 = No challenge requested (transactional risk analysis is already performed)** <br/>**• 06 = No challenge requested (Data share only)** <br/>**• 07 = No challenge requested (strong consumer authentication is already performed)** <br/>**• 08 = No challenge requested (utilise whitelist exemption if no challenge required)** <br/>**• 09 = Challenge requested (whitelist prompt requested if challenge required)** <br/>**• 10–79 = Reserved for EMVCo future use (values invalid untildefined by EMVCo)** <br/>**• 80–99 = Reserved for DS use** <br/> <br/>**Note: If the element is not provided, the expected action is that the ACSwould interpret as 01 = No** <br/>**preference.** |
| threeDSReqPriorRef                       | Optional | String   | This data element provides additional information to the ACS to determine the best approach for handing a request. <br/><br/>**Length: 36 characters** <br/> <br/>**Value accepted:** <br/>**This data element contains an ACS Transaction ID for a prior authenticated transaction (for example, the first** <br/>**recurring transaction that was authenticated with the cardholder).** |
| threeDSReqPriorAuthMethod                | Optional | String   | Mechanism used by the Cardholder to previously authenticate to the 3DS Requestor. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = Frictionless authentication occurred by ACS** <br/>**• 02 = Cardholder challenge occurred by ACS** <br/>**• 03 = AVS verified** <br/>**• 04 = Other issuer methods** <br/>**• 05–79 = Reserved for EMVCo future use (values invalid until defined by EMVCo)** <br/>**• 80–99 = Reserved for DS use** |
| threeDSReqPriorAuthTimestamp             | Optional | String   | Date and time in UTC of the prior cardholder authentication. <br/><br/>**Length: 12 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDDHHMM** |
| threeDSReqPriorAuthData                  | Optional | String   | Data that documents and supports a specific authentication process. <br/> In the current version of the specification this data element is not defined in detail, however the intention is that for each 3DS Requestor Authentication Method, this field carry data that the ACS can use to verify the authentication process. In future versions of the specification, these details are expected to be included. <br/><br/>**Length: maximum 2048 characters** |

<details><summary>Click to view threeDSRequestor Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "threeDSRequestor": {
         "threeDSRequestorAuthenticationInd": "01",
         "threeDSRequestorAuthenticationInfo": {
            "threeDSReqAuthMethod": "05",
            "threeDSReqAuthTimestamp": "201905280754",
            "threeDSReqAuthData": ""
         },
         "threeDSRequestorChallengeInd": "01",
         "threeDSRequestorPriorAuthenticationInfo": {
            "threeDSReqPriorRef": "ccbafb54-2be3-46fb-8097-21c28034dab9",
            "threeDSReqPriorAuthMethod": "02",
            "threeDSReqPriorAuthTimestamp": "201905280752",
            "threeDSReqPriorAuthData": ""
         }
      },
      // ...
   }
}
```
</p>
</details>

## threeDSRequestorURL - Parameters

| Parameter           | Required | DataType | Description                              |
|---------------------|----------|----------|------------------------------------------|
| threeDSRequestorURL | Optional | String   | Fully qualified URL of 3DS Requestor website or customer care site. <br/> This data element provides additional information to the receiving 3-D Secure system if a problem arises and should provide contact information. <br/><br/>**Length: Variable, maximum 2048 characters** <br/> <br/>**Value accepted:** <br/>**Fully qualified URL** <br/>**For example:** <br/>**http://server.domainname.com** |

<details><summary>Click to view threeDSRequestorURL Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "threeDSRequestorURL": "https://www.example.com",
      // ...
   }
}
```
</p>
</details>

## cardholderAccount - Parameters

:::caution
Cardholder Account Information data elements used to define a time period can be included as either: the specific date or an
approximate indicator for when the action occurred. 3DS Requestors can use either format.
:::

| Parameter             | Required | DataType | Description                              |
|-----------------------|----------|----------|------------------------------------------|
| acctId                | Optional | String   | Additional information about the account optionally provided by the 3DS Requestor. <br/><br/>**Length: Variable, maximum 64 characters** |
| chAccAgeInd           | Optional | String   | Length of time that the cardholder has had the account with the 3DS Requestor. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No account (guest check-out)** <br/>**• 02 = Created during this transaction** <br/>**• 03 = Less than 30 days** <br/>**• 04 = 30−60 days** <br/>**• 05 = More than 60 days** |
| chAccDate             | Optional | String   | Date that the cardholder opened the account with the 3DS Requestor. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD** |
| chAccChangeInd        | Optional | String   | Length of time since the cardholder’s account information with the 3DS Requestor was last changed, including Billing or Shipping address, new payment account, or new user(s) added. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = Changed during this transaction** <br/>**• 02 = Less than 30 days** <br/>**• 03 = 30−60 days** <br/>**• 04 = More than 60 days** |
| chAccChange           | Optional | String   | Length of time since the cardholder’s account information with the 3DS Requestor was last changed, including Billing or Shipping address, new payment account, or new user(s) added. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD** |
| chAccPwChangeInd      | Optional | String   | Indicates the length of time since the cardholder’s account with the 3DS Requestor had a password change or account reset. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No change** <br/>**• 02 = Changed during this transaction** <br/>**• 03 = Less than 30 days** <br/>**• 04 = 30−60 days** <br/>**• 05 = More than 60 days** |
| chAccPwChange         | Optional | String   | Date that cardholder’s account with the 3DS Requestor had a password change or account reset. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD** |
| shipAddressUsageInd   | Optional | String   | Indicates when the shipping address used for this transaction was first used with the 3DS Requestor. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = This transaction** <br/>**• 02 = Less than 30 days** <br/>**• 03 = 30−60 days** <br/>**• 04 = More than 60 days** |
| shipAddressUsage      | Optional | String   | Date when the shipping address used for this transaction was first used with the 3DS Requestor. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD** |
| txnActivityDay        | Optional | String   | Number of transactions (successful and abandoned) for this cardholder account with the 3DS Requestor across all payment accounts in the previous 24 hours. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: maximum 3 characters** |
| txnActivityYear       | Optional | String   | Number of transactions (successful and abandoned) for this cardholder account with the 3DS Requestor across all payment accounts in the previous year. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: maximum 3 characters** |
| provisionAttemptsDay  | Optional | String   | Number of Add Card attempts in the last 24 hours. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: maximum 3 characters** |
| nbPurchaseAccount     | Optional | String   | Number of purchases with this cardholder account during the previous six months. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: maximum 3 characters** |
| suspiciousAccActivity | Optional | String   | Indicates whether the 3DS Requestor has experienced suspicious activity (including previous fraud) on the cardholder account. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No suspicious activity has been observed** <br/>**• 02 = Suspicious activity has been observed** |
| shipNameIndicator     | Optional | String   | Indicates if the Cardholder Name on the account is identical to the shipping Name used for this transaction. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = Account Name identical to shipping Name** <br/>**• 02 = Account Name different than shipping Name** |
| paymentAccInd         | Optional | String   | Indicates the length of time that the payment account was enrolled in the cardholder’s account with the 3DS Requestor. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No account (guest check-out)** <br/>**• 02 = During this transaction** <br/>**• 03 = Less than 30 days** <br/>**• 04 = 30−60 days** <br/>**• 05 = More than 60 days** |
| paymentAccAge         | Optional | String   | Date that the payment account was enrolled in the cardholder’s account with the 3DS Requestor. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD** |

<details><summary>Click to view cardholderAccount Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "cardholderAccount": {
         "acctId": "",
         "acctInfo": {
            "chAccAgeInd": "",
            "chAccDate": "",
            "chAccChangeInd": "",
            "chAccChange": "",
            "chAccPwChangeInd": "",
            "chAccPwChange": "",
            "shipAddressUsageInd": "",
            "shipAddressUsage": "",
            "txnActivityDay": "43",
            "txnActivityYear": "130",
            "provisionAttemptsDay": "1",
            "nbPurchaseAccount": "75",
            "suspiciousAccActivity": "",
            "shipNameIndicator": "",
            "paymentAccInd": "03",
            "paymentAccAge": "20190506"
         }
      },
      // ...
   }
}
```
</p>
</details>

## cardholder - Parameters

| Parameter           | Required | DataType | Description                              |
|---------------------|----------|----------|------------------------------------------|
| addrMatch           | Optional | String   | Indicates whether the Cardholder Shipping Address and Cardholder Billing Address are the same. <br/><br/>**Length: 1 character**<br/><br/>**Values accepted:**<br/>**• Y = Shipping Address matches BillingAddress**<br/>**• N = Shipping Address does not match Billing Address**  |
| billAddrCity        | Optional | String   | The city of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters** |
| billAddrCountry     | Optional | String   | The country of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: 3 characters**<br/><br/>**Value accepted:**<br/>**Shall be the ISO 3166-1 numeric three-digit country code** |
| billAddrLine1       | Optional | String   | First line of the street address or equivalent local portion of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters** |
| billAddrLine2       | Optional | String   | Second line of the street address or equivalent local portion of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters** |
| billAddrLine3       | Optional | String   | Third line of the street address or equivalent local portion of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters** |
| billAddrPostCode    | Optional | String   | ZIP or other postal code of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 16 characters** |
| billAddrState       | Optional | String   | The state or province of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 3 characters**<br/><br/>**Value accepted:**<br/>**Should be the country subdivision code defined in ISO 3166-2.** |
| shipAddrCity        | Optional | String   | City portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters** |
| shipAddrCountry     | Optional | String   | Country of the shipping address requested by the Cardholder. <br/><br/>**Length: 3 characters**<br/><br/>**Value accepted:**<br/>**ISO 3166-1 three-digit country code** |
| shipAddrLine1       | Optional | String   | First line of the street address or equivalent local portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters** |
| shipAddrLine2       | Optional | String   | The second line of the street address or equivalent local portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters** |
| shipAddrLine3       | Optional | String   | The third line of the street address or equivalent local portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters** |
| shipAddrPostCode    | Optional | String   | The ZIP or other postal code of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 16 characters** |
| shipAddrState       | Optional | String   | The state or province of the shipping address associated with the card being used for this purchase. <br/><br/>**Length: Variable: maximum 3 characters**<br/><br/>**Value accepted:**<br/>**Should be the country subdivision code defined in ISO 3166-2.** |
| email               | Optional | String   | The email address associated with the account that is either entered by the Cardholder, or is on file with the 3DS Requestor. <br/><br/>**Length: Variable, maximum 254 characters**<br/><br/>**Value accepted:**<br/>**Shall meet requirements of Section 3.4 of IETF RFC 5322.** |
| cc                  | Optional | String   | Country Code of the mobilePhone/"homePhone/workPhone number. <br/>**Length: Variable, 1–3 characters**<br/><br/>**Values accepted:**<br/>**Refer to ITU-E.164 for additional information on format and length.** |
| subscriber          | Optional | String   | Subscriber sections of the mobilePhone/"homePhone/workPhone number. <br/>**Length: Variable, 15 characters**<br/><br/>**Values accepted:**<br/>**Refer to ITU-E.164 for additional information on format and length.** |
| cardholderName      | Optional | String   | Name of the Cardholder. <br/><br/>**Length: Variable, 2–45 characters**<br/><br/>**Value accepted:**<br/>**Alphanumeric special characters, listed in EMV Book 4, “Appendix B”.** |

<details><summary>Click to view cardholder Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "cardholder": {
         "addrMatch": "",
         "billAddrCity": "Stockholm",
         "billAddrCountry": "752",
         "billAddrLine1": "Storgatan 1",
         "billAddrLine2": "",
         "billAddrLine3": "",
         "billAddrPostCode": "12345",
         "billAddrState": "AB",
         "shipAddrCity": "",
         "shipAddrCountry": "",
         "shipAddrLine1": "",
         "shipAddrLine2": "",
         "shipAddrLine3": "",
         "shipAddrPostCode": "",
         "shipAddrState": "",
         "email": "kalle.andersson@example.com",
         "mobilePhone": {
            "cc": "46",
            "subscriber": "733123456"
         },
         "homePhone": {
            "cc": "",
            "subscriber": ""
         },
         "workPhone": {
            "cc": "",
            "subscriber": ""
         },
         "cardholderName": "Kalle Andersson"
      },
      // ...
   }
}
```
</p>
</details>

## purchase - Parameters

Please note that it is strongly recommended (but still optional) to include Merchant Risk Indicator (See 3DS 2.0 spec section A.7.2).

| Parameter            | Required | DataType | Description                              |
|----------------------|----------|----------|------------------------------------------|
| purchaseInstalData   | Optional | String   | Indicates the maximum number of authorisations permitted for instalment payments. <br/><br/>**Length: Variable, maximum 3 characters**<br/><br/>**Values accepted:**<br/>**Value shall be greater than 1**<br/>**Example values accepted:**<br/>**• 2**<br/>**• 02**<br/>**• 002** |
| shipIndicator        | Optional | String   | Indicates shipping method chosen for the transaction. <br/> Merchants must choose the Shipping Indicator code that most accurately describes the cardholder’s specific transaction, not their general business. <br/> If one or more items are included in the sale, use the Shipping Indicator code for the physical goods, or if all digital goods, use the Shipping Indicator code that describes the most expensive item. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/>**• 01 = Ship to cardholder’s billing address**<br/>**• 02 = Ship to another verified address on file with merchant**<br/>**• 03 = Ship to address that is different than the cardholder’s billing address**<br/>**• 04 = “Ship to Store” / Pick-up at local store (Store address shall be populated in shipping address fields)**<br/>**• 05 = Digital goods (includes online services, electronic gift cards and redemption codes)**<br/>**• 06 = Travel and Event tickets, not shipped**<br/>**• 07 = Other (for example, Gaming, digital services not shipped, emedia subscriptions, etc.)**           |
| deliveryTimeframe    | Optional | String   | Indicates the merchandise delivery timeframe. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/>**• 01 = Electronic Delivery**<br/>**• 02 = Same day shipping**<br/>**• 03 = Overnight shipping**<br/>**• 04 = Two-day or more shipping**            |
| deliveryEmailAddress | Optional | String   | For Electronic delivery, the email address to which the merchandise was delivered. <br/><br/>**Length: maximum 254 characters**            |
| reorderItemsInd      | Optional | String   | Indicates whether the cardholder is reordering previously purchased merchandise. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = First time ordered** <br/>**• 02 = Reordered**             |
| preOrderPurchaseInd  | Optional | String   | Indicates whether Cardholder is placing an order for merchandise with a future availability or release date. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/>**• 01 = Merchandise available**<br/>**• 02 = Future availability**           |
| preOrderDate         | Optional | String   | For a pre-ordered purchase, the expected date that the merchandise will be available. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD**             |
| giftCardAmount       | Optional | String   | For prepaid or gift card purchase, the purchase amount total of prepaid or gift card(s) in major units (for example, USD 123.45 is 123). <br/><br/>**Length: maximum 15 characters**           |
| giftCardCurr         | Optional | String   | For prepaid or gift card purchase, ISO 4217 three-digit currency code of the gift card. <br/><br/>**Length: 3 characters, numeric**           |
| giftCardCount        | Optional | String   | For prepaid or gift card purchase, total count of individual prepaid or gift cards/codes purchased. <br/><br/>**Length: 2 characters**            |
| purchaseAmount       | Optional | String   | Purchase amount in minor units of currency with all punctuation removed. <br/><br/>**Length: Variable, maximum 48 characters** <br/> <br/>**Example: purchase amount is USD 123.45,** <br/>**Example values accepted:** <br/>**• 12345** <br/>**• 012345** <br/>**• 0012345**  |
| purchaseCurrency     | Optional | String   | Currency in which purchase amount is expressed. <br/><br/>**Length: 3 characters, numeric** |
| purchaseExponent     | Optional | String   | Minor units of currency as specified in the ISO 4217 currency exponent. <br/><br/>**Length: 1 character** |
| purchaseDate         | Optional | String   | Date and time of the purchase expressed in UTC. <br/><br/>**Length: 14 characters** <br/> <br/>**Format accepted:** <br/>**YYYYMMDDHHMMSS**  |
| recurringExpiry      | Optional | String   | Date after which no further authorisations shall be performed. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**YYYYMMDD**  |
| recurringFrequency   | Optional | String   | Indicates the minimum number of days between authorisations. <br/><br/>**Length: Variable, maximum 4 characters** <br/> <br/>**Example values accepted:** <br/>**• 31** <br/>**• 031** <br/>**• 0031** |
| transType            | Optional | String   | Identifies the type of transaction being authenticated. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = Goods/ Service Purchase** <br/>**• 03 = Check Acceptance** <br/>**• 10 = Account Funding** <br/>**• 11 = Quasi-Cash Transaction** <br/>**• 28 = Prepaid Activation and Load** <br/>**Note: Values derived fromthe 8583 ISO Standard.**  |

<details><summary>Click to view purchase Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "purchase": {
         "purchaseInstalData": "",
         "merchantRiskIndicator": {
            "shipIndicator": "",
            "deliveryTimeframe": "",
            "deliveryEmailAddress": "",
            "reorderItemsInd": "",
            "preOrderPurchaseInd": "",
            "preOrderDate": "",
            "giftCardAmount": "",
            "giftCardCurr": "",
            "giftCardCount": ""
         },
         "purchaseAmount": "17600",
         "purchaseCurrency": "978",
         "purchaseExponent": "2",
         "purchaseDate": "20190528075426",
         "recurringExpiry": "",
         "recurringFrequency": "",
         "transType": ""
      },
      // ...
   }
}
```
</p>
</details>

## acquirer  - Parameters

| Parameter          | Required | DataType | Description                              |
|--------------------|----------|----------|------------------------------------------|
| acquirerBin        | Optional | String   | Acquiring institution identification code as assigned by the DS receiving the AReq message. <br/><br/>**Length: Variable, maximum 11 characters** <br/> <br/>**Value accepted:** <br/>**This value correlates to the Acquirer BIN as defined by each Payment System or DS.**   |
| acquirerMerchantId | Optional | String   | Acquirer-assigned Merchant identifier. <br/><br/>**Length: Variable, maximum 35 characters** <br/> <br/>**Value accepted:** <br/>**Individual Directory Servers may impose specific format and character requirements on the contents of this field.**  |

<details><summary>Click to view acquirer Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "acquirer": {
         "acquirerBin": "12345",
         "acquirerMerchantId": "123456"
      },
      // ...
   }
}
```
</p>
</details>

## merchant - Parameters

| Parameter           | Required | DataType | Description                              |
|---------------------|----------|----------|------------------------------------------|
| mcc                 | Optional | String   | DS-specific code describing the Merchant’s type of business, product or service. <br/><br/> **Length: 4 characters**<br/><br/> **This value correlates to the Merchant Category Code as defined by each Payment System or DS** |
| merchantCountryCode | Optional | String   | Country Code of the Merchant. This value correlates to the Merchant Country Code as defined by each Payment System or DS. <br/><br/>**Length: 3 characters**<br/><br/>**ISO 3166-1 numeric three-digit country code**<br/><br/>**Note: The same value must be used in the authorisation request.** |
| merchantName        | Optional | String   | Merchant name assigned by the Acquirer or Payment System. <br/><br/>**Length: Variable, maximum 40 characters**<br/>**Same name used in the authorisation message as defined in ISO 8583.**|

<details><summary>Click to view merchant Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "merchant": {
         "mcc": "7995",
         "merchantCountryCode": "752",
         "merchantName": "TestMerchant",
      },
      // ...
   }
}
```
</p>
</details>

## browserInformation - Parameters

Please note that if these are submitted via the Front API as well, those parameters will be used.


| Parameter           | Required | DataType | Description                              |
|---------------------|----------|----------|------------------------------------------|
| browserAcceptHeader | Required | String   | Exact content of the HTTP accept headers as sent to the 3DS Requestor from the Cardholder’s browser. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: Variable, maximum 2048 characters** <br/> <br/>**Value accepted:** <br/>**If the total length of the accept header sent by the browser exceeds 2048 characters, the 3DS Server truncates the excess portion**  |
| browserIP           | Required | String   | IP address of the browser as returned by the HTTP headers to the 3DS Requestor. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: Variable, maximum 45 characters** <br/> <br/>**Value accepted:** <br/> **• IPv4 address is represented in the dotted decimal format of 4 sets of decimal numbers separated by dots. The decimal number in each and every set is in the range 0 to 255.**<br/>**Example IPv4 address: 1.12.123.255** <br/>**• IPv6 address is represented as eight groups of four hexadecimal digits, each group representing 16 bits (two octets. The groups are separated by colons (:).** <br/>**Example IPv6 address:2011:0db8:85a3:0101:0101:8a2e:0370:7334**  |
| browserJavaEnabled  | Required | Boolean  | Boolean that represents the ability of the cardholder browser to execute Java. <br/><br/>**Values accepted:**<br/>**• true**<br/>**• false**                                         |
| browserLanguage     | Required | String   | Value representing the browser language as defined in IETF BCP47. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: Variable, 1–8 characters**                                         |
| browserColorDepth   | Required | String   | Value representing the bit depth of the color palette for displaying images, in bits per pixel. <br/><br/>**Length: 1–2 characters**<br/><br/>**Values accepted:**<br/>**• 1 = 1 bit**<br/>**• 4 = 4 bits**<br/>**• 8 = 8 bits**<br/>**• 15 = 15 bits**<br/>**• 16 = 16 bits**<br/>**• 24 = 24 bits**<br/>**• 32 = 32 bits**<br/>**• 48 = 48 bits**                                         |
| browserScreenHeight | Required | String   | Total height of the Cardholder’s screen in pixels. <br/><br/>**Length: Variable, 1–6 characters; Numeric**                                         |
| browserScreenWidth  | Required | String   | Total width of the cardholder’s screen in pixels. <br/><br/>**Length: Variable, 1–6 characters; Numeric**                                         |
| browserTZ           | Required | String   | Time-zone offset in minutes between UTC and the Cardholder browser local time. <br/> Note that the offset is positive if the local time zone is behind UTC and negative if it is ahead. <br/><br/>**Length: Variable, 1–5 characters** <br/><br/> **Value accepted: Value is returned from the getTimezoneOffset() method.** <br/> **Example time zone offset values in minutes:**<br/>**If UTC -5 hours:**<br/>**• 300**<br/>**• +300**<br/>**If UTC +5 hours:**<br/>**• -300**                                        |
| browserUserAgent    | Required | String   | Exact content of the HTTP user-agent header. Provided by PaymentIQ, can be overridden. <br/><br/>**Length: Variable, maximum 2048 characters** <br/> <br/>**Value accepted:** <br/>**Note: If the total length of the User-Agent sent by the browser exceeds 2048 characters, the 3DS Server truncates the excess portion.**  |
| challengeWindowSize | Optional | String   | Dimensions of the challenge window that has been displayed to the Cardholder. The ACS shall reply with content that is formatted to appropriately render in this window to provide the best possible user experience. <br/> Preconfigured sizes are width x height in pixels of the window displayed in the Cardholder browser window. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = 250 x 400** <br/>**• 02 = 390 x 400** <br/>**• 03 = 500 x 600** <br/>**• 04 = 600 x 400** <br/>**• 05 = Full screen**  |

<details><summary>Click to view browserInformation Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "browserInformation": {
         "browserAcceptHeader": "*/*",
         "browserIP": "127.0.0.1",
         "browserJavaEnabled": "false",
         "browserLanguage": "en-GB",
         "browserColorDepth": "24",
         "browserScreenHeight": "768",
         "browserScreenWidth": "1366",
         "browserTZ": "0",
         "browserUserAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36",
         "challengeWindowSize": ""
      }
   }
}
```
</p>
</details>

