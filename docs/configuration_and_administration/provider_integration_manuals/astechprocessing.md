--- 
id: "AstechProcessing" 
title: "AsTech Processing"
hide_title: "true"
---
 
![](/img/providers/logos/astech.png)

# AsTech Processing

## About
ASTech is a credit card provider that offers only deposits. Refunds and payouts can be done from ASTech backoffice. ASTech is a provider that is popular for Binary Forex customers.

| Provider Name                | AsTech Processing                                                               |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.astechprocessing.com/](http://www.astechprocessing.com/)            |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                                                             |
| PaymentIQ Configuration File | `AsTechConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.astech.ASTechConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <password>??</password>
        <secretKey>??</secretKey>
        <brandId>??</brandId>
        <storeId>??</storeId>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.astech.ASTechConfig>
```
</details>

| Attribute  | Description                                                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId | Provided by ASTech (One merchant id for each merchant)                                                                                   |
| password   | An API password for the server to server integration                                                                                     |
| secretKey  | Used for checking against fraud (md5 checks). This key is selected by the merchant.                                                      |
| brandId    | A brand is N3DS or 3DS and also for different currencies.  Ex: Our test brand T3504T_Test is for both N3DS and 3DS for the currency USD. |
| storeId    | A merchant can have multiple stores. Each store has redirect url, notification url that is used when doing 3DS transactions.             |

### ASTech backoffice

Refunds can be done from the transaction history report.
REPORTS > TRANSACTION HISTORY
By clicking the money icon to the right.

![](/img/providers/astechrefund.png)

To change info for the store go to.

OTHER > STORES 

Here you can change the url for return and notification.

![](/img/providers/astechinfo.png)

### Notification URLs:
Test: https://test.paymentiq.biz/paymentiq/api/astech/deposit/callback

Live: https://api.paymentiq.biz/paymentiq/api/astech/deposit/callback

### Return URLs:
Test: https://test.paymentiq.biz/paymentiq/api/astech/deposit/redirect

Live: https://api.paymentiq.biz/paymentiq/api/astech/deposit/redirect

## Example Routing Rule
![](/img/providers/routing/astech.png)

## Test Information

- Currency: USD

### N3DS (amount 1-99)

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4006111122223333 | 555 | Any         |

### 3DS (amount < 100)

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4000000000000002 | 555 | Any         |