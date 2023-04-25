--- 
id: "billspay" 
title: "Billspay"
hide_title: "true"
---
 
![](/img/providers/logos/billspay.png)

# Billspay

## About
Billspay offers credit card deposits and bank withdrawals in USD.

| Provider Name                | Billspay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | Not available                                                                   |
| Classification               | CreditCard / Bank                                                               |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditCardDeposit`<br/> `BankIBANWithdrawal`<br/> `BankLocalWithdrawal`        |
| PaymentIQ Configuration File | `BillspayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.billspay.BillspayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>n3ds</string>
      <account>
        <siteId>??</siteId>
        <password>??????</password>
        <use3Dsecure>false</use3Dsecure>
        <supportedCurrencies>USD</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>3ds</string>
      <account>
        <key1>?????</key1>
        <apiSalt>?????</apiSalt>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>USD</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>payout</string>
      <account>
        <apiKey>??????</apiKey>
        <secretKey>??????</secretKey>
        <supportedCurrencies>USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.billspay.BillspayConfig>
```

</details>

### Attributes
| Attribute           | Description                                              |
|---------------------|----------------------------------------------------------|
| siteId              | Used for deposits. Provided by Billspay. "SID"           |
| password            | Used for deposits. Provided by Billspay. "r-code"        |
| key1                | Used for 3DS. Provided by Billspay. "keycode"            |
| apiSalt             | Used for 3DS. Provided by Billspay. "salt"               |
| secretKey           | Used for withdrawals. Provided by Billspay. "api secret" |
| apiKey              | Used for withdrawals. Provided by Billspay. "api key"    |
| supportedCurrencies | USD is the only supported currency ATM                   |

### Provider Configuration

:::danger IMPORTANT!

Billspay returns card number in clear text in their responses by default. It should be taken care of by VaultIQ but to be on the safe side please always notify Billspay to not include sensitive data in responses. It has to be turned on for each merchant on Billspay side (each SID).

:::

### ZedPayments
To send the 3DS requests directly to ZedPayments add the following to the top level of BillspayConfig:
```
<deposit3dsUrl>https://api.zedpayments.com/Service.svc/rest/v2/create</deposit3dsUrl>
```

## Example Routing Rules
![](/img/providers/routing/billspay-dp.png)
![](/img/providers/routing/billspay-wd.png)

## Test Information
Any valid Visa or MasterCard can be used when testing non-3DS credit card deposits.

Any valid IBAN and BIC can be used when testing bank IBAN withdrawals.

### 3DS
| Card             | Expiry  | CVV |
|------------------|---------|-----|
| 4000000000003220 | 2022-02 | 123 |

