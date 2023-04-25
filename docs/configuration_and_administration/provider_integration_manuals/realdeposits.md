--- 
id: "realdeposits" 
title: "Real Deposits"
hide_title: "true"
---
 
![](/img/providers/logos/realdeposits.png)

# Real Deposits

## About
Real Deposits is an aggregator and credit card provider that offers 3DS and N3DS deposit (sale), refund, withdrawal(payout) and status check.

| Provider Name                | Real Deposits                                                                                                                                     |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://realdeposits.com/](https://realdeposits.com/)                                                                                            |
| Classification               | Debit/Credit Card Processor                                                                                                                       |
| Regions                      | `International`                                                                                                                                   |
| Currencies                   | `EUR`, `DKK`, `CAD`                                                                                                                               |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Capture`<br/> `Void`<br/> `RealDepositsDeposit`<br/> `RealDepositsWithdrawal` |
| PaymentIQ Configuration File | `RealDepositsConfig`                                                                                                                              |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.realdeposits.RealDepositsConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId><!--merchant_id-->
        <secretKey>??</secretKey><!--merchant_secret-->
        <profileId>??</profileId><!--application_key-->
        <supportedCurrencies>EUR|DKK|CAD</supportedCurrencies>
        <version>1.3</version>
        <gatewayNo>??</gatewayNo>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.realdeposits.RealDepositsConfig>
```

</details>

### Attributes

| Attribute                | Description                                                                                                                                                                         |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.merchantId | Corresponds to the *merchant_id* from Real Deposits.                                                                                                                                |
| accountConfig.secretKey  | Corresponds to the *merchant_secret* from Real Deposits.                                                                                                                            |
| accountConfig.profileId  | Corresponds to the *application_key* from Real Deposits.                                                                                                                            |
| accountConfig.gatewayNo  | Corresponds to the *gateway* from Real Deposits.                                                                                                                                    |
| useTransactionLookup     | If we should us the tx status service to get status or get status from the notificiation. Default is false due to error on Real Deposits side. But we can enable it when its fixed. |
| accountConfig.version    | Use value "1.3" to use the latest API. "1.2" is the old API                                                                                                                         |

### APMs
APMs are initialized with TxTypes RealDepositsDeposit and RealDepositsWithdrawal. Each APM method gets an assigned gateway hash by RealDeposits. This value needs to be configured as `gatewayNo` on account level in RealDepositsConfig.

## Example Routing Rules
![](/img/providers/routing/realdeposits.png)

## Test Information

CVC = 568 to test a successful transaction.

CVC = 333 to test a 3DS transaction.

CVC = any other to test a failed transaction.

