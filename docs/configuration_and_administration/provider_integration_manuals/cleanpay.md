--- 
id: "cleanpay" 
title: "CleanPay"
hide_title: "true"
--- 


# CleanPay

## About
CleanPay is a credit/debit card payment processor offering 3DS deposits. Auth/capture/void and refunds are not supported.

| Provider Name                | CleanPay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://dev.cosmo.tech/](https://dev.cosmo.tech/)                              |
| Classification               | Debit/Credit Card Processsor                                                    |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                                                             |
| PaymentIQ Configuration File | `CleanPayConfig`                                                                |

## Configuration Information
<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.cleanpay.CleanPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <apiKey>??????</apiKey>
        <supportedCurrencies>???|???</supportedCurrencies>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.cleanpay.CleanPayConfig>
```

</details>

### Attributes


| Attribute | Description                  |
|-----------|------------------------------|
| apiKey    | API key provided by provider |

### 3DSecure
3DS is controlled on the provider side and can't be configured in PaymentIQ.

## Example Routing Rule
![](/img/providers/routing/cleanpay.png)

## Test Information

Please visit https://www.notion.so/innostream/Cosmonaut-Test-Cards-9f5448e4dd7d4abc9ac6d2617d859b80 for testing cards and other information
