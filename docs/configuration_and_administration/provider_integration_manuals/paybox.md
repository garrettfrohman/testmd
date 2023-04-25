--- 
id: "paybox" 
title: "Paybox"
hide_title: "true"
---
 
![](/img/providers/logos/paybox.png)

# Paybox

## About
Paybox is a mobile payment platform supporting deposits.

| Provider Name                | Paybox                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.payboxtech.com/](https://www.payboxtech.com/)                      |
| Classification               | Mobile Payment                                                                  |
| Regions                      | `Austria`                                                                       |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `PayboxDeposit`                                                                 |
| PaymentIQ Configuration File | `PayboxConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paybox.PayboxConfig>
  <enabled>true</enabled>
  <mock>false</mock>
  <asyncCalls>false</asyncCalls>
  <lang>en</lang>
  <auth>
    <activeAuth>default</activeAuth>
    <authConfigs>
      <entry>
        <string>default</string>
        <com.devcode.paymentiq.integration.AuthConfig_-AuthSetting>
          <username>??</username>
          <mode>TEST</mode>
        </com.devcode.paymentiq.integration.AuthConfig_-AuthSetting>
      </entry>
    </authConfigs>
  </auth>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <accountID>??</accountID>
        <username>??</username>
        <password>??</password>
      </account>
    </entry>
  </accounts>
  <errorCodeToStatusCode>
    <entry>
      <string>0</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>SUCCESS</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>13</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_LIMIT_OVERDRAWN</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>42</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_INVALID_ACCOUNT_NUMBER</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
  </errorCodeToStatusCode>
</com.devcode.paymentiq.integration.paybox.PayboxConfig>
```

</details>

### Attributes

| Attribute | Description        |
|-----------|--------------------|
| accountID | Provided by Paybox |
| username  | Provided by Paybox |
| password> | Provided by Paybox |

## Example Routing Rule

![](/img/providers/routing/paybox.png)

## Test Information

Please contact the Provider directly.
