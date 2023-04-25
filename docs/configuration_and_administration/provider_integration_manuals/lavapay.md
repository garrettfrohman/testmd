--- 
id: "lavapay" 
title: "LavaPay"
hide_title: "true"
---
 
![](/img/providers/logos/lavapay.png)

# LavaPay

## About
Lavapay is a card processor supporting Deposits and Withdrawals.

| Provider Name                | LavaPay                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.lavapay.com/en/index.html](https://www.lavapay.com/en/index.html)  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `LavaPayDeposit` <br/> `LavaPayWithdrawal`                                      |
| PaymentIQ Configuration File | `LavaPayConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.lavapay.LavaPayConfig>
  <enabled>true</enabled>
<accounts>
    <entry>
     <string></string>
     <account>
       <accountID>??</accountID>
       <merchantId>??</merchantId>
       <password>??</password>
        <serviceEndpoint>https://www.LavaPay.com/checkout/</serviceEndpoint>
        <redirectUrl>${baseRedirectUrl}/api/lavapay/deposit/redirect</redirectUrl>
         <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
     </account>
    </entry>
  </accounts>
  <sendPaymentUrl>https://api.lavapay.com/LavaPayAPI</sendPaymentUrl>
  <transferActionHeadre>https://api.lavapay.com/I_LavaPayAPI/TransferMoney</transferActionHeadre>
  <withdrawActionHeadre>https://api.lavapay.com/I_LavaPayAPI/Withdraw_To_Ecurrency</withdrawActionHeadre>
 <verifyCallbackUrl>https://www.lavapay.com/callback-verify.html?</verifyCallbackUrl> 
</com.devcode.paymentiq.integration.lavapay.LavaPayConfig>
```
</details>

### Attributes

| Attribute  | Description            |
|------------|------------------------|
| accountID  | Wallet Id              |
| merchantId | Merchant account email |
| password   | API access password    |

## Example Routing Rule
![](/img/providers/routing/lavapay.png)

## Test Information

