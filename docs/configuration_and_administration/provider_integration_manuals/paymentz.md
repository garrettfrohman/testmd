---
id: "paymentz"
title: "TransactWorld (via Paymentz)"
hide_title: "true"
---

![](/img/providers/logos/transactworld.png)

# TransactWorld (via Paymentz)

## About
TransactWorld (via Paymentz) is an aggregator payment provider offering credit card Sale (Auth + Capture as one transaction), Auth, Capture, Void, Withdrawal confirmation and reversal operations and several alternative payment methods:<br/>
- Banking: IMPS withdrawal
- Indian payment methods: UPI (Deposit and Withdrawal), NetBanking, RUPAY, WALLET

Please check at the bottom of this document or contact provider for more information which payment methods are supported.

| Provider Name                | Paymentz                                                                                                                                                                                                                  |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.transactworld.com/](https://www.transactworld.com/)                                                                                                                                                          |
| Classification               | Aggregator                                                                                                                                                                                                                |
| Regions                      | `International`                                                                                                                                                                                                           |
| Currencies                   | `INR`, `USD`, `EUR`, `NZD`, `CAD`, `JPY` and others (please check with Paymentz)                                                                                                                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund`<br/>`Capture`<br/>`Void`<br/>`WebRedirectDeposit`<br/>`PaymentzWebRedirectDeposit`<br/>`PaymentzBankWithdrawal`<br/>`PaymentzWalletWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `PaymentzConfig`                                                                                                                                                                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paymentz.PaymentzConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>false</testMode>
  <terminalMapping>??</terminalMapping>
  <paymentModeMapping>??</paymentModeMapping>
  <transferTypeMapping>??</transferTypeMapping>
  <accounts>
    <entry>
        <string>CARDS</string>
        <account>
            <username>??</username>
            <password>??</password>
            <merchantId>??</merchantId>
            <memberId>??</memberId>
            <secretKey>??</secretKey>
            <use3Dsecure>true</use3Dsecure>
            <useTokenId>true</useTokenId>
            <authType>AUTH_CAPTURE</authType>
            <withdrawalType>OCT</withdrawalType>
            <supportedCurrencies>USD|INR</supportedCurrencies>
            <terminal>xxxx</terminal>
            <!--<terminal>VISA_EUR->2656,MASTERCARD_EUR->2657</terminal>-->
            <version>v1</version>
        </account>
    </entry>
    <entry>
      <string>IMPS</string>
      <account>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <memberId>??</memberId>
        <secretKey>??</secretKey>
        <supportedCurrencies>INR</supportedCurrencies>
        <terminal>IMPS_INR->xxxx</terminal>
        <version>v1</version>
      </account>
    </entry>
    <entry>
      <string>INR</string>
      <account>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <memberId>??</memberId>
        <secretKey>??</secretKey>
        <supportedCurrencies>INR</supportedCurrencies>
        <terminal>RUPAY_INR->xxxx,UPI_INR->xxxx,WALLET_INR->xxxx</terminal>
        <version>v1</version>
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <txHistoryDelayHours>0</txHistoryDelayHours>
</com.devcode.paymentiq.integration.paymentz.PaymentzConfig>
```
</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username             | Corresponds to the `user name` value from Paymentz. It is the username to the merchant back office account and it is used in **AuhtToken** request                                                                                                                                                                                                                                                                                                                               |
| account.password             | Corresponds to the password to the merchant back office account.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| account.merchantId           | Corresponds to the `authentication.memberId` value from Paymentz used in the all requests.                                                                                                                                                                                                                                                                                                                                                                                       |
| account.memberId             | Corresponds to `partnerId` value from Paymentz. This is `partnerId` to the merchant back office account and it is used in the **AuhtToken** request.                                                                                                                                                                                                                                                                                                                             |
| account.secretKey            | Corresponds to `Secret Key` which  should be generated from merchant back office. It is used for both encryption and in **AuthToken** requests.                                                                                                                                                                                                                                                                                                                                  |
| account.serviceEndpoint      | Request URL, provided by Paymentz. This parameter must be added in case non default request URL should be used (default URL is: https://secure.paymentz.com/transactionServices/REST/v1/).                                                                                                                                                                                                                                                                                       |
| account.use3Dsecure          | It is used to enable 3DS deposit                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| account.useTokenId           | It is used to enable recurring                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| account.authType             | - AUTH_CAPTURE <br/> - AUTH_CAPTURE <br/> - FINAL_AUTH <br/> - PRE_AUTH <br/>                                                                                                                                                                                                                                                                                                                                                                                                    |
| account.withdrawalType       | It is used to enable OCT withdrawal, for which a prior successful deposit with the same PSP is required. In case this parameter is blank or missing, an independen withdrawal (for which no prior successful deposit is required) will be triggerd.                                                                                                                                                                                                                              |
| account.supportedCurrencies  | It is used to define supported currencies. `INR`, `USD`, `EUR`, `NZD`, `CAD`, `JPY` can be specified.                                                                                                                                                                                                                                                                                                                                                                            |
| account.terminal             | It is used to define terminal(s). Terminal defined at account level has higher priority than terminal defined using `terminalMapping` parameter and overrides terminal defined in `terminalMapping` parameter. Please check terminal definition examples below.                                                                                                                                                                                                                  |
| terminalMapping              | It is used to define terminal(s). Please check terminal definition examples below.                                                                                                                                                                                                                                                                                                                                                                                               |
| paymentModeMapping           | It is used to define payment mode mapping based on `service` parameter. Please always check with Paymentz which `paymentMode` should be used for your payment method and configure it in the **PaymentzConfig** (or ask PaymentIQ technical support to do so) if it isn't defined by default.<br/>By default the following mapping is defined:<br/>`NET_BANKING_INR->NBI,SEPBANKS_INR->NBI,BDBANKS_INR->NBI,IMPS_INR->NBI,NET_BANKING->NB,WALLET_INR->EWI,WALLET->EW,RUPAY->DC`. |
| transferTypeMapping          | It is used to define transfer type mapping based on `service` parameter. Please always check with Paymentz which `transferType` should be used for your payment method and configure it in the **PaymentzConfig** (or ask PaymentIQ technical support to do so) if it isn't defined by default.                                                                                                                                                                                  |
| sendCardHolderAsCustomerName | Set to true to send the input "card holder" as customer name. "card holder" will be splitted on the first space and use the first part as first name and the second part as last name                                                                                                                                                                                                                                                                                            |
| container                    | Indicates the way how the user will be redirected to the checkout URL (`window` is allowed only).                                                                                                                                                                                                                                                                                                                                                                                |
| velocityDaysBack             | It is used to define time interval for searching successfully made payments e.g. `[velocityDaysBack, currentDateTime - txHistoryDelayHours]`. Should be used for withdrawal only.                                                                                                                                                                                                                                                                                                |
| txHistoryDelayHours          | It is used to define time interval for searching successfully made payments e.g. `[velocityDaysBack, currentDateTime - txHistoryDelayHours]`. Should be used for withdrawal only.                                                                                                                                                                                                                                                                                                |

### Tokenized repeat or recurring payment
Merchants should have a PSP account with active tokenized payment. To activate tokenized payment, please check with the PSP.

After activating the tokenized payment on the PSP account, the merchant should activate the following flag in the **PaymentzConfig**.
```xml
<useTokenId>true</useTokenId>
```
This is to be able to use the tokenized payment later on. This flag will activate registering credit card details at Paymentz side.<br/>

In **PaymentzConfig**, the recurring or repeat payment tx should be routed to another PSP account that has the following tags:
```xml
<useTokenId>true</useTokenId>
<use3Dsecure>false</use3Dsecure>
```

### Terminal Mapping
There are two ways to specify terminal mapping:
1. as `terminalMapping` root parameter in the **PaymentzConfig** e.g. `<terminalMapping>RUPAY_INR->0000</terminalMapping>`;
2. as `terminal` account level parameter in the **PaymentzConfig** (see examples below).

#### Credit Cards

| Terminal mapping examples                                        | Description                                                                                                                      |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| `<terminal>{TERMINAL_ID}</terminal>`                             | Defines a generic terminal for all card types and currencies                                                                     |
| `<terminal>{CARD_TYPE}->{TERMINAL_ID},...</terminal>`            | Defines a specific terminals for a different card types e.g. `VISA->0000,MASTERCARD->1111`                                       |
| `<terminal>{CARD_TYPE}_{CURRENCY}->{TERMINAL_ID},...</terminal>` | Defines a specific terminals for a different card types and currencies e.g. `VISA_EUR->0011,VISA_USD->0022,MASTERCARD_EUR->0033` |
| -                                                                | `UNKNOWN` will be sent in case no terminal map is configured or it can't be resolved                                             |

#### APMs

| Terminal mapping examples                                                      | Description                                                                                                              |
|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `<terminal>{TERMINAL_ID}</terminal>`                                           | Defines a generic terminal for all payment methods and currencies                                                        |
| `<terminal>{SERVICE}_{CURRENCY}->{TERMINAL_ID},...</terminal>`                 | Defines a specific terminals for a different services and currencies e.g. `RUPAY_INR->0000,UPI_INR->1111,IMPS_INR->2222` |
| `<terminal>{SERVICE}_{PAYMENT_BRAND}_{CURRENCY}->{TERMINAL_ID},...</terminal>` | Defines a specific terminals for a different services, payment brands and currencies e.g. `IMPS_BDBANKS_INR->1111`       |
| -                                                                              | `UNKNOWN` will be sent in case no terminal map is configured or it can't be resolved                                     |

## Configure APMs in PaymentIQ Back Office

Please make sure Paymentz is enabled in PaymentIQ before it can be used. It can be done in the **MerchantConfig** by adding "Paymentz" to the `<psps>` section:
```xml
<psps>Paymentz|...</psps>
```

Before configuring any payment method, please make sure the following parameters are defined for account in your **PaymentzConfig**:
```xml
<version>v1</version>
<secretKey>??</secretKey>
<terminal>??</terminal> <!--clarify it with provider-->
```
Please note, you can use one account for one payment method (in such case you can define terminal like `<terminal>xxxx</terminal>`).<br/>Also, you can use one account for a group of payment methods e.g. for Indian payment methods (in such case you can define several terminals like `<terminal>RUPAY_IND->xxxx,UPI_IND->xxxx,WALLET_IND->xxxx</terminal>`).

### RUPAY/UPI/WALLET Deposit

RUPAY
- paymentMode=DC
- paymentBrand=RUPAY

UPI
- paymentMode=UPI
- paymentBrand=UPI

WALLET
- paymentMode=EW (EWI - for India)
- paymentBrand=

1). **MerchantConfig**: configure a specific service for `WEBREDIRECT` provider type:
```xml
<entry>
  <string>WEBREDIRECT</string>
  <string>RUPAY|UPI|WALLET|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `WEBREDIRECT_RUPAY` as a deposit payment option<br/>
3). Create/Update routing rule by specifying `WebRedirectDeposit` transaction type.

