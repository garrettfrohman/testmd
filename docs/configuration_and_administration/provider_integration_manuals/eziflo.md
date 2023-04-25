---
id: "eziflo"
title: "eziflo"
hide_title: "true"
---

![](/img/providers/logos/eziflo.png)

# eziflo

## About
eziflo is an aggregator provider supporting creditcard deposits, withdrawals (OCT), refunds, voids and captures.

eziflo also supports the following alternative payment methods (APMs):

### India
Deposit: Direct Banking (UPI, IMPS, GPAY, PHONEPE), Direct Wallet (PayTM), Bank Transfer

Withdrawal: Direct Banking (UPI, IMPS), Direct Wallet (PayTM)

### LATAM countries
Deposit: Bank Transfer and Cash

Withdrawal: Direct Bank Payout

### Canada
Deposit: Interac Online, Interac E-Transfer, Interac Direct Debit+, Bank Transfer

Withdrawal: Interac E-Transfer, VISA Direct, Direct Credit

| Provider Name                | eziflo                                                                                                                                                                                                                                                                                                |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | Not available                                                                                                                                                                                                                                                                                         |
| Classification               | Aggregator                                                                                                                                                                                                                                                                                            |
| Regions                      | `International`                                                                                                                                                                                                                                                                                       |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                       |
| Methods/PaymentTxTypes       | `CreditCardDeposit`<br/>`Void`<br/>`Capture`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`WebRedirectDeposit`<br/>`WebRedirectWithdrawal`<br/> `BankDeposit`<br/>`BankLatamDeposit`<br/>`CashLatamDeposit`<br/>`BankLocalWithdrawal`<br/>`BankDirectWithdrawal`<br/>`WalletWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `EzifloConfig`                                                                                                                                                                                                                                                                                        |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

# Credit cards configuration
```xml
<com.devcode.paymentiq.integration.eziflo.EzifloConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>CC</string>
      <account>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <authType>???</authType>
        <supportedCurrencies>???</supportedCurrencies>
        <container>window</container>
        <defaultDescriptor>???</defaultDescriptor>
      </account>
    </entry>
    <entry>
      <string>APM</string>
      <account>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <method>ETRANSFER</method><!--INTERAC|ETRANSFER|DIRECTDEBITPLUS|DIRECTCREDIT-->
        <!--<productCategory>gaming</productCategory>-->
        <supportedCurrencies>INR|CAD</supportedCurrencies>
        <container>window</container>
      </account>
    </entry>
    <entry>
      <string>APM_LATAM</string>
      <account>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <!--<method>??</method>-->
        <productCategory>gaming</productCategory>
        <supportedCurrencies>CLP|ARS|PEN|USD</supportedCurrencies>
        <container>window</container>
      </account>
    </entry>
    <entry>
      <string>PAYOUT</string>
      <account>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <!--<method></method>--><!--UPI|IMPS-->
        <!--<productCategory>gaming</productCategory>-->
        <supportedCurrencies>INR</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>OCT_PAYOUT</string>
      <account>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <useTokenId>true</useTokenId>
        <withdrawalType>OCT</withdrawalType>
        <!--<method>??</method>-->
        <!--<productCategory>gaming</productCategory>-->
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>iframe</container>
  <txHistoryDelayHours>0</txHistoryDelayHours>
  <defaultDescriptor>Product/Service name goes here</defaultDescriptor>
</com.devcode.paymentiq.integration.eziflo.EzifloConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                |
|---------------------|--------------------------------------------------------------------------------------------|
| apiKey              | Client's apiKey. Provided by eziflo                                                        |
| secretKey           | Client's secretKey. Provided by eziflo                                                     |
| authType            | Possible types: FINAL_AUTH, AUTH_CAPTURE, AUTH_AUTO_CAPTURE                                |
| supportedCurrencies | Supported currencies (`All`)                                                               |
| container           | Container type. `window` is supported for all payment methods.                             |
| defaultDescriptor   | Product/Service name. Mandatory                                                            |
| withdrawalType      | Type of withdrawal. Only OCT for credit cards                                              |
| useTokenId          | It is a PaymentIQ related setting to enable and use card tokenization. Should be `true`    |
| method              | It can be used to specify payment method e.g. `INTERAC`, `ETRANSFER`, `UPI`, ... Optional. |
| productCategory     | It is used to specify category e.g. `gaming`. Optional.                                    |

