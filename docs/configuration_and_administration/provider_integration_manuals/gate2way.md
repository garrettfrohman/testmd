---
id: "gate2way"
title: "gate2way"
hide_title: "true"
---

![](/img/providers/logos/gate2way.png)

# gate2way

## About
gate2way is an aggregator provider supporting creditcard deposits, withdrawals (OCT), refunds, voids and captures. Withdrawal reversal is also supported.<br/>
gate2way also supports the following alternative payment methods (APMs):

### Europe
Deposit: Paysafecard, Skrill, Neteller, Giropay, Sofort

### India
Deposit: Direct Banking (UPI, IMPS, GPAY, PHONEPE), Direct Wallet (PayTM), Bank Transfer<br/>
Withdrawal: Direct Banking (UPI, IMPS), Direct Wallet (PayTM)

### LATAM countries
Deposit: Bank Transfer and Cash<br/>
Withdrawal: Direct Bank Payout

### Canada
Deposit: Interac Online, Interac E-Transfer, Interac Direct Debit+, Bank Transfer<br/>
Withdrawal: Interac E-Transfer, VISA Direct, Direct Credit

### Japan
Deposit: TigerPay Wallet<br/>
Withdrawal: TigerPay Wallet

| Provider Name                | Gate2Way                                                                                                                                                                                                                                                                                              |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://gate2way.com/](https://gate2way.com/)                                                                                                                                                                                                                                                        |
| Classification               | Aggregator                                                                                                                                                                                                                                                                                            |
| Regions                      | `International`                                                                                                                                                                                                                                                                                       |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                       |
| Methods/PaymentTxTypes       | `CreditCardDeposit`<br/>`Void`<br/>`Capture`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`WebRedirectDeposit`<br/>`WebRedirectWithdrawal`<br/> `BankDeposit`<br/>`BankLatamDeposit`<br/>`CashLatamDeposit`<br/>`BankLocalWithdrawal`<br/>`BankDirectWithdrawal`<br/>`WalletWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `Gate2WayConfig`                                                                                                                                                                                                                                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

# Credit cards configuration
```xml
<com.devcode.paymentiq.integration.gate2way.Gate2WayConfig>
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
</com.devcode.paymentiq.integration.gate2way.Gate2WayConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                |
|---------------------|--------------------------------------------------------------------------------------------|
| apiKey              | Client's apiKey. Provided by gate2way                                                      |
| secretKey           | Client's secretKey. Provided by gate2way                                                   |
| authType            | Possible types: FINAL_AUTH, AUTH_CAPTURE, AUTH_AUTO_CAPTURE                                |
| supportedCurrencies | Supported currencies (`All`)                                                               |
| container           | Container type. `window` is supported for all payment methods.                             |
| defaultDescriptor   | Product/Service name. Mandatory                                                            |
| withdrawalType      | Type of withdrawal. Only OCT for credit cards                                              |
| useTokenId          | It is a PaymentIQ related setting to enable and use card tokenization. Should be `true`    |
| method              | It can be used to specify payment method e.g. `INTERAC`, `ETRANSFER`, `UPI`, ... Optional. |
| productCategory     | It is used to specify category e.g. `gaming`. Optional.                                    |

## Example Routing Rule

### Credit Card
![](/img/providers/routing/gate2way_cc.png)

### Bank
![](/img/providers/routing/gate2way_bank.png)

### Wallet
![](/img/providers/routing/gate2way_wallet.png)

### Cash
![](/img/providers/routing/gate2way_cash.png)

### Canada
![](/img/providers/routing/gate2way_canada.png)

### WebRedirect (APM)
![](/img/providers/routing/gate2way_webredirect.png)

Paysafecard, Skrill, Neteller, Giropay, Sofort

## Payment Method to Tx Type Mapping

