--- 
id: "spark" 
title: "Spark"
hide_title: "true"
---
 
![](/img/providers/logos/spark.png)

# Spark

## About
Spark is a wallet provider offering solutions to pay and receive money with your Spark account. 

:::warning  NOTE

Please note that Spark does not support gaming.

:::

| Provider Name                | Spark                                       |
|------------------------------|---------------------------------------------|
| Link                         | -                                           |
| Classification               | E-Wallet                                    |
| Regions                      | `India`                                     |
| Currencies                   | `INR`                                       |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/> `SparkWithdrawal` |
| PaymentIQ Configuration File | `SparkConfig`                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.spark.SparkConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <notificationPassword>???</notificationPassword>
        <merchantName>???</merchantName>
        <beneficiaryLogoUrl>https://www.example.com/image</beneficiaryLogoUrl>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.spark.SparkConfig>
```

</details>

### Attributes

| Attribute            | Description                                    |
|----------------------|------------------------------------------------|
| username             | Provided by Spark. "User ID"                   |
| apiKey               | Provided by Spark. "sparkkey"                  |
| secretKey            | Provided by Spark. "sparkkeypasscode"          |
| notificationPassword | Webhook secret. Configured in Spark Backoffice |
| merchantName         | Will be displayed at checkout                  |
| benificiaryLogoUrl   | URL to logo that will be displayed in checkout |

### Notes
- Spark supports two ways of handling withdrawals approvals, auto or manual. Manual approvals are default and they must be done through Spark Backoffice. For easier handling, this should be set to auto on Spark's side so that PaymentIQ will handle the complete approval flow.

## Example Routing Rules
![](/img/providers/routing/spark-dp.png)
![](/img/providers/routing/spark-wd.png)

## Test Information

| Phone number | Password   |
|--------------|------------|
| 4123412341   | XLta9bDwvP |

- New test Spark Customer Accounts can also be created in the checkout page.

- Please note that for card deposits during the spark transaction use the following card test credentials and OTP. [https://developer.paytm.com/docs/testing-integration/](https://developer.paytm.com/docs/testing-integration/)
