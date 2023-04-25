--- 
id: "ecommpay" 
title: "ECommPay"
hide_title: "true"
---
 
![](/img/providers/logos/ecommpay.png)

# ECommPay

## About
ECommPay is a payment provider that supports credit card and wallet payments.
For credit cards it offers 3DS and N3DS deposit (sale, authorization + capture), void, refund, withdrawal and status check. In order to make 3DS payment the user must use 3DS enrolled card and specify "use3Dsecure=true" in config.
For wallets (Yandex, Qiwi, WebMoney, Papara) it offers payin (deposit) and payout (withdrawal).

| Provider Name                | ECommPay                                                                                                                                              |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://ecommpay.com/](https://ecommpay.com/)                                                                                                        |
| Classification               | Credit Card and Wallet payments                                                                                                                       |
| Regions                      | `International`                                                                                                                                       |
| Currencies                   | `SEK`, `EUR`                                                                                                                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Capture`<br/> `Void`<br/> `ECommPayWalletDeposit`<br/> `ECommPayWalletWithdrawal` |
| PaymentIQ Configuration File | `ECommPayConfig`                                                                                                                                      |

## APM (Using the ECommPayWalletDeposit or ECommPayWalletWithdrawal)

| PaymentIQ Service           | ECommPay name / documentation                                                                                      |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------|
| QIWI                        | [Qiwi](https://developers.trxhost.com/en/pm_qiwi_wallet_gate.html#pm_qiwi_wallet_gate)                             |
| YANDEX                      | [Yandex.Money](https://developers.trxhost.com/en/pm_yandex_gate.html#pm_yandex_gate)                               |
| WEBMONEY                    | [WebMoneyClassic](https://developers.trxhost.com/en/pm_webmoney_gate.html#pm_webmoney_gate)                        |
| WEBMONEY_LIGHT              | [WebMoneyLight](https://developers.trxhost.com/en/pm_webmoney_gate.html#pm_webmoney_gate)                          |
| PAPARA                      | [Papara](https://developers.trxhost.com/en/pm_papara_gate.html#pm_papara_gate)                                     |
| BANKS_OF_PHILIPPINES        | [Banks of the Philippines](https://developers.trxhost.com/en/pm_philippines.html#pm_philippines)                   |
| PHILIPPINES_PAYMENT_CENTERS | [Philippines Payment Centers](https://developers.trxhost.com/en/pm_philippines_cash.html#pm_philippines_cash)      |
| PHILIPPINES_OTC_ATM         | [Philippines Over the Counter & ATM](https://developers.trxhost.com/en/pm_philippines_atm.html#pm_philippines_atm) |
| COINS_PH                    | [Coins.ph](https://developers.trxhost.com/en/pm_coinsph.html#pm_coinsph)                                           |
| GCASH                       | [GCash](https://developers.trxhost.com/en/pm_gcash.html#pm_gcash)                                                  |
| GRABPAY                     | [GrabPay](https://developers.trxhost.com/en/pm_grabpay.html#pm_grabpay)                                            |
| BANKS_OF_INDIA              | [Banks of India](https://developers.trxhost.com/en/pm_india.html)                                                  |
| BANKS_OF_INDONESIA_VA       | [ATM & Bank Transfer in Indonesia (Virtual Accounts)](https://developers.trxhost.com/en/pm_indonesia_va.html)      |
| THAILAND_QR_BANKING         | [Thailand QR banking](https://developers.trxhost.com/en/pm_thailandqr.html)                                        |
| MOMO_WALLET                 | [MoMo Wallet](https://developers.trxhost.com/en/pm_momoqr.html)                                                    |

## APM (Using CreditcardDeposit or CreditcardWithdrawal)
| PaaymentIQ Service | ECommPay name / documentation                                                            |
|--------------------|------------------------------------------------------------------------------------------|
| CHINA_UNION_PAY    | [CUP P2P](https://developers.trxhost.com/en/pm_cup_p2p_gate.html#en_pm_cup_p2p_overview) |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.ecommpay.ECommPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string> <!-- use for credit cards -->
      <account>
        <secretKey>??</secretKey>
        <projectId>??</projectId>
        <useTokenId>false</useTokenId>
        <authType>AUTH_CAPTURE</authType><!--FINAL_AUTH, AUTH_CAPTURE-->
        <supportedCurrencies>USD|RUB</supportedCurrencies>
        <templateName>ecommpay-3ds-loading-template</templateName>
      </account>
    </entry>
    
    <entry>
      <string>YANDEX</string>
      <account>
        <secretKey>??</secretKey>
        <projectId>??</projectId>
        <supportedCurrencies>RUB</supportedCurrencies>
        <container>window</container>
        <templateName>ecommpay-wallet-loading-template</templateName>
      </account>
    </entry>
    
    <entry>
    <string>QIWI</string>
      <account>
        <secretKey>??</secretKey>
        <projectId>??</projectId>
        <supportedCurrencies>USD|RUB</supportedCurrencies>
        <container>iframe</container>
        <width>600</width>
        <height>600</height>
        <templateName>ecommpay-wallet-loading-template</templateName>
      </account>
    </entry>
    
    <!-- PAPARA -->
    <entry>
    <string>PAPARA</string>
      <account>
        <secretKey>??</secretKey>
        <projectId>??</projectId>
        <supportedCurrencies>TRY</supportedCurrencies>
        <container>iframe</container>
        <width>600</width>
        <height>600</height>
        <templateName>ecommpay-wallet-loading-template</templateName>
      </account>
    </entry>
    
    <entry>
    <string>WEBMONEY</string>
      <account>
        <secretKey>??</secretKey>
        <projectId>??</projectId>
        <supportedCurrencies>RUB|EUR|USD</supportedCurrencies>
        <container>iframe</container>
        <width>600</width>
        <height>600</height>
        <templateName>ecommpay-wallet-loading-template</templateName>
      </account>
    </entry>
    
    <entry>
    <string>WEBMONEY_LIGHT</string>
      <account>
        <secretKey>??</secretKey>
        <projectId>??</projectId>
        <supportedCurrencies>RUB|EUR|USD</supportedCurrencies>
        <container>iframe</container>
        <width>600</width>
        <height>600</height>
        <templateName>ecommpay-wallet-loading-template</templateName>
      </account>
    </entry>
    
  </accounts>
  <defaultDescriptor>??</defaultDescriptor> <!-- Set the descriptor which will be displayed on the cardholder's statement -->
</com.devcode.paymentiq.integration.ecommpay.ECommPayConfig>
```

