--- 
id: "sofort" 
title: "Sofort"
hide_title: "true"
---
 
![](/img/providers/logos/sofort.png)

# Sofort

## About
Sofort is a banking provider with support for Deposits and Refunds.

| Provider Name                | Sofort                                                                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.sofort.com/](https://www.sofort.com/)                                                                                                                                                 |
| Classification               | Online Banking                                                                                                                                                                                     |
| Regions                      | `Austria`, `Belgium`, `Czech Republic*`, `Finland`, `France`, `Germany`, `Hungary*`, `Italy, Netherlands`, `Norway`, `Poland*`, `Slovakia`, `Spain`, `Sweden*`, `Switzerland*`, `United Kingdom**` |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                    |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `SofortDeposit`<br/> `Refund`                                                                                                                                                   |
| PaymentIQ Configuration File | `SofortConfig`                                                                                                                                                                                     |

\* A local recipient account is required for transactions in local currency

\** Prerequisite: local recipient account

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.sofort.SofortConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <secretKey>??</secretKey>
        <accountID>??</accountID>
        <projectId>??</projectId>
        <serviceEndpoint></serviceEndpoint>
        <redirectUrl>${baseRedirectUrl}/api/sofort/deposit/redirect?transId=${ptx.txRefId}</redirectUrl>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
  </accounts>
  <!-- <defaultDescriptor>${ptx.merchantUser.attributes.descriptor} ${ptx.txRefId}</defaultDescriptor> -->
  <defaultDescriptor>${ptx.merchantUser.attributes.descriptor} ${ptx.id}</defaultDescriptor>
  <notificationUrl>${baseCallbackUrl}/api/sofort/deposit/callback?transId=${ptx.txRefId}</notificationUrl>
</com.devcode.paymentiq.integration.sofort.SofortConfig>
```
</details>

### Attributes

| Attribute | Description        |
|-----------|--------------------|
| secretKey | Provided by Sofort |
| accountID | Provided by Sofort |
| projectId | Provided by Sofort |

## Example Routing Rule
![](/img/providers/routing/sofort.png)
## Test Information

- User country: DEU
- Currency: EUR
- (Mock User: EUR_SOFORT)

1. Begin a transaction in the cashier.
2. After being redirected to the Sofort payment, enter as sort code or BIC: 88888888 Country: Germany.
3. After that, follow the steps and freely add information.
