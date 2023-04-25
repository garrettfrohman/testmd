--- 
id: "fstech" 
title: "FSTech"
hide_title: "true"
--- 

![](/img/providers/logos/fstech.png)

# FSTech

## About
FSTech is a provider processing credit card payments, both as a hosted solution and as a direct server-to-server solution.

| Provider Name                | FSTech                                                                                                                                                                                           |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Links                        | [Site](https://www.elepayments.com/templates/fstech//about/overview/index.html)<br/>[API docs](https://test.elepayments.com/docs/v2/)<br/>[Portal](https://www.elepayments.com/portal/index.php) |
| Classification               | Debit/Credit Card Processor                                                                                                                                                                      |
| Regions                      | International                                                                                                                                                                                    |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`WebRedirectDeposit`<br/>`FSTechWithdrawal`<br/>`Refund`                                                                                                                 |
| PaymentIQ Configuration File | `FSTechConfig`                                                                                                                                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.fstech.FSTechConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>??</merchantId> <!-- MerchantId -->
        <terminalId>??</terminalId> <!-- TerminalId -->
        <password>??</password> <!-- ApiPassword -->
        <secretKey>??</secretKey> <!-- PrivateKey -->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
     </account>
    </entry>
    <entry>
     <string>hosted</string>
     <account>
        <merchantId>??</merchantId> <!-- MerchantId -->
        <terminalId>??</terminalId> <!-- TerminalId -->
        <password>??</password> <!-- ApiPassword -->
        <secretKey>??</secretKey> <!-- PrivateKey -->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <!-- <testServiceEndPoint>https://test.elepayments.com/</testServiceEndPoint> Possible to change the endpoint due to whitelabel -->
  <!-- <liveServiceEndPoint>https://gate.fstech.net/</liveServiceEndPoint> Possible to change the endpoint due to whitelabel -->
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.fstech.FSTechConfig>
```

</details>

### Attributes

| Attribute  | Description                                                                                             |
|------------|---------------------------------------------------------------------------------------------------------|
| merchantId | The `MerchantId` value. Used as identification in requests sent to gateway, provided by the gateway.    |
| terminalId | The `TerminalId` value. This is a unique ID number of each terminal(currency), provided by the gateway. |
| password   | The `ApiPassword` value. This is a unique password, provided by the gateway.                            |
| secretKey  | The `PrivateKey` value. This is a unique ID, provided by the gateway.                                   |

## Example Routing Rule

![](/img/providers/routing/fstech1.png)

## Transaction Flow

### server-to-server payment
The server-to-server payment solution is a regular credit card deposit using transaction type `CreditcardDeposit`, from either the PIQ standardized cashier or merchants own.

### Hosted payment
The hosted payment solution is when transaction type `WebRedirectDeposit` is used, which opens a redirect URL on FSTech's end where the end-user adds the card details and finishes the payment.

### Payouts
Payouts are done with transaction type `FSTechWithdrawal`. Since the payouts are referring to a previous deposit transaction, a previous successful deposit has to have been performed with the same user on that merchant account.

## Test Information

| Card number      | Expiry              | CVV |
|------------------|---------------------|-----|
| 4200000000000000 | Any (in the future) | Any |
| 5212345678901234 | Any (in the future) | Any |

Use different expiry months to simulate different outcomes of the test.

| Outcome   | Month |
|-----------|-------|
| Approved  | 01    |
| Declined  | 02    |
| 3D secure | 05    |
