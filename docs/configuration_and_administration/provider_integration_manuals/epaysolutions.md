--- 
id: "epaysolutions" 
title: "EPaySolutions"
hide_title: "true"
---
 
![](/img/providers/logos/epaysolutions.png)

# EPaySolutions

## About
E-PaySolution is a credit card processor that has support for N3DS and refunds.

| Provider Name                | EPaySolutions                                                                   |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.e-paysolution.com/](http://www.e-paysolution.com/)                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`                                               |
| PaymentIQ Configuration File | `EPaySolutionsConfig`                                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
 <com.devcode.paymentiq.integration.epaysolution.EPaySolutionConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS_NEWBE</string>
      <account>
        <use3Dsecure>false</use3Dsecure>
        <merchantId>******</merchantId> <!-- MID -->
        <gatewayNo>8001</gatewayNo> <!-- Gateway -->
        <secretKey>??</secretKey> <!-- Key -->
        <refundReason>*</refundReason> <!-- Reason code for refunds. See e-paysolution docs for list of codes -->
      </account>
    </entry>
    <entry>
      <string>N3DS_VIP</string>
      <account>
        <use3Dsecure>false</use3Dsecure>
        <merchantId>******</merchantId> <!-- MID -->
        <gatewayNo>8002</gatewayNo> <!-- Gateway -->
        <secretKey>??</secretKey> <!-- Key -->
        <refundReason>*</refundReason> <!-- Reason code for refunds. See e-paysolution docs for list of codes -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.epaysolution.EPaySolutionConfig>
```

</details>

### Attributes

| Attribute    | Description                                                                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId   | Provided by EPaySolutions                                                                                                                            |
| gatewayNo    | There are two different configs needed depending on what gateway that should be used. The gateways that can a be used are 8001(newbe) and 8002(VIP). |
| secretKey    | Provided by EPaySolutions                                                                                                                            |
| refundReason | Reason code for refunds. See list below.                                                                                                             |

### Refund Reason Codes

Note that it is not possible to route refunds to a different account config than the one used in the deposit. Transaction specific refund reason code is currently not implemented. For this reason it is recommended to alwasy use '8' (Other).

![](/img/providers/epaysolutions01.png)

## Example Routing Rule
![](/img/providers/routing/epaysolution.png)

## Test Information

### Test Cards
Any valid Visa or MasterCard credit card number can be used in test.
