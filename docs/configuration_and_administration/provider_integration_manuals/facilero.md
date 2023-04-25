---
id: "facilero"
title: "Facilero"
hide_title: "true"
---

![](/img/providers/logos/facilero.png)

# Facilero

## About
Facilero is an aggregator payment provider offering credit card Sale (Auth + Capture as one transaction), Auth, Capture, Void, Withdrawal confirmation and reversal operations and several alternative payment methods:<br/>
- Flexepin Voucher: deposit and withdrawal
- TigerPay Wallet: deposit and withdrawal
- TigerGate Banking: deposit and withdrawal
- Indian payment methods: UPI (Deposit and Withdrawal), NetBanking, RUPAY, WALLET

Please check with the provider for more details.

| Provider Name                | Facilero                                                                                                                                                                                                                  |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://facilero.com/](https://facilero.com/)                                                                                                                                                                            |
| Classification               | Aggregator                                                                                                                                                                                                                |
| Regions                      | `International`                                                                                                                                                                                                           |
| Currencies                   | `INR`, `USD`, `EUR`, `NZD`, `CAD`, `JPY` and others (please check with Fqcilero)                                                                                                                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund`<br/>`Capture`<br/>`Void`<br/>`WebRedirectDeposit`<br/>`FacileroWebRedirectDeposit`<br/>`FacileroBankWithdrawal`<br/>`FacileroWalletWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `FacileroConfig`                                                                                                                                                                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.facilero.FacileroConfig>
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
            <version>v1</version>
        </account>
    </entry>
    <entry>
      <string>FLEXEPIN</string>
      <account>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <memberId>??</memberId>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|NZD|CAD</supportedCurrencies>
        <terminal>xxxx</terminal>
        <version>v1</version>
      </account>
    </entry>
    <entry>
      <string>TIGERPAY</string>
      <account>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <memberId>??</memberId>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|NZD|CAD|JPY</supportedCurrencies>
        <terminal>xxxx</terminal>
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
</com.devcode.paymentiq.integration.facilero.FacileroConfig>
```
</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username             | Corresponds to the `user name` value from Facilero. It is the username to the merchant back office account and it is used in **AuhtToken** request                                                                                                                                                                                                                                                                                                                          |
| account.password             | Corresponds to the password to the merchant back office account.                                                                                                                                                                                                                                                                                                                                                                                                            |
| account.merchantId           | Corresponds to the `authentication.memberId` value from Facilero used in the all requests.                                                                                                                                                                                                                                                                                                                                                                                  |
| account.memberId             | Corresponds to `partnerId` value from Facilero. This is `partnerId` to the merchant back office account and it is used in the **AuhtToken** request.                                                                                                                                                                                                                                                                                                                        |
| account.secretKey            | Corresponds to `Secret Key` which  should be generated from merchant back office. It is used for both encryption and in **AuthToken** requests.                                                                                                                                                                                                                                                                                                                             |
| account.serviceEndpoint      | Request URL, provided by Facilero. This parameter must be added in case non default request URL should be used (default URL is: https://secure.facilero.com/transactionServices/REST/v1/).                                                                                                                                                                                                                                                                                  |
| account.use3Dsecure          | It is used to enable 3DS deposit                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| account.useTokenId           | It is used to enable recurring                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| account.authType             | - AUTH_CAPTURE <br/> - AUTH_CAPTURE <br/> - FINAL_AUTH <br/> - PRE_AUTH <br/>                                                                                                                                                                                                                                                                                                                                                                                               |
| account.withdrawalType       | It is used to enable OCT withdrawal, for which a prior successful deposit with the same PSP is required. In case this parameter is blank or missing, an independen withdrawal (for which no prior successful deposit is required) will be triggerd.                                                                                                                                                                                                                         |
| account.supportedCurrencies  | It is used to define supported currencies. `INR`, `USD`, `EUR`, `NZD`, `CAD`, `JPY` can be specified.                                                                                                                                                                                                                                                                                                                                                                       |
| account.terminal             | It is used to define terminal(s). Terminal defined at account level has higher priority than terminal defined using `terminalMapping` parameter and overrides terminal defined in `terminalMapping` parameter. Please check terminal definition examples below.                                                                                                                                                                                                             |
| terminalMapping              | It is used to define terminal(s). Please check terminal definition examples below.                                                                                                                                                                                                                                                                                                                                                                                          |
| paymentModeMapping           | It is used to define payment mode mapping based on `service` parameter. Please always check with Facilero which `paymentMode` should be used for your payment method and configure it in the **FacileroConfig** (or ask PaymentIQ technical support to do so) if it isn't defined by default.<br/>By default the following mapping is defined:<br/>`FLEXEPIN->PV,TIGERPAY->TPAY,TIGERGATE->TPAY,NET_BANKING_INR->NBI,NET_BANKING->NB,WALLET_INR->EWI,WALLET->EW,RUPAY->DC`. |
| transferTypeMapping          | It is used to define transfer type mapping based on `service` parameter. Please always check with Facilero which `transferType` should be used for your payment method and configure it in the **FacileroConfig** (or ask PaymentIQ technical support to do so) if it isn't defined by default.<br/>By default the following mapping is defined:<br/>`FLEXEPIN->FLEXEPIN VOUCHER,TIGERPAY->TigerPayWallet,TIGERGATE->JPBank`.                                               |
| sendCardHolderAsCustomerName | Set to true to send the input "card holder" as customer name. "card holder" will be splitted on the first space and use the first part as first name and the second part as last name                                                                                                                                                                                                                                                                                       |
| container                    | Indicates the way how the user will be redirected to the checkout URL (`window` is allowed only).                                                                                                                                                                                                                                                                                                                                                                           |

### Tokenized repeat or recurring payment
Merchants should have a PSP account with active tokenized payment. To activate tokenized payment, please check with the PSP.

After activating the tokenized payment on the PSP account, the merchant should activate the following flag in the FacileroConfig.
```xml
<useTokenId>true</useTokenId>
```
This is to be able to use the tokenized payment later on. This flag will activate registering credit card details at Facilero side.<br/>

In **FacileroConfig**, the recurring or repeat payment tx should be routed to another PSP account that has the following tags:
```xml
<useTokenId>true</useTokenId>
<use3Dsecure>false</use3Dsecure>
```

### Terminal Mapping
There are two ways to specify terminal mapping:
1. as `terminalMapping` root parameter in the **FacileroConfig** e.g. `<terminalMapping>RUPAY_INR->0000</terminalMapping>`;
2. as `terminal` account level parameter in the **FacileroConfig** (see examples below).

#### Credit Cards

| Terminal mapping examples                                        | Description                                                                                                                      |
|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| `<terminal>{TERMINAL_ID}</terminal>`                             | Defines a generic terminal for all card types and currencies                                                                     |
| `<terminal>{CARD_TYPE}->{TERMINAL_ID},...</terminal>`            | Defines a specific terminals for a different card types e.g. `VISA->0000,MASTERCARD->1111`                                       |
| `<terminal>{CARD_TYPE}_{CURRENCY}->{TERMINAL_ID},...</terminal>` | Defines a specific terminals for a different card types and currencies e.g. `VISA_EUR->0011,VISA_USD->0022,MASTERCARD_EUR->0033` |
| -                                                                | `UNKNOWN` will be sent in case no terminal map is configured or it can't be resolved                                             |

#### APMs

| Terminal mapping examples                                                      | Description                                                                                                                                                        |
|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `<terminal>{TERMINAL_ID}</terminal>`                                           | Defines a generic terminal for all payment methods and currencies                                                                                                  |
| `<terminal>{SERVICE}_{CURRENCY}->{TERMINAL_ID},...</terminal>`                 | Defines a specific terminals for a different services and currencies e.g. `RUPAY_INR->0000,UPI_INR->1111,FLEXEPIN_CAD->2222,TIGERPAY_USD->3333`                    |
| `<terminal>{SERVICE}_{PAYMENT_BRAND}_{CURRENCY}->{TERMINAL_ID},...</terminal>` | Defines a specific terminals for a different services, payment brands and currencies e.g. `TIGERPAY_TigerPay Wallet_USD->1111,FLEXEPIN_FLEXEPIN VOUCHER_USD->2222` |
| -                                                                              | `UNKNOWN` will be sent in case no terminal map is configured or it can't be resolved                                                                               |

## Configure APMs in PaymentIQ Back Office

Please make sure Facilero is enabled in PaymentIQ before it can be used. It can be done in the **MerchantConfig** by adding "Facilero" to the `<psps>` section:
```xml
<psps>Facilero|...</psps>
```

Before configuring any payment method, please make sure the following parameters are defined for account in your **FacileroConfig**:
```xml
<version>v1</version>
<secretKey>??</secretKey>
<terminal>??</terminal> <!--clarify it with provider-->
```
Please note, you can use one account for one payment method (in such case you can define terminal like `<terminal>xxxx</terminal>`).<br/>Also, you can use one account for a group of payment methods e.g. for Indian payment methods (in such case you can define several terminals like `<terminal>RUPAY_IND->xxxx,UPI_IND->xxxx,WALLET_IND->xxxx</terminal>`).


### RUPAY/UPI/WALLET/FLEXEPIN/TIGERPAY/TIGERGATE Deposit

RUPAY
- paymentMode=DC
- paymentBrand=RUPAY

UPI
- paymentMode=UPI
- paymentBrand=UPI

WALLET
- paymentMode=EW (EWI - for India)
- paymentBrand=??

FLEXEPIN
- paymentMode=PV
- paymentBrand=FLEXEPIN VOUCHER

TIGERPAY
- paymentMode=TPAY
- paymentBrand=TigerPay Wallet

TIGERGATE (JPBANK deposit)
- paymentMode=TPAY
- paymentBrand=JPBANK

1). **MerchantConfig**: configure a specific service for `WEBREDIRECT` provider type:
```xml
<entry>
  <string>WEBREDIRECT</string>
  <string>RUPAY|UPI|WALLET|FLEXEPIN|TIGERPAY|TIGERGATE|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `WEBREDIRECT_FLEXEPIN` as a deposit payment option<br/>