</details>

### Attributes

| Attribute               | Description                                                                                                                                                                                                                                                                                                                                                                                                               | Default value   |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| projectId               | Project ID. Provided by ECommPay.                                                                                                                                                                                                                                                                                                                                                                                         |                 |
| secretKey               | This key is used to generate SHA512 signature. Provided by ECommPay.                                                                                                                                                                                                                                                                                                                                                      |                 |
| enableCascading         | To enable cascading between 3DS2 and 3DS1                                                                                                                                                                                                                                                                                                                                                                                 |                 |
| validAccountNumberRegex | Map from service parameter to regex for validation of the account numbers entered by the user during wallet transactions. If configured for the current service, the regex will be applied on the entered account number and the transaction will fail with status `ERR_DECLINED_INVALID_ACCOUNT_NUMBER` if it does not match. This validation is done during `validate` and `process` for both deposits and withdrawals. | QIWI->[0-9]{11} |

### Callback URLs
In order to make a successful credit card or wallet payment via ECommPay the merchant should ask ECommPay to configure below callback URLs:

`https://{env-host}/paymentiq/api/mntx/callback` - for credit card related payments

`https://{env-host}/paymentiq/api/mntx/callback/wallet` - for Yandex and Qiwi and other wallet related payments

{env-host} is to be replaced with `test-api.paymentiq.io` for the test environment and `api.paymentiq.io` for the prod environment.

