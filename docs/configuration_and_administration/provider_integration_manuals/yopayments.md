--- 
id: "yopayments" 
title: "Yo! Payments"
hide_title: "true"
---
 
![](/img/providers/logos/yopayments.png)

# Yo! Payments

## About
Yo! Payments is a mobile payments gateway service. Yo! Payments enables businesses to receive payments from their customers via mobile money, as well as make mobile money payments to any mobile money account holder.

| Provider Name                | Yo! Payments                                                   |
|------------------------------|----------------------------------------------------------------|
| Link                         | [https://paymentsweb.yo.co.ug/](https://paymentsweb.yo.co.ug/) |
| Classification               | Mobile Payment                                                 |
| Regions                      | `Uganda`                                                       |
| Currencies                   | `UGX`                                                          |
| Methods/PaymentTxTypes       | `YopaymentsDeposit` <br/> `YopaymentsWithdrawal`               |
| PaymentIQ Configuration File | `YopaymentsConfig`                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.yopayments.YopaymentsConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <accountID>??</accountID>
        <username>??</username>
        <password>??</password>
        <secretKey>??</secretKey>
         <serviceEndpoint>http://41.220.12.206/services/yopaymentsdev/task.php</serviceEndpoint>
         <supportedCurrencies>UGX</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Devcode_PaymentIQ_YoUganda</defaultDescriptor>
</com.devcode.paymentiq.integration.yopayments.YopaymentsConfig>
```
</details>

### Attributes

| Attribute           | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| accountID           | AccountNumber                                                               |
| username            | API Username                                                                |
| password            | API Password                                                                |
| secretKey           | the SecretKey need to be created and sent to Yopaymnet at: support@yo.co.ug |
| supportedCurrencies | Yo!Payments - Yo!Uganda only support UGX currency.                          |

## Example Routing Rule

![](/img/providers/routing/yopayments.png)

## Test Information

Yopayments test number, using Sandbox, any digits will be fine so long as they are 	in the required format and belong to the prefix of one of the mobile networks we support i.e.

- 25670XXXXXXX

- 25675XXXXXXX for Airtel

- 25677XXXXXXX

- 25678XXXXXXX for MTN.

Kindly replace the Xs with digits of your choice. Please make sure you first deposit virtual funds on your account before you perform a withdrawal transaction.
