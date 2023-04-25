--- 
id: "globepay" 
title: "Globepay"
hide_title: "true"
---
 
![](/img/providers/logos/globepay.png)

# Globepay

## About
Globepay is a wallet solution supporting Deposits and Withdrawals.

| Provider Name                | Globepay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.globepayinc.com/](https://www.globepayinc.com/)                    |
| Classification               | MWallet                                                                         |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `GlobepayDeposit` <br/> `GlobepayWithdrawal`                                    |
| PaymentIQ Configuration File | `GlobepayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.globepay.GlobepayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|EUR|GBP|INR</supportedCurrencies>
        <email>??</email>
      </account>
    </entry>
  </accounts>
  <container>window</container>
</com.devcode.paymentiq.integration.globepay.GlobepayConfig>
```
</details>

### Attributes

| PaymentIQ Configuration | Description                       |
|-------------------------|-----------------------------------|
| secretKey               | Secret Key. Provided by Globepay. |
| email                   | Email                             |

## Example Routing Rule
![](/img/providers/routing/globepay.png)

## Test Information

- Use as low amount as possible but amounts lower than 1 INR are not accepted.

| Email                   | Password    | Masterkey |
|-------------------------|-------------|-----------|
| testing@globepayinc.com | Testing1234 | 2010      |