## Card Holder Validation

1. Dot can be used only once.
EXAMPLE: ("Anthony Jr. Smith" - OK, "Anthony Jr. Smith Jr. " - NOT OK)
2. The field 'holder' must contain no less than two words. where each word must consist of at least two letters.
EXAMPLE: ("Al Mahal" - OK, "A Mahal" - NOT OK)
3. The symbol "-" is identified as splitter between words.
EXAMPLE: ("Ed Malone" - OK, "E-d Malone" - NOT OK)
4. Only Latin letters can be used.

## Limits

### Credit Card

1. Limits per card (Russian Cardholder) per day: min transaction - 1 RUB; max transaction – 600,000 RUB; limit per day/month – none
2. Limits per card (Not Russian Cardholder) per day: min transaction – 100EUR (or equal in other currency); max transaction – 100,000 RUB; limit per day for card – 100,000 RUB; limit per month – none. Visa not available for non Russian cardholders for current moment, however it will be soon.

### YandexMoney

#### Payin

Min depostit: 1 RUB

Max deposit:
- for anonymous users — 15 000 RUB;
- for nominal wallet type — 60 000 RUB;
- for identified wallet type — 250 000 RUB.

#### Payout

Min transaction amount: 1 RUB;

Max transaction amount:
- anonymous wallet — not more than 15 000 RUB;
- nominal or identified status — not more than 60 000 RUB

### Qiwi

#### Payin

Min Transaction amount: 1 RUB

Max Transaction amount:
- 3-rd level of wallet (minimal) - 15,000 RUB per/operation, not more than 40,000 RUB per/month
- 2-nd level of wallet (main) - 60,000 RUB per/operation, not more than 200,000 RUB per/month
- 1-st level of wallet (professional) - 500,000 RUB per/operation

#### Payout

Min Transaction amount: 1 RUB

Max Transaction amount depends on wallet type: 15,000 RUB/60,000 RUB/250,000 RUB

### WebMoney / WebMoney light

#### Payin

Min Transaction amount: 0,01 BYN, EUR, KZT, RUB, VND, UAH, USD

Max Transaction amount depends webmoney passport

#### Payout

Min Transaction amount: 0,01 BYN, EUR, KZT, RUB, VND, UAH, USD

Max Transaction amount depends webmoney passport

### Papara

#### Payin

Min Transaction amount: 100 TRY

Max Transaction amount: 10,000.00 TRY

#### Payout

Min Transaction amount: 50 TRY

Max Transaction amount: 10,000.00 TRY

### Banks of the Philippines

#### Payin

Min Transaction amount: 1 PHP

Max Transaction amount: 1,000,000 PHP

#### Payout

Min Transaction amount: 10 PHP

Max Transaction amount: 100,000 PHP

### Philippines Payment Centers

#### Payin

Min Transaction amount: 1 PHP

Max Transaction amount: 1,000,000 PHP

#### Payout

Min Transaction amount: 10 PHP

Max Transaction amount: 100,000 PHP

### Philippines Over the Counter & ATM

#### Payin

Min Transaction amount: 1 PHP

Max Transaction amount: 1,000,000 PHP

#### Payout
Not supported

### Coins.ph

#### Payin

Min Transaction amount: 1 PHP

Max Transaction amount: 1,000,000 PHP

#### Payout
Not supported

### GCash

#### Payin

Min Transaction amount: 1 PHP

Max Transaction amount: 10,000 PHP

#### Payout

Min Transaction amount: 10 PHP

Max Transaction amount: 100,000 PHP

### GrabPay

#### Payin

Min Transaction amount: 1 PHP

Max Transaction amount: 10,000 PHP

#### Payout
Not supported

### CUP P2P

#### Payin

Min Transaction amount: 600 CNY

Max Transaction amount: 49,000 CNY

#### Payout

Min Transaction amount: 10 CNY

Max Transaction amount: 44,999 CNY


