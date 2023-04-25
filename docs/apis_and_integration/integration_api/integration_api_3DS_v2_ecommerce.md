---
id: "integration_api_3DS_v2_ecommerce"
---

# E-commerce

## cardholderAccount - Parameters

:::caution
Cardholder Account Information data elements used to define a time period can be included as either: the specific date or an
approximate indicator for when the action occurred. 3DS Requestors can use either format.
:::

| Parameter             | Required | DataType | Description                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| chAccAgeInd           | Optional | String   | Length of time that the cardholder has had the account with the 3DS Requestor. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = No account (guest check-out)**<br/><br/>**• 02 = Created during this transaction**<br/><br/>**• 03 = Less than 30 days**<br/><br/>**• 04 = 30−60 days**<br/><br/>**• 05 = More than 60 days**                                                     |
| chAccDate             | Optional | String   | Date that the cardholder opened the account with the 3DS Requestor. <br/><br/>**Length: 8 characters**<br/><br/>**Format accepted:**<br/><br/>**Date format = YYYYMMDD**                                                                                                                                                                                                                                            |
| chAccChangeInd        | Optional | String   | Length of time since the cardholder’s account information with the 3DS Requestor was last changed, including Billing or Shipping address, new payment account, or new user(s) added.<br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = Changed during this transaction**<br/><br/>**• 02 = Less than 30 days**<br/><br/>**• 03 = 30−60 days**<br/><br/>**• 04 = More than 60 days** |
| chAccChange           | Optional | String   | Length of time since the cardholder’s account information with the 3DS Requestor was last changed, including Billing or Shipping address, new payment account, or new user(s) added. <br/><br/>**Length: 8 characters**<br/><br/>**Format accepted:**<br/><br/>**Date format = YYYYMMDD**                                                                                                                           |
| chAccPwChangeInd      | Optional | String   | Indicates the length of time since the cardholder’s account with the 3DS Requestor had a password change or account reset.<br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = No change**<br/><br/>**• 02 = Changed during this transaction**<br/><br/>**• 03 = Less than 30 days**<br/><br/>**• 04 = 30−60 days**<br/><br/>**• 05 = More than 60 days**                             |
| chAccPwChange         | Optional | String   | Date that cardholder’s account with the 3DS Requestor had a password change or account reset. <br/><br/>**Length: 8 characters**<br/><br/>**Format accepted:**<br/><br/>**Date format = YYYYMMDD**                                                                                                                                                                                                                  |
| shipAddressUsageInd   | Optional | String   | Indicates when the shipping address used for this transaction was first used with the 3DS Requestor. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = This transaction**<br/><br/>**• 02 = Less than 30 days**<br/><br/>**• 03 = 30−60 days**<br/><br/>**• 04 = More than 60 days**                                                                                               |
| shipAddressUsage      | Optional | String   | Date when the shipping address used for this transaction was first used with the 3DS Requestor. <br/><br/>**Length: 8 characters**<br/><br/>**Format accepted:**<br/><br/>**Date format = YYYYMMDD**                                                                                                                                                                                                                |
| suspiciousAccActivity | Optional | String   | Indicates whether the 3DS Requestor has experienced suspicious activity (including previous fraud) on the cardholder account. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = No suspicious activity has been observed**<br/><br/>**• 02 = Suspicious activity has been observed**                                                                                               |
| shipNameIndicator     | Optional | String   | Indicates if the Cardholder Name on the account is identical to the shipping Name used for this transaction. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = Account Name identical to shipping Name**<br/><br/>**• 02 = Account Name different than shipping Name**                                                                                                             |