| Payment Method                     | Type       | Service or Method                          | PaymentIQ Tx Type                    | Currencies                | Comments                                                                                                                                                                                                               |
|------------------------------------|------------|--------------------------------------------|--------------------------------------|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Europe APM                         | Deposit    | PAYSAFECARD/SKRILL/NETELLER/GIROPAY/SOFORT | WebRedirectDeposit or BankDeposit    | EUR                       | Countries: All European Countries                                                                                                                                                                                      |
|                                    | Deposit    | -                                          | WebRedirectDeposit                   | INR                       | Hosted Payment Page (HPP) with all available payment options.<br/>Payment method is not required.                                                                                                                      |
| UPI, PayTM, IMPS, GPAY and PHONEPE | Deposit    | UPI/PAYTM/IMPS/GPAY/PHONEPE                | WebRedirectDeposit                   | INR                       | Specific INR payment method initiated via HPP (user will be redirected directly to the payment page).                                                                                                                  |
| Bank Transfer                      | Deposit    | BANKTRANSFER or BANK_TRANSFER              | WebRedirectDeposit                   | INR                       | service/method=BANKTRANSFER/BANK_TRANSFER is required.                                                                                                                                                                 |
| Direct Bank Payout (UPI, IMPS)     | Withdrawal | UPI/IMPS                                   | BankLocalWithdrawal                  | INR                       | Payment method can be specified in the config or can be provided with `BankLocalWithdrawalInput.service`.<br/>**ifscCode > input.clearingNumber**                                                                      |
| Direct Wallet Payout (PayTM)       | Withdrawal | PAYTM                                      | WalletWithdrawal                     | INR                       | service/method=PAYTM is required.                                                                                                                                                                                      |
| LATAM Bank Transfer                | Deposit    | blank or BANKTRANSFER or BANK_TRANSFER     | BankLatamDeposit or BankDeposit      | All LATAM currencies, USD | Payment method should be provided via `input.service`.<br/>BankLatamDeposit tx type can be used without service parameter and it will be mapped to BANK_TRANSFER by default.<br/>`window` container is only supported. |
| LATAM Cash                         | Deposit    | blank or CASH                              | CashLatamDeposit                     | All LATAM currencies, USD | `window` container is only supported                                                                                                                                                                                   |
| LATAM Direct Payout                | Withdrawal | DIRECTCREDIT                               | BankLocalWithdrawal                  | All LATAM currencies, USD | Direct Payouts in Argentina, Chile, Ecuador, Peru. Service should be configured for `BankLocalWithdrawalInput`.<br/>**cciNumber > input.clearingNumber**                                                               |
| Interac Online                     | Deposit    | INTERAC                                    | InteracDeposit or WebRedirectDeposit | CAD                       | Payment method can be configured either using `input.service` or `accountConfig.method`.<br/>`window` container is only supported.                                                                                     |
| Interac E-Transfer                 | Deposit    | ETRANSFER or INTERAC_ETRANSFER             | InteracDeposit or WebRedirectDeposit | CAD                       |                                                                                                                                                                                                                        |
| Interac Direct Debit+              | Deposit    | DIRECTDEBITPLUS or INTERAC_DIRECTDEBITPLUS | InteracDeposit or WebRedirectDeposit | CAD                       |                                                                                                                                                                                                                        |
| Bank Transfer                      | Deposit    | BANKTRANSFER or BANK_TRANSFER              | WebRedirectDeposit                   | CAD                       |                                                                                                                                                                                                                        |
| VISA Direct Payout                 | Withdrawal | VISADIRECT                                 | CreditcardWithdrawal                 | CAD                       | CC payout in Canada.        |
| Direct Credit Payout               | Withdrawal | blank or DIRECTCREDIT                      | BankDirectWithdrawal                 | CAD                       | Bank payout in Canada.<br/>`DIRECTCREDIT` service is used by default if no service is specified in the `input.service` or method configured in the `accountConfig.method`.                                             |
| TigerPay (Japan e-wallet)          | Deposit    | TIGERPAY                                   | WebRedirectDeposit                   | USD, JPY                  | Payment method can be configured either using `input.service` or `accountConfig.method`.<br/>`window` container is only supported.                                                                                     |
| TigerPay (Japan e-wallet)          | Withdrawal | TIGERPAY                                   | WalletWithdrawal                     | USD, JPY                  | Only "walletNumber" should be provided by the user.                                                                                                                                                                    |