## Supported countries / currencies
| Payment method                     | Currency                                        | Countries                                                                                                                                                                                                                |
|------------------------------------|-------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Credit Card                        | `No limit`                                      | `Australia`, `Indonesia`, `Iran`, `Canada`, `South Korea`, `Cote d'Ivoire (Ivory Coast)`, `Lebanon`, `Macedonia`, `Malaysia`, `Nigeria`, `New Zealand`, `Pakistan`, `USA`, `Siria`, `Sudan`, `Cuba`, `North Korea`, `Uk` |
| CUP P2P                            | `CNY`                                           | `China`                                                                                                                                                                                                                  |
| Yandex                             | `RUB`                                           | `Russia`                                                                                                                                                                                                                 |
| Qiwi                               | `RUB`                                           | `Russia`                                                                                                                                                                                                                 |
| Webmoney                           | `BYN`, `EUR`, `KZT`, `RUB`, `VND`, `UAH`, `USD` | `No limit`                                                                                                                                                                                                               |
| Papara                             | `TRY`                                           | `Turkey`                                                                                                                                                                                                                 |
| Banks of the Philippines           | `PHP`                                           | `Philippines`                                                                                                                                                                                                            |
| Philippines Payment Centers        | `PHP`                                           | `Philippines`                                                                                                                                                                                                            |
| Philippines Over the Counter & ATM | `PHP`                                           | `Philippines`                                                                                                                                                                                                            |
| Coins.ph                           | `PHP`                                           | `Philippines`                                                                                                                                                                                                            |
| GCash                              | `PHP`                                           | `Philippines`                                                                                                                                                                                                            |
| GrabPay                            | `PHP`                                           | `Philippines`                                                                                                                                                                                                            |
| Banks of India                     | `INR`                                           | `India`                                                                                                                                                                                                                  |
| Banks of Indonesia                 | `IDR`                                           | `Indonesia`                                                                                                                                                                                                              |
| Banks of Thailand                  | `THB`                                           | `Thailand`                                                                                                                                                                                                               |
| Banks of Vietnam                   | `VND`                                           | `Vietnam`                                                                                                                                                                                                                |
| Banks of Malaysia                  | `MYR`                                           | `Malaysia`                                                                                                                                                                                                               |
| ATM & Bank Transfer in Indonesia   | `INR`                                           | `Indonesia`                                                                                                                                                                                                              |
| Thailand QR banking                | `THB`                                           | `Thailand`                                                                                                                                                                                                               |
| MoMo Wallet                        | `VND`                                           | `Vietnam`                                                                                                                                                                                                                |


## Example Routing Rules

### Credit Card

![](/img/providers/routing/ecommpay.png)

### Wallet

![](/img/providers/routing/ecommpay_wallet.png)

### CUP P2P
The China UnionPay card service uses the `CreditcardDeposit` and `CreditcardWithdrawal` transaction types, but must be routed to an account configured for wallet callbacks.

## Test Information

## 3DS1 and N3DS

| Card Brand | Number           | CVV | Expiry date | Result/Info     |
|------------|------------------|-----|-------------|-----------------|
| Visa       | 4314220000000056 | Any | Any         | Approved (3DS)  |
| Visa       | 4314220000000072 | Any | Any         | Declined (3DS)  |
| Visa       | 4477000000000006 | Any | Any         | Approved (N3DS) |
| Visa       | 4477000000000014 | Any | Any         | Declined (N3DS) |
| MasterCard | 5413330000000019 | Any | Any         | Approved (3DS)  |
| MasterCard | 5413330000000035 | Any | Any         | Declined (3DS)  |
| MasterCard | 5252000000000004 | Any | Any         | Approved (N3DS) |
| MasterCard | 5252000000000012 | Any | Any         | Declined (N3DS) |

## 3DS2