<details><summary>Click to view cardholderAccount Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "cardholderAccount": {
         "acctInfo": {
            "chAccAgeInd": "",
            "chAccDate": "",
            "chAccChangeInd": "",
            "chAccChange": "",
            "chAccPwChangeInd": "",
            "chAccPwChange": "",
            "shipAddressUsageInd": "",
            "shipAddressUsage": "",
            "suspiciousAccActivity": "",
            "shipNameIndicator": "",
            }
      },
      // ...
   }
}
```
</p>
</details>

## cardholder - Parameters

| Parameter        | Required | DataType | Description                                                                                                                                                                                                                                                                                  |
|------------------|----------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| addrMatch        | Optional | String   | Indicates whether the Cardholder Shipping Address and Cardholder Billing Address are the same. <br/><br/>**Length: 1 character**<br/><br/>**Values accepted:**<br/><br/>**• Y = Shipping Address matches BillingAddress**<br/><br/>**• N = Shipping Address does not match Billing Address** |
| billAddrCity     | Optional | String   | The city of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                                                                            |
| billAddrCountry  | Optional | String   | The country of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: 3 characters**<br/><br/>**Value accepted:**<br/><br/>**Shall be the ISO 3166-1 numeric three-digit country code**                                                         |
| billAddrLine1    | Optional | String   | First line of the street address or equivalent local portion of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                        |
| billAddrLine2    | Optional | String   | Second line of the street address or equivalent local portion of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                       |
| billAddrLine3    | Optional | String   | Third line of the street address or equivalent local portion of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                        |
| billAddrPostCode | Optional | String   | ZIP or other postal code of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 16 characters**                                                                                                                            |
| billAddrState    | Optional | String   | The state or province of the Cardholder billing address associated with the card used for this purchase. <br/><br/>**Length: Variable, maximum 3 characters**<br/><br/>**Value accepted:**<br/><br/>**Should be the country subdivision code defined in ISO 3166-2.**                        |
| shipAddrCity     | Optional | String   | City portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                                                                                                      |
| shipAddrCountry  | Optional | String   | Country of the shipping address requested by the Cardholder. <br/><br/>**Length: 3 characters**<br/><br/>**Value accepted:**<br/><br/>**ISO 3166-1 three-digit country code**                                                                                                                |
| shipAddrLine1    | Optional | String   | First line of the street address or equivalent local portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                                                      |
| shipAddrLine2    | Optional | String   | The second line of the street address or equivalent local portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                                                 |
| shipAddrLine3    | Optional | String   | The third line of the street address or equivalent local portion of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 50 characters**                                                                                                                  |
| shipAddrPostCode | Optional | String   | The ZIP or other postal code of the shipping address requested by the Cardholder. <br/><br/>**Length: Variable, maximum 16 characters**                                                                                                                                                      |
| shipAddrState    | Optional | String   | The state or province of the shipping address associated with the card being used for this purchase. <br/><br/>**Length: Variable: maximum 3 characters**<br/><br/>**Value accepted:**<br/><br/>**Should be the country subdivision code defined in ISO 3166-2.**                            |
| email            | Optional | String   | The email address associated with the account that is either entered by the Cardholder, or is on file with the 3DS Requestor. <br/><br/>**Length: Variable, maximum 254 characters**<br/><br/>**Value accepted:**<br/><br/>**Shall meet requirements of Section 3.4 of IETF RFC 5322.**      |
| cc               | Optional | String   | Country Code of the mobilePhone/"homePhone/workPhone number.<br/><br/>**Length: Variable, 1–3 characters**<br/><br/>**Values accepted:**<br/><br/>**Refer to ITU-E.164 for additional information on format and length.**                                                                    |
| subscriber       | Optional | String   | Subscriber sections of the mobilePhone/"homePhone/workPhone number.<br/><br/>**Length: Variable, 15 characters**<br/><br/>**Values accepted:**<br/><br/>**Refer to ITU-E.164 for additional information on format and length.**                                                              |

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
      },
   // ...
   }
}
```
</p>
</details>

## purchase - Parameters

Please note that it is strongly recommended (but still optional) to include Merchant Risk Indicator (See 3DS 2 spec section A.7.2).

| Parameter            | Required | DataType | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------|----------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| shipIndicator        | Optional | String   | Indicates shipping method chosen for the transaction.<br/><br/>Merchants must choose the Shipping Indicator code that most accurately describes the cardholder’s specific transaction, not their general business.<br/><br/>If one or more items are included in the sale, use the Shipping Indicator code for the physical goods, or if all digital goods, use the Shipping Indicator code that describes the most expensive item. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = Ship to cardholder’s billing address**<br/><br/>**• 02 = Ship to another verified address on file with merchant**<br/><br/>**• 03 = Ship to address that is different than the cardholder’s billing address**<br/><br/>**• 04 = “Ship to Store” / Pick-up at local store (Store address shall be populated in shipping address fields)**<br/><br/>**• 05 = Digital goods (includes online services, electronic gift cards and redemption codes)**<br/><br/>**• 06 = Travel and Event tickets, not shipped**<br/><br/>**• 07 = Other (for example, Gaming, digital services not shipped, emedia subscriptions, etc.)** |
| deliveryTimeframe    | Optional | String   | Indicates the merchandise delivery timeframe. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = Electronic Delivery**<br/><br/>**• 02 = Same day shipping**<br/><br/>**• 03 = Overnight shipping**<br/><br/>**• 04 = Two-day or more shipping**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| deliveryEmailAddress | Optional | String   | For Electronic delivery, the email address to which the merchandise was delivered. <br/><br/>**Length: maximum 254 characters**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| reorderItemsInd      | Optional | String   | Indicates whether the cardholder is reordering previously purchased merchandise. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = First time ordered**<br/><br/>**• 02 = Reordered**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| preOrderPurchaseInd  | Optional | String   | Indicates whether Cardholder is placing an order for merchandise with a future availability or release date. <br/><br/>**Length: 2 characters**<br/><br/>**Values accepted:**<br/><br/>**• 01 = Merchandise available**<br/><br/>**• 02 = Future availability**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| preOrderDate         | Optional | String   | For a pre-ordered purchase, the expected date that the merchandise will be available. <br/><br/>**Length: 8 characters**<br/><br/>**Format accepted:**<br/><br/>**Date format = YYYYMMDD**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| giftCardAmount       | Optional | String   | For prepaid or gift card purchase, the purchase amount total of prepaid or gift card(s) in major units (for example, USD 123.45 is 123). <br/><br/>**Length: maximum 15 characters**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| giftCardCurr         | Optional | String   | For prepaid or gift card purchase, ISO 4217 three-digit currency code of the gift card. <br/><br/>**Length: 3 characters, numeric**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| giftCardCount        | Optional | String   | For prepaid or gift card purchase, total count of individual prepaid or gift cards/codes purchased. <br/><br/>**Length: 2 characters**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

<details><summary>Click to view purchase Example</summary>
<p>

```json
{
   "threeDS2": {
      // ...
      "purchase": {
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
         }
      },
      // ...
   }
}
```
</p>
</details>