### Payment Method to Tx Type Mapping
| Payment Method                     | Type       | Service or Method                          | PaymentIQ Tx Type                    | Currencies         | Comments                                                                                                                                                                                                               |
|------------------------------------|------------|--------------------------------------------|--------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                    | Deposit    | -                                          | WebRedirectDeposit                   | INR                | Hosted Payment Page (HPP) with all available payment options.<br/>Payment method is not required.                                                                                                                      |
| UPI, PayTM, IMPS, GPAY and PHONEPE | Deposit    | UPI/PAYTM/IMPS/GPAY/PHONEPE                | WebRedirectDeposit                   | INR                | Specific INR payment method initiated via HPP (user will be redirected directly to the payment page).                                                                                                                  |
| Bank Transfer                      | Deposit    | BANKTRANSFER or BANK_TRANSFER              | WebRedirectDeposit                   | INR                | service/method=BANKTRANSFER/BANK_TRANSFER is required.                                                                                                                                                                 |
| Direct Bank Payout (UPI, IMPS)     | Withdrawal | UPI/IMPS                                   | BankLocalWithdrawal                  | INR                | Payment method can be specified in the config or can be provided with `BankLocalWithdrawalInput.service`.<br/>**ifscCode > input.clearingNumber**                                                                      |
| Direct Wallet Payout (PayTM)       | Withdrawal | PAYTM                                      | WalletWithdrawal                     | INR                | service/method=PAYTM is required.                                                                                                                                                                                      |
| LATAM Bank Transfer                | Deposit    | blank or BANKTRANSFER or BANK_TRANSFER     | BankLatamDeposit or BankDeposit      | CLP, PEN, USD      | Payment method should be provided via `input.service`.<br/>BankLatamDeposit tx type can be used without service parameter and it will be mapped to BANK_TRANSFER by default.<br/>`window` container is only supported. |
| LATAM Cash                         | Deposit    | blank or CASH                              | CashLatamDeposit                     | ARS, PEN, USD, CLP | `window` container is only supported                                                                                                                                                                                   |
| LATAM Direct Payout                | Withdrawal | DIRECTCREDIT                               | BankLocalWithdrawal                  | ARS, CLP, PEN, USD | Direct Payouts in Argentina, Chile, Ecuador, Peru. Service should be configured for `BankLocalWithdrawalInput`.<br/>**cciNumber > input.clearingNumber**                                                               |
| Interac Online                     | Deposit    | INTERAC                                    | InteracDeposit or WebRedirectDeposit | CAD                | Payment method can be configured either using `input.service` or `accountConfig.method`.<br/>`window` container is only supported.                                                                                     |
| Interac E-Transfer                 | Deposit    | ETRANSFER or INTERAC_ETRANSFER             | InteracDeposit or WebRedirectDeposit | CAD                |                                                                                                                                                                                                                        |
| Interac Direct Debit+              | Deposit    | DIRECTDEBITPLUS or INTERAC_DIRECTDEBITPLUS | InteracDeposit or WebRedirectDeposit | CAD                |                                                                                                                                                                                                                        |
| Bank Transfer                      | Deposit    | BANKTRANSFER or BANK_TRANSFER              | WebRedirectDeposit                   | CAD                |                                                                                                                                                                                                                        |
| VISA Direct Payout                 | Withdrawal | VISADIRECT                                 | CreditcardWithdrawal                 | CAD                | CC payout in Canada.                                                            |
| Direct Credit Payout               | Withdrawal | blank or DIRECTCREDIT                      | BankDirectWithdrawal                 | CAD                | Bank payout in Canada.<br/>`DIRECTCREDIT` service is used by default if no service is specified in the `input.service` or method configured in the `accountConfig.method`.                                             |

### Notification URL

Please configure a notification URL at provider's side:

```
TEST: https://test-api.paymentiq.io/paymentiq/api/eziflo/callback
PROD: https://api.paymentiq.io/paymentiq/api/eziflo/callback
```

### APM deposits: INTERAC, ETRANSFER/INTERAC_ETRANSFER, DIRECTDEBITPLUS/INTERAC_DIRECTDEBITPLUS, BANKTRANSFER/BANK_TRANSFER
- configure service using either `input.service` or `accountConfig.method`

### APM withdrawals: ETRANSFER, DIRECTCREDIT
- configure service using either `input.service` or `accountConfig.method`

## Example Routing Rule

### Credit Card
![](/img/providers/routing/eziflo_cc.png)

### Bank
![](/img/providers/routing/eziflo_bank.png)

### Wallet
![](/img/providers/routing/eziflo_wallet.png)

### Cash
![](/img/providers/routing/eziflo_cash.png)

### Canada
![](/img/providers/routing/eziflo_canada.png)

### WebRedirect (APM)
![](/img/providers/routing/eziflo_webredirect.png)

## Test Information

| Card Number      | Expiry Date | CVV | Result   | Comment                                                           |
|------------------|-------------|-----|----------|-------------------------------------------------------------------|
| 4000000000000002 | Any         | 123 | Success  | Authorize or purchase transaction is successfully created         |
| 5555555555554444 | Any         | 123 | Declined | Authorization failure                                             |
| 4008460000000000 | Any         | 123 | Declined | The card has expired                                              |
| 4716160000000009 | Any         | 123 | Declined | The payment has been declined because the card is reported stolen |
| 5531886652142950 | 01/2023     | 003 |          | Direct Visa Payout (CAD)                                          |
