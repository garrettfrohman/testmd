--- 
id: "cubixpay"
title: "CubixPay"
hide_title: "true"
---

![](/img/providers/logos/cubixpay.png)

# CubixPay

## About
CubixPay is a credit card provider that allowos deposits and refunds.

| Provider Name                | CubixPay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://cubixpay.com/](https://cubixpay.com/)                                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | Check directly with the provider                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Refund`                                              |
| PaymentIQ Configuration File | `CubixPayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.cubixpay.CubixPayConfig>
   <enabled>true</enabled>
   <testMode>true</testMode>
   <useViqProxy>true</useViqProxy>
   <accounts>
    <entry>
     <string>default</string>
     <account>
       <apiKey>??</apiKey>
       <secretKey>??</secretKey>
       <supportedCurrencies>??|??|??</supportedCurrencies>
     </account>
    </entry>
   </accounts>
</com.devcode.paymentiq.integration.cubixpay.CubixPayConfig>
```

</details>

### Attributes

| Attribute           | Description                                       |
|---------------------|---------------------------------------------------|
| apiKey              | API Key provided by CubixPay                      |
| secretKey           | Secret Key provided by CubixPay                   |
| supportedCurrencies | Supported currencies separated by pipe characters |

### Callback configuration

You need to specify the callback URL, under "Merchants" -> "Edit" -> "IPN URL" section 
in your CubixPay merchant account.

Test callback Url : https://test-api.paymentiq.io/paymentiq/api/cubixpay/callback

Live callback Url : https://api.paymentiq.io/paymentiq/api/cubixpay/callback

  ![](/img/providers/cubixpay02.png)

## Example Routing Rule

  ![](/img/providers/routing/cubixpay.png)

## Test Information
To be able to test the CubixPay you need to contact CubixPay to create a merchant account.

Log in to the CubixPay test dashboard at https://testpanel.cubixpay.net

Under "Merchants", find your API Key and your Secret Key.

![](/img/providers/cubixpay01.png)

Add the API Key created in your CubixPay merchant account as `apiKey` in the config, and the Secret Key as `secretKey`.

### Test cards

| Description | Credit Card Number  | Brand      |
|-------------|---------------------|------------|
| APPROVED    | 4012888888881881    | VISA       |
| DECLINED    | 4242424242424242    | VISA       |
| NOTENROLLED | 4900000000000086    | VISA       |
| APPROVED    | 5500000000000004    | MASTERCARD |
| DECLINED    | 5200000000000007    | MASTERCARD |
| NOTENROLLED | 5200000000000080    | MASTERCARD |
| APPROVED    | 6799851000000032    | MAESTRO    |
| DECLINED    | 6759000000000018    | MAESTRO    |
| NOTENROLLED | 6799990100000000019 | MAESTRO    |

For each credit card number the expiry date
must be in the future, and cvv must be 3 digits.