--- 
id: "royalpay" 
title: "RoyalPay"
hide_title: "true"
---
 
![](/img/providers/logos/royalpay.png)

# RoyalPay

## About
RoyalPay offers credit card deposits & withdrawals and voucher deposits.

| Provider Name                | RoyalPay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://royalpay.eu/](https://royalpay.eu/)                                    |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `RoyalPayVoucherDeposit`   |
| PaymentIQ Configuration File | `RoyalPayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.royalpay.RoyalPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>true</use3Dsecure>
        <merchantCode>??</merchantCode>
        <supportedCurrencies>RUB|EUR|USD|UAH</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <container>window</container><!--iframe is not supported-->
  <!--<width>600</width>
  <height>600</height>-->
  <liveServiceEndPoint>https://royalpay.eu/api</liveServiceEndPoint>
  <redirectUrl>${baseRedirectUrl}/api/royalpay/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseRedirectUrl}/api/royalpay/callback/${ptx.txRefId}</callbackUrl>
  <defaultDescriptor>??</defaultDescriptor> <!-- Set the descriptor which will be displayed on the cardholder's statement -->
</com.devcode.paymentiq.integration.royalpay.RoyalPayConfig>
```

</details>

### Attributes

| Attribute                        | Description                                                                                                                                                                                |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantCode                     | Provided by RoyalPay to uniquely identify the merchant in the `Auth` header                                                                                                                |
| secretKey                        | Provided by RoyalPay to create a signature                                                                                                                                                 |
| Supported Currencies             | RUB, EUR, USD                                                                                                                                                                              |
| forcePayment                     | Optional. Set this value to force a specific payment system                                                                                                                                |
| subAccount                       | Optional. This value will be sent as submerchant_id in the deposit request                                                                                                                 |
| liveTxTypeToPaymentSystemMapping | Mapping that dictates which payment system to use for each transaction type. Please see [custom payment system mapping](./royalpay#custom-payment-system-mapping) for further information. |

### Custom payment system mapping
The configuration tag `liveTxTypeToPaymentSystemMapping` has a default value that should work for most setups and should therefore not be altered.

Default: `deposit_N3DS->CardGateN3D,deposit_3DS->CardGate,withdrawal_UAH->CardUA,withdrawal_EUR->CardEU,withdrawal.*->Card,voucher->Voucher`

However there might be situations where you will have to change the payment system for e.g payouts. The default payment system for payouts is "Card", however currencies `UAH` and `EUR` have their own, "CardUA" and "CardEU" respectively. These are all known and is covered with the default mapping, but if it turns out that some other currency needs a specific payment system it can be configured.

Let's take `USD` as a theoretic example, and that it needs "CardUS" as payment system, then the new mapping would look like this:
`deposit_N3DS->CardGateN3D,deposit_3DS->CardGate,withdrawal_UAH->CardUA,withdrawal_EUR->CardEU,withdrawal_USD->CardUS,withdrawal.*->Card,voucher->Voucher`

Note the added `withdrawal_USD->CardUS`, and also note that all other currencies will default to "Card".

## Example Routing Rule
![](/img/providers/routing/royalpay01.png)
![](/img/providers/routing/royalpay02.png)

## Test Information

### Test Cards

| Card Brand | Card Number         |
|------------|---------------------|
| VISA       | 4111 1111 1111 1111 |

Any other card numbers will initiate an error

### Voucher

| Voucher Number     | Password | Result       |
|--------------------|----------|--------------|
| 360046146009394524 | 123456   | Success      |
| 360046146009399184 | Any      | Unavailable  |
| 360046146009400339 | Any      | User blocked |
