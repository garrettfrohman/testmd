--- 
id: "wallet88" 
title: "Wallet88"
hide_title: "true"
---
 
![](/img/providers/logos/wallet88.png)

# Wallet88

## About 
Wallet88 is a Wallet provider with support for Deposits and Withdrawals.

| Provider Name                | Wallet88                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.wallet88.com/](http://www.wallet88.com/)                            |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `Wallet88Deposit`<br/> `Wallet88Withdrawal`                                     |
| PaymentIQ Configuration File | `Wallet88Config`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.wallet88.Wallet88Config>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
          <customerId>??</customerId>     <!-- client_id -->
          <secretKey>??</secretKey>       <!-- client_secret -->
          <accountID>??</accountID>       <!-- merchant_control_id -->
          <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.wallet88.Wallet88Config>
```

</details>

### Attributes

| Attribute  | Description                                |
|------------|--------------------------------------------|
| customerId | client_id. Provided by Wallet88.           |
| secretKey> | client_secret. Provided by Wallet88.       |
| accountID> | merchant_control_id. Provided by Wallet88. |

## Example Routing Rule

![](/img/providers/routing/wallet88.png)

## Test Information

| Username           | Code   |
|--------------------|--------|
| miguel@systrix.com | 067474 |