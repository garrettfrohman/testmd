--- 
id: "moneymatrix" 
title: "MoneyMatrix"
hide_title: "true"
---
 
![](/img/providers/logos/moneymatrix.png)

# MoneyMatrix

## About
MoneyMatrix is an aggregator that offers a number of alternative payment methods using their hosted payment page.

| Provider Name                | MoneyMatrix                                                                                                                                     |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://moneymatrix.com/](https://moneymatrix.com/)                                                                                            |
| Classification               | Aggregator                                                                                                                                      |
| Regions                      | `International`                                                                                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                 |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/> `WebRedirectWithdrawal`<br/> `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`<br/> `Capture` |
| PaymentIQ Configuration File | `MoneyMatrixConfig`                                                                                                                             |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.moneymatrix.MoneyMatrixConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <merchantName>??</merchantName>
        <supportedCurrencies>EUR</supportedCurrencies>
        <container>iframe</container>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.moneymatrix.MoneyMatrixConfig>
```

</details>

### Attributes

| Attribute  | Description             |
|------------|-------------------------|
| merchantId | Provided by MoneyMatrix |
| secretKey  | Provided by MoneyMatrix |

### IP Whitelisting
Please request that MoneyMatrix whitelist the following IPs:

[PaymentIQ IP addresses](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist)

### 3D Secure

3D Secure is configured on MoneyMatrix side and can't be controlled by PaymentIQ.

## Example Routing Rule
![](/img/providers/routing/moneymatrix.png)

## Test Information
### Hosted
For credit cards and banks, any valid card/account number can be used.

### Non-hosted
For all test credit cards below use any future Expired Date, and CVV 111 or 123.

To get 3DS use cards with expected 3DS "Success" status and amount >= 100.

To get N3DS use any card with amount < 100.

3D secure verification password for Visa card: 12345

3D secure verification password for Mastercard: 12343

| Card Number      | Enrolled | N3DS Status | 3DS Status                                                  |
|------------------|----------|-------------|-------------------------------------------------------------|
| 4012001036275556 | N/A      | Success     | Failed. VendorMessage = 'Directory server not available'    |
| 4012001038443335 | N        | Success     | Success                                                     |
| 4012001038488884 | U        | Success     | Failed. VendorMessage = 'Cardholder enrolment not verified’ |
| 4012001036298889 | Y        | Success     | Failed. VendorMessage = 'Data is inaccurate or missing'     |
| 5453010000070888 | N/A      | Success     | Failed. VendorMessage = 'Cardholder enrolment failed'       |
| 4715059999000437 | N/A      | Success     | Failed. VendorMessage = 'Invalid merchant account number'   |
| 5453010000070789 | Y        | Success     | Success                                                     |
| 4929483900003342 | Y        | Success     | Success                                                     |

