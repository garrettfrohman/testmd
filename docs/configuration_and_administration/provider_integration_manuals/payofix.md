--- 
id: "payofix" 
title: "Payofix"
hide_title: "true"
---
 
![](/img/providers/logos/payofix.png)

# Payofix

## About
Payofix offers credit card deposits (3DS and non-3DS) and refunds.

| Provider Name                | Payofix                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://payofix.com/](https://payofix.com/)                                    |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Refund`                                              |
| PaymentIQ Configuration File | `PayofixConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payofix.PayofixConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>false</testMode>

  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username>
        <apiKey>???</apiKey>
        <supportedCurrencies>XXX|YYY</supportedCurrencies>
      </account>
    </entry>
  </accounts>

</com.devcode.paymentiq.integration.payofix.PayofixConfig>
```
</details>

### Attributes

| Attribute                  | Description                                                                                                    |
|----------------------------|----------------------------------------------------------------------------------------------------------------|
| username                   | Provided by Payofix                                                                                            |
| apiKey                     | Provided by Payofix                                                                                            |
| useCountryIpFromVerifyUser | Set to true to override the ip lookup from the front end to use attribute send in verify user, (default false) |
| sendCountry                | Set to false to not send the country code to Payofix (default true)                                            |

### Note

3DSecure is controlled on Payofix' side and can't be configured in PaymentIQ.

### Use country IP from verify user
This feature is used to override the IP address from the FrontAPI/Cashier with an IP sent in the verifyuser response.

You can provide the verify user IP in an attribute named `countryip` in verifyuser. this name can also be overriden in `MerchantConfig` by adding `<countryIpAttributeName>countryip</countryIpAttributeName>`.

To enable using the verifyuser IP setting, you add `<useCountryIpFromVerifyUser>true</useCountryIpFromVerifyUser>` in the PayofixConfig either on the root level or on a specific account.

## Example Routing Rule

![](/img/providers/routing/payofix.png)

## Test Information

### Declined cards

| Card number      | Action                                                               |
|------------------|----------------------------------------------------------------------|
| 5555555555554444 | Declined transaction                                                 |
| 4444333322221111 | Pending transaction                                                  |
| 4242424242424242 | Pending transaction. Will be changed to Declined in about 10 minutes |

### Approved cards

Example: 

| Card number         | Action               |
|---------------------|----------------------|
| 4111 1111 1111 1111 | Approved transaction |

All other numbers will be approved.
