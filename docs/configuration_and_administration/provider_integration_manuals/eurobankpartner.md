--- 
id: "eurobankpartner" 
title: "EuroBankPartner"
hide_title: "true"
---
 
![](/img/providers/logos/eurobankpartner.png)


# EuroBankPartner

## About
EuroBankPartner provides fast, low-cost, and innovative solutions for sending and receiving money.

| Provider Name                | EuroBankPartner                                                      |
|------------------------------|----------------------------------------------------------------------|
| Link                         | [https://eurobankpartner.com/](https://eurobankpartner.com/)         |
| Classification               | Online Banking                                                       |
| Regions                      | `International`                                                      |
| Currencies                   | `USD`, `EUR`                                                         |
| Methods/PaymentTxTypes       | `FixiPayBankWithdrawal` <br/> `BankIBANWithdrawal`  <br/> `Reversal` |
| PaymentIQ Configuration File | `FixiPayConfig`                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.fixipay.FixiPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <waitForNotification>false</waitForNotification>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <apiKey>???</apiKey>
        <apiToken>???</apiToken> <!--callback auth token-->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
        <merchantId>bambora test merchant</merchantId>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.fixipay.FixiPayConfig>

```

</details>

### Attributes

| Attribute           | Description                                                                                                                              |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId          | Merchant ID (Provided by EuroBankPartner).                                                                                               |
| apiKey              | apiKey (Provided by EuroBankPartner).                                                                                                    |
| apiToken            | apiToken (Provided by EuroBankPartner)                                                                                                   |
| waitForNotification | (false by default) Set true if want to receive success withdrawal status only after request is processed successfully on EuroBankPartner |

## Example Routing Rule

![](/img/providers/routing/eurobankpartner.png)

## Test Information

Testing could be done by entering any valid form bic or swift code  

Valid Swift code example:
BIINARBAXXX

Valid BIC example:
EMPOALTR