## Configuration

### Notification URL

Please configure a notification URL at provider's side:

```
TEST: https://test-api.paymentiq.io/paymentiq/api/gate2way/callback
PROD: https://api.paymentiq.io/paymentiq/api/gate2way/callback
```

### APM deposits: INTERAC, ETRANSFER/INTERAC_ETRANSFER, DIRECTDEBITPLUS/INTERAC_DIRECTDEBITPLUS, BANKTRANSFER/BANK_TRANSFER
- configure service using either `input.service` or `accountConfig.method`

### APM withdrawals: ETRANSFER, DIRECTCREDIT
- configure service using either `input.service` or `accountConfig.method`
- create routing rule
- add **gate2way-withdrawal-email** email template

### Direct Visa Payout
- **MerchantConfig:** configure `VISADIRECT` for `CREDITCARD` provider type
- **Rules > Payment Methods:** enable `CREDITCARD-VISADIRECT` withdrawal payment method
- **Routing Rule:** add withdrawal routing rule by specifying `CreditcardWithdrawal` tx type
- Add Visa Direct related icon

### Direct Bank Payout: UPI, IMPS
- **MerchantConfig:** configure `UPI`/`IMPS` for `BANKLOCAL` provider type
- **Rules > Payment Methods:** enable `BANKLOCAL-UPI`/`BANKLOCAL-IMPS` withdrawal payment method
- **Routing Rule:** add withdrawal routing rule by specifying `BankLocalWithdrawal` tx type

### Direct Wallet Payout: PAYTM

#### WalletWithdrawal
- **MerchantConfig:** configure `PAYTM` for `WALLET` provider type
- **Rules > Payment Methods:** enable `WALLET-PAYTM` withdrawal payment method
- **Routing Rule:** add withdrawal routing rule by specifying `WalletWithdrawal` tx type
- Add "wallet" icon
- Add translations

| Key                           | Text                       |
|-------------------------------|----------------------------|
| wallet.service.invalid        | Invalid Service            |
| wallet.walletAccount.required | Wallet Account is Required |
| wallet.walletAccount.invalid  | Wallet Account is Invalid  |
| wallet.walletName.required    | Wallet Name is Required    |
| wallet.main.walletAccount     | Wallet Account             |
| wallet.main.walletName        | Wallet Name                |

### LATAM Bank Transfer (Deposit)
- **MerchantConfig:** configure `BANK_TRANSFER` for `BANKLATAM` provider type
- **Rules > Payment Methods:** enable `BANKLATAM-BANK_TRANSFER` deposit payment method
- **Routing Rule:** add deposit routing rule by specifying `BankLatamDeposit` tx type
- Add **gate2way-latam-documenttype-template** HTML template
- Add translations

| Key                      | Text                 |
|--------------------------|----------------------|
| bank.main.nationalIdType | National ID Type     |
| gate2way.select_doc_type | Select Document Type |

### LATAM Cash Deposit
- **Rules > Payment Methods:** enable `CASHLATAM` deposit payment method
- **Routing Rule:** add deposit routing rule by specifying `CashLatamDeposit` tx type
- Add **gate2way-latam-documenttype-template** HTML template
- Add cash related icon
- Add translations

| Key                     | Text                         |
|-------------------------|------------------------------|
| nationalId.required     | National ID is required      |
| nationalIdType.required | National ID Type is required |