#### Notes
- Similar steps are valid for deposit methods: RUPAY, UPI, WALLET
- you can also use `PaymentzWebRedirectDeposit` transaction type instead of `WebRedirectDeposit`. In that case you will have a possibility to provide a `paymentBrand` parameter (configure it in the Cashier Payment Method-settings) and it will be used to be sent in the request to Paymentz. It might be useful as Paymentz can add new payment brands for new acquirers e.g. `EW`(`EWI`) and `NB`(`NBI`).

### IMPS Bank Withdrawal

IMPS
- paymentMode=NBI
- paymentBrand=BDBANKS
- transferType=IMPS

1). **MerchantConfig**: configure a specific service for `PAYMENTZBANK` provider type:
```xml
<entry>
  <string>PAYMENTZBANK</string>
  <string>IMPS|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `PAYMENTZBANK_IMPS` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `PaymentzBankWithdrawal` transaction type.

## Example Routing Rules

![](/img/providers/routing/paymentz.png)

## Test Information

### Test Cards (CreditcardDeposit)

| Brand | 3DS | Card number      | Cvv | Expiry Date     |
|-------|-----|------------------|-----|-----------------|
| VISA  | No  | 4000000000000051 | 745 | any future date |
| VISA  | Yes | 4000000000000002 | 237 | any future date |

### Test Cards (WebRedirectDeposit)

| Brand      | Card number      | Cvv | Expiry Date     |
|------------|------------------|-----|-----------------|
| VISA       | 4000000000000051 | 745 | any future date |
| MASTERCARD | 5101080000000009 | 123 | any future date |

### Test UPI ID

`8778567834@upi`, `abc234@abc`

### Additional information
Provider API: https://docs.paymentz.com/integration/asynchronous-workflow.php

### Supported Payment Methods

| Payment Type                  | Payment Method/PIQ service | Payment Mode | Payment Brand |
|-------------------------------|----------------------------|--------------|---------------|
| Credit Card Account           |                            |              |               |
|                               | VISA                       | CC           | VISA          |
|                               | MAESTRO                    | CC           | MAESTRO       |
|                               | JCB                        | CC           | JCB           |
|                               | DISC                       | CC           | DISC          |
|                               | DINER                      | CC           | DINER         |
|                               | Master Card                | CC           | MC            |
|                               | AMEX                       | CC           | AMEX          |
| Net Banking Account           |                            |              |               |
|                               | TRUSTLY                    | NB           | TRUSTLY       |
|                               | EPAY                       | NB           | EPAY          |
|                               | Ideal                      | NB           | IDEAL         |
|                               | Sofort                     | NB           | SOFORT        |
|                               | YANDEX                     | NB           | YANDEX        |
|                               | QIWI                       | NB           | QIWI          |
|                               | SKILL                      | NB           | SKRILL        |
|                               | NETELLER                   | NB           | NETELLER      |
|                               | ASTROPAY                   | NB           | ASTROPAY      |
|                               | MULTIBANCO                 | NB           | MULTIBANCO    |
|                               | GIROPAY                    | NB           | GIROPAY       |
|                               | NEOSURF                    | NB           | NEOSURF       |
|                               | InPay                      | NB           | INPAY         |
| UPI India Account             |                            |              |               |
|                               | UPI                        | UPI          | UPI           |
| Bank Transfer Account         |                            |              |               |
|                               | IMPS                       | NBI          | BDBANKS       |
| Wallet Account                |                            |              |               |
|                               | NETELLER                   | EW           | NETELLER      |
|                               | SKRILL                     | EW           | SKRILL        |
| Wallet India Account          |                            |              |               |
|                               | MOBIKWIK                   | EWI          |               |
|                               | JIOMONEY                   | EWI          |               |
|                               | FREECHARGE                 | EWI          |               |
| Mobile Banking Bangla Account |                            |              |               |
|                               | TAP                        | BDM          | TAP           |
|                               | UPAY                       | BDM          | UPAY          |
|                               | NAGAD                      | BDM          | NAGAD         |