| Card Brand | Number           | CVV | Expiry date | Result/Info             | Use for cascading |
|------------|------------------|-----|-------------|-------------------------|-------------------|
| Visa       | 4477000000000006 | Any | Any         | Approved (frictionless) | No                |
| Visa       | 4012000000020063 | Any | Any         | Declined (frictionless) | No                |
| Visa       | 4314220000000056 | Any | Any         | Approved (challenge)    | No                |
| Visa       | 4012000000020089 | Any | Any         | Declined (challenge)    | Yes               |
| MasterCard | 5252000000000004 | Any | Any         | Approved (frictionless) | No                |
| MasterCard | 5544330000000029 | Any | Any         | Declined (frictionless) | No                |
| MasterCard | 5413330000000019 | Any | Any         | Approved (challenge)    | No                |
| MasterCard | 5544330000000045 | Any | Any         | Declined (challenge)    | Yes               |

## CUP P2P
Use the card number `4111111111111111` for testing.

### Yandex, Qiwi, WebMoney and Papara
In order to do wallet payments via Yandex, Qiwi, WebMoney or Papara user should use real wallet accounts with real money.

## Payment Flow

### 3DS2 Payment
In order to make 3DS2 payments you will have to talk to ECommPay support to enable that on your project. 
In PaymentIQ you will have to use a psp account with 3DS enabled ("use3Dsecure=true"). 
In Staging you can use the 3DS2 testing cards to test each flow.

#### Fallback cascading
ECommPay can do a fallback (cascade) to 3DS1 if the card was not enrolled for 3DS2.
This can be enabled by setting the ("enableCascading=true") on EcompayConfig root level or psp account level (The account will override the root).
To simulate this scenario in test use the 3DS2 testing cards and one that has (Use for cascading=Yes).

### 3DS Payment
In order to make 3DS payment the user should use 3DS related card (e.g. 4314220000000056) and enable 3DS in config ("use3Dsecure=true").
In case of 3DS payment the user will be redirected to 3DS authentication page where security code must be entered (1234 on TEST).

![](/img/providers/ecommpay_3ds_auth.png)

Once it is done, user will be redirected to success or failed page, depending on payment status.

### YandexMoney Payment

#### Payin
To initiate YandexMoney deposit, user should just enter amount, and then he/she will be redirected to YandexMoney page to complete payment.
In order to do it, user should select his/her Yandex wallet, specify some personal info (e.g. date of birth, passport ID, ...) and also password, sent by Yandex via SMS.

![](/img/providers/ecommpay_yandex_01.png)

After all required fields are specified, the user will have to press pay button in order to complete payment. In case of successful payment the following page will be shown

![](/img/providers/ecommpay_yandex_02.png)

#### Payout
To do payout user should specify amount and Yandex wallet account number and then press pay button.


### Qiwi Payment

#### Payin
To initiate Qiwi deposit, user should specify amount and account number (basically it is phone number), and then he/she will be redirected to Qiwi page to complete payment.
In order to do it, user should specify SMS code or wallet password as depicted below:

![](/img/providers/ecommpay_qiwi_01.png)

Then Qiwi will ask again if payment should be processed

![](/img/providers/ecommpay_qiwi_02.png)

and if yes, user will need to enter SMS code once again in order to confirm payment

![](/img/providers/ecommpay_qiwi_03.png)

After payment is done, user will see a result page

![](/img/providers/ecommpay_qiwi_04.png)

#### Payout
To do payout user should specify amount and Qiwi wallet account number (mobile phone) and then press pay button.

### WebMoney Payment

#### Payin

##### WebMoneyClassic

To initiate WebMoneyClassic deposit, user should enter amount and WebMoney e-wallet number, and then he/she will be redirected to its WebMoney APP on dektop or mobile where payment is completed.

##### WebMoneyLight

To initiate WebMoneyLight deposit, user should just enter amount, and then he/she will be redirected to WebMoney page to complete payment.

#### Payout

To do payout user should specify amount and WebMoney e-wallet number and then press pay button.

### Papara Payment

#### PayIn

To initiate Papara deposit, user should just enter amount, and then he/she will be redirected to Papara page to complete payment.

#### Payout

To do payout user should specify amount and Papara wallet account number and then press pay button.
