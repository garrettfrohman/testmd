--- 
id: "piastrix" 
title: "Piastrix"
hide_title: "true"
---
 
![](/img/providers/logos/piastrix.png)

# Piastrix

## About
Piastrix is e-wallet solution for money transfer over the world. Piastrix’s wallet has several levels of money and data loss protection. Replenish can be done in more than 50 ways: e-currency, bank transfers, cards etc.

## Links
| Provider Name                | Piastrix                                                             |
|------------------------------|----------------------------------------------------------------------|
| Link                         | [https://piastrix.com/en/individs](https://piastrix.com/en/individs) |
| Classification               | E-wallet                                                             |
| Regions                      | International                                                        |
| Currencies                   | `EUR` , `USD` , `RUB` , `UAH`                                        |
| Methods/PaymentTxTypes       | `PiastrixWalletDeposit`, `PiastrixWalletWithdrawal`                  |
| PaymentIQ Configuration File | `PiastrixConfig`                                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.piastrix.PiastrixConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <siteId>3***</siteId>
        <secretKey>T2*******6Q</secretKey>
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <useSystemTimeAsTxRefId>true</useSystemTimeAsTxRefId>
  <container>window</container>
</com.devcode.paymentiq.integration.piastrix.PiastrixConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Can be set at        | Required | Description                                                                                |
|-------------------------|----------------------|----------|--------------------------------------------------------------------------------------------|
| siteId                  | Config account level | Required | Shop id in Piastrix system                                                                 |
| secretKey               | Config account level | Required | Secret key from Shop security settings                                                     |
| container               | Config root level    | Required | Type of container to handle redirect. Recommended value `window` for full pay ways support |

### Notes

- Before start working with Piastrix service, merchants should have an active registered account [https://wallet.piastrix.com/auth/register](https://wallet.piastrix.com/auth/register) and active shop [https://wallet.piastrix.com/en/shops/create](https://wallet.piastrix.com/en/shops/create) , on behalf of which requests will be sent.
- Each shop has its own balance in each currency and it's not connected with the balance of personal wallet.
- Important! Success URL, Fail URL, Notification URL, Reject notification URL specified in the Shop settings have priority over the ones sent in the request, so for correct handling in PaymentIQ merchants need to remove them from the Shop settings.

## Example Routing Rule
![](/img/providers/routing/piastrix.png)

## Flow
Deposits performed using Piastrix Pay with various options of pay ways.

Pay ways as well as fees for each option can be configured in shop settings under Payment Methods section.

![](/img/providers/piastrix_pm.png)


## Test Information

Piastrix doesn't have any sandbox environment all the transactions has to go through their production environment.