3). Create/Update routing rule by specifying `WebRedirectDeposit` transaction type.

#### Notes
- Similar steps are valid for deposit methods: RUPAY, UPI, WALLET, FLEXEPIN, TIGERPAY, TIGERGATE
- you can also use `FacileroWebRedirectDeposit` transaction type instead of `WebRedirectDeposit`. In that case you will have a possibility to provide a `paymentBrand` parameter (configure it in the Cashier Payment Method-settings) and it will be used to be sent in the request to Facilero. It might be useful as Facilero can add new payment brands for new acquirers e.g. `EW`(`EWI`) and `NB`(`NBI`).


### UPI Withdrawal

UPI
- paymentMode=UPI
- paymentBrand=UPI
- transferType=UPI

1). **MerchantConfig**: configure a specific service for `FACILEROWALLET` provider type:
```xml
<entry>
  <string>FACILEROWALLET</string>
  <string>UPI|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `FACILEROWALLET_UPI` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `FacileroWalletWithdrawal` transaction type.


### FLEXEPIN Voucher Withdrawal

FLEXEPIN<br/>
- paymentMode=PV
- paymentBrand=FLEXEPIN VOUCHER
- transferType=FLEXEPIN VOUCHER

1). **MerchantConfig**: configure a specific service for `FACILEROWALLET` provider type:
```xml
<entry>
  <string>FACILEROWALLET</string>
  <string>FLEXEPIN|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `FACILEROWALLET_FLEXEPIN` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `FacileroWalletWithdrawal` transaction type.