### LATAM Direct Payout: DIRECTCREDIT
**Note:** `DIRECTCREDIT` payment method should be provided via `input.service`.
- **MerchantConfig:** configure `DIRECTCREDIT` for `BANKLOCAL` provider type
- **Rules > Payment Methods:** enable `BANKLOCAL-DIRECTCREDIT` deposit payment method
- **Routing Rule:** add withdrawal routing rule by specifying `BankLocalWithdrawal` tx type
- Add **gate2way-latam-inputs-template** HTML template
- Add icon
- Add translations

| Key                               | Text                         |
|-----------------------------------|------------------------------|
| banklocal.nationalidtype.required | National ID Type is required |
| gate2way.select_acc_type          | Select Account Type          |
| gate2way.select_doc_type          | Select Document Type         |

### Interac Online/Interac E-Transfer/Interac Direct Debit+
- **MerchantConfig:** configure a specific service (`INTERAC`/`INTERAC_ETRANSFER`/`INTERAC_DIRECTDEBITPLUS`) for `INTERAC` provider type
- **Rules > Payment Methods:** enable specific deposit payment method: `INTERAC-INTERAC_ETRANSFER`
- **Routing Rule:** add deposit routing rule by specifying `InteracDeposit` tx type

### Direct Credit Payout (Bank Payout in Canada)
**Note:** currently only one service/method is allowed - `DIRECTCREDIT`, and it will be used by default if none is specified in the config or in the payment request. If non-default service will be needed, it can be configured in the config using `accountConfig.method` or via `input.service`.
- **Rules > Payment Methods:** enable `BANKDIRECT` withdrawal payment method
- **Routing Rule:** add withdrawal routing rule by specifying `BankDirectWithdrawal` tx type
- Add icon
- Add translations (if missing)

| Key                                  | Text                                     |
|--------------------------------------|------------------------------------------|
| transitNumber.required               | Transit Number is Required               |
| transitNumber.invalid                | Transit Number is Invalid                |
| financialInstitutionNumber.required  | Financial Institution Number is Required |
| financialInstitutionNumber.invalid   | Financial Institution Number is Invalid  |
| bank.main.financialinstitutionnumber | Financial Institution Number             |
| bank.main.transitnumber              | Transit Number                           |

### TigerPay Wallet Deposit
- **MerchantConfig:** configure a specific service (`TIGERPAY`) for `WEBREDIRECT` provider type
- **Rules > Payment Methods:** enable specific deposit payment method: `WEBREDIRECT-TIGERPAY`
- **Routing Rule:** add deposit routing rule by specifying `WebRedirectDeposit` tx type

### TigerPay Wallet Withdrawal
- **MerchantConfig:** configure a specific service (`TIGERPAY`) for `WALLET` provider type
- **Rules > Payment Methods:** enable `WALLET-TIGERPAY` withdrawal payment method
- **Routing Rule:** add withdrawal routing rule by specifying `WalletWithdrawal` tx type

## Additional Notes and Information
A common issue that may occur is the "Account Reference size must be between 4 and 32" error. <br/>
This refers to Gate2Way's `Customer.AccountReference` parameter, which is taken from the `userId` sent in the verifyUser. <br/>
As the parameter's value needs to be between 4-32 characters, please check that the userId sent is at least 4 characters and equal to or less than 32 characters. <br/>

Provider API: https://portal.gate2way.com/

## Test Information

| Card Number      | Expiry Date | CVV | Result   | Comment                                                           |
|------------------|-------------|-----|----------|-------------------------------------------------------------------|
| 4000000000000002 | Any         | 123 | Success  | Authorize or purchase transaction is successfully created         |
| 5555555555554444 | Any         | 123 | Declined | Authorization failure                                             |
| 4008460000000000 | Any         | 123 | Declined | The card has expired                                              |
| 4716160000000009 | Any         | 123 | Declined | The payment has been declined because the card is reported stolen |
| 5531886652142950 | 01/2023     | 003 |          | Direct Visa Payout (CAD)                                          |
