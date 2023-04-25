---
id: "integration_api_3DS_v2_online_services"
---

# Online Services

For online services merchants (for example gaming), in regard to the Integration API we recommend you to add the following parameter information to Verify User to comply with the 3DS 2 standard. Any additional parameters will be provided by PaymentIQ.

## cardholderAccount - Parameters

:::caution
Cardholder Account Information data elements used to define a time period can be included as either: the specific date or an
approximate indicator for when the action occurred. 3DS Requestors can use either format.
:::

| Parameter             | Required | DataType | Description                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| chAccAgeInd           | Optional | String   | Length of time that the cardholder has had the account with the 3DS Requestor. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No account (guest check-out)** <br/>**• 02 = Created during this transaction** <br/>**• 03 = Less than 30 days** <br/>**• 04 = 30−60 days** <br/>**• 05 = More than 60 days**                                                          |
| chAccDate             | Optional | String   | Date that the cardholder opened the account with the 3DS Requestor. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD**                                                                                                                                                                                                                                 |
| chAccChangeInd        | Optional | String   | Length of time since the cardholder’s account information with the 3DS Requestor was last changed, including Billing or Shipping address, new payment account, or new user(s) added. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = Changed during this transaction** <br/>**• 02 = Less than 30 days** <br/>**• 03 = 30−60 days** <br/>**• 04 = More than 60 days** |
| chAccChange           | Optional | String   | Length of time since the cardholder’s account information with the 3DS Requestor was last changed, including Billing or Shipping address, new payment account, or new user(s) added. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD**                                                                                                                |
| chAccPwChangeInd      | Optional | String   | Indicates the length of time since the cardholder’s account with the 3DS Requestor had a password change or account reset. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No change** <br/>**• 02 = Changed during this transaction** <br/>**• 03 = Less than 30 days** <br/>**• 04 = 30−60 days** <br/>**• 05 = More than 60 days**                                 |
| chAccPwChange         | Optional | String   | Date that cardholder’s account with the 3DS Requestor had a password change or account reset. <br/><br/>**Length: 8 characters** <br/> <br/>**Format accepted:** <br/>**Date format = YYYYMMDD**                                                                                                                                                                                                       |
| suspiciousAccActivity | Optional | String   | Indicates whether the 3DS Requestor has experienced suspicious activity (including previous fraud) on the cardholder account. <br/><br/>**Length: 2 characters** <br/> <br/>**Values accepted:** <br/>**• 01 = No suspicious activity has been observed** <br/>**• 02 = Suspicious activity has been observed**                                                                                        |

<details><summary>Click to view cardholderAccount Examples</summary>
<p>

## Example using specific date cardholder account

```json
{
   "threeDS2": {
      "cardholderAccount": {
         "acctInfo": {
            "chAccDate": "20190101",
            "chAccChange": "20190101",
            "chAccPwChange": "20190101",
            "suspiciousAccActivity": "01"
         }
      }
   }
}
```

## Example using approximate date cardholder account


```json
{
   "threeDS2": {
      "cardholderAccount": {
         "acctInfo": {
            "chAccAgeInd": "02",
            "chAccChangeInd": "01",
            "chAccPwChangeInd": "02",
            "suspiciousAccActivity": "01"
         }
      }
   }
}
```


</p>
</details>