### TIGERPAY Wallet Withdrawal

TIGERPAY
- paymentMode=TPAY
- paymentBrand=TigerPay Wallet
- transferType=TigerPayWallet

1). **MerchantConfig**: configure a specific service for `FACILEROBANK` provider type:
```xml
<entry>
  <string>FACILEROBANK</string>
  <string>TIGERPAY|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `FACILEROBANK_TIGERPAY` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `FacileroBankWithdrawal` transaction type.


### TIGERGATE Bank Withdrawal

TIGERGATE
- paymentMode=TPAY
- paymentBrand=JPBANK
- transferType=JPBank

1). **MerchantConfig**: configure a specific service for `FACILEROBANK` provider type:
```xml
<entry>
  <string>FACILEROBANK</string>
  <string>TIGERGATE|...</string>
</entry>
```
2). **Rules** > **Payment Methods**: enable `FACILEROBANK_TIGERGATE` as a withdrawal payment option<br/>
3). Create/Update routing rule by specifying `FacileroBankWithdrawal` transaction type.


## Example Routing Rules

![](/img/providers/routing/facilero.png)

## Test Information

### Test Cards

| Brand      | 3DS | Card number      | Cvv | Expiry Date | Currency |
|------------|-----|------------------|-----|-------------|----------|
| VISA       | No  | 4488394721120087 | 111 | 12/30       | INR      |
| MasterCard | No  | 5555555555554444 | 111 | 12/30       | INR      |
| VISA       | No  | 4444333322221111 | 123 | 12/30       | USD      |
| MasterCard | No  | 5453010000070789 | 123 | 12/30       | USD      |
| VISA       | Yes | 4018490000000013 | 212 | 12/30       | USD      |
| MasterCard | Yes | 5186160400000011 | 100 | 12/30       | USD      |
