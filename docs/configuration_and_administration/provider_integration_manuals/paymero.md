--- 
id: "paymero" 
title: "Paymero"
hide_title: "true"
---
 
![](/img/providers/logos/paymero.png)

# Paymero

## About
Paymero is a payment provider offering bank deposit, withdrawal, reversal and crypto deposit and withdrawal operations.

| Provider Name                | Paymero                                                                                                                                          |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://paymero.com/](https://paymero.com/)                                                                                                     |
| Classification               | Online Banking / Cryptocurrency                                                                                                                  |
| Regions                      | China, India, Thailand, Malaysia, Vietnam, Indonesia                                                                                             |
| Currencies                   | `CNY`, `INR`, `THB`, `VND`, `MYR`, `IDR`                                                                                                         |
| Cryptocurrencies             | `BTC`, `BCH`, `BSV`, `ETH`, `LTC`, `USDT (ERC-20)`                                                                                               |
| Methods/PaymentTxTypes       | `BankDeposit`<br/>`WebRedirectDeposit`<br/>`PaymeroBankIntlWithdrawal`<br/>`Reversal`<br/>`CryptoCurrencyDeposit`<br/>`CryptoCurrencyWithdrawal` |
| PaymentIQ Configuration File | `PaymeroConfig`                                                                                                                                  |

### Supported Bank Operations

#### Deposit

| Currency | Bank Transfer | Virtual Account | P2P | QR | UPI | Net Banking | Wallet |
|----------|---------------|-----------------|-----|----|-----|-------------|--------|
| CNY      |               |                 | +   |    |     |             |        |
| IDR      | +             | +               |     |    |     |             |        |
| INR      | +             |                 |     |    | +   | +           | +      |
| MYR      | +             |                 |     |    |     |             |        |
| THB      | +             |                 |     | +  |     |             |        |
| VND      | +             |                 |     |    |     |             |        |

#### Withdrawal

| Currency | Bank Transfer |
|----------|---------------|
| CNY      | +             |
| IDR      | +             |
| INR      | +             |
| MYR      | +             |
| THB      | +             |
| VND      | +             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paymero.PaymeroConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <!--'default' account is required in order to retrieve available banks for a specific payment method (Bank Transfer or Virtual Account payments)-->
    <entry>
      <string>default</string>
      <account>
        <apiKey>??</apiKey>
        <supportedCurrencies>CNY|THB|VND|IDR|MYR|INR</supportedCurrencies>
      </account>
    </entry>
    <!--'ALL_CURRENCIES' account can be used to make Bank Transfer deposit or withdrawal as long as payment via Hosted Payment Page-->
    <entry>
      <string>ALL_CURRENCIES</string>
      <account>
        <apiKey>??</apiKey>
        <!--CNY: "储蓄卡" (Debit Card) or "信用卡" (Credit Card)-->
        <cardType>信用卡</cardType>
        <supportedCurrencies>CNY|THB|VND|IDR|MYR|INR</supportedCurrencies>
      </account>
    </entry>
    <!--'VA' account can only be used to make Bank Virtual Account deposit as it can only be made for `IDR` currency-->
    <entry>
      <string>VA</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <productName>Virtual Account product</productName>
        <supportedCurrencies>IDR</supportedCurrencies>
      </account>
    </entry>
    <!--'P2P' account can only be used to make a P2P deposit as it can only be made for `CNY` currency-->
    <entry>
      <string>P2P</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <productName>P2P product</productName>
        <supportedCurrencies>CNY</supportedCurrencies>
      </account>
    </entry>
    <!--'QR' account can only be used to make a QR deposit as it can only be made for `THB` currency-->
    <entry>
      <string>QR</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <productName>QR product</productName>
        <supportedCurrencies>THB</supportedCurrencies>
      </account>
    </entry>
    <!--'CRYPTO' account can be used to make a Crypto Currency deposit and withdrawal-->
    <entry>
      <string>CRYPTO</string>
      <account>
        <apiKey>??</apiKey>
        <!--<targetCurrency>USD</targetCurrency>-->
        <supportedCurrencies>CNY|THB|VND|IDR|MYR|INR|USD|EUR|GBP</supportedCurrencies><!--USD,EUR,GBP for liquidation-->
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <testMode>true</testMode>
  <defaultDescriptor>Payment: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.paymero.PaymeroConfig>
```
</details>

### Attributes

| Attribute              | Required    | Description                                                                                            |
|------------------------|-------------|--------------------------------------------------------------------------------------------------------|
| account.merchantId     | No          | Merchant ID defined by the Paymero. It is used to authenticate the requests from PIQ to the PSP.       |
| account.apiKey         | Yes         | Corresponds to the *API Key* from Paymero. It is used to authenticate the requests from PIQ to the PSP |
| account.cardType       | Conditional | Required for `CNY` Bank Withdrawal only                                                                |
| account.targetCurrency | Conditional | Required only for cryptocurrency payments if liquidation is needed                                     |
| account.productName    | Yes         | Product name (please put merchandise descriptions here)                                                |

### Note

The provider should send all the required account details (SANDBOX or LIVE) to the merchant and the merchant should contact PaymentIQ tech support in order to configure the requested payment options by sending an email to technicalsupport@bambora.com. If it is a new merchant, they will need to send a corresponding email to the PaymentIQ onboarding team using onboardingiq@bambora.com.

## Example Routing Rules

### Bank Operations

![](/img/providers/routing/paymerorouting_bank.png)

### Cryptocurrency Operations

![](/img/providers/routing/paymerorouting_crypto.png)

## Test Information

### Online Banking

Please use a corresponding PaymentTxType and Service to make Deposit or Withdrawal operation like is shown below.

#### DEPOSIT

| Operation               | PaymentTxType      | Service            |
|-------------------------|--------------------|--------------------|
| Bank Transfer Deposit   | BankDeposit        | FAST_BANK_TRANSFER |
| Virtual Account Deposit | BankDeposit        | VIRTUAL_ACCOUNT    |
| Net Banking Deposit     | BankDeposit        | NET_BANKING        |
| UPI Deposit             | BankDeposit        | UPI                |
| Wallet Deposit          | BankDeposit        | WALLET             |
| P2P Deposit             | WebRedirectDeposit | P2P                |
| QR Deposit              | WebRedirectDeposit | QR                 |
| Hosted Payment Page     | WebRedirectDeposit | none               |

#### WITHDRAWAL

| Operation                | PaymentTxType             | Service            |
|--------------------------|---------------------------|--------------------|
| Bank Transfer Withdrawal | PaymeroBankIntlWithdrawal | FAST_BANK_TRANSFER |

### Cryptocurrency

On sandbox MID only `BTC` (Bitcoin) and `TST` (Tether) currencies are allowed.

Paymero has limits on trade/liquidation and these are the following:

`0.001 BTC` \
`0.01 ETH` \
`0.01 BCH` \
`0.1 LTC`

 e.g. they can't process a smaller deposit and / or payout than this amount in crypto.

#### DEPOSIT

Before making a cryptocurrency deposit user will have to request to generate a new wallet address that will be used to make a payment.

It can be done from PaymentIQ Cashier by selecting required cryptocurrency and pressing "Complete Purchase" button like is shown below:

![](/img/providers/paymero_001.png)

After wallet address is generated it will be show on the UI

![](/img/providers/paymero_002.png)

User can use this address to make a cryptocurrency deposit. It can be used once or multiple times (it is preferred to use a unique wallet address for each new payment).

Cryptocurrency deposit itself is triggered by the provider, and once it is done, PaymentIQ will receive a corresponding notification and will create a new payment tx.

##### What is liquidation?

In some cases merchant doesn't want to store cryptocurrency, but only use it as a deposit method. In such situation Paymero converts it to fiat and settles with merchant as per agreement.
In other words, if merchant's user sends BTC to merchant's wallet address, Paymero will not store it like BTC but will convert it to fiat (EUR, GBP or USD) as shown in the table below.
In case of no-liquidation, merchant will receive money in same currency that was sent by his user e.g. BTC (if targetCurrency wasn't specified), or will be converted to another crypto currency if targetCurrency was specified (BTC, USDT, ETH) as show in the table below.

If liquidation is required then you can pass targetCurrency as USD/GBP/EUR, but if targetCurrency is missing it will be the same like currency and liquidation will not happen.

| Currency        | Description                              | Examples                                                                                             |
|-----------------|------------------------------------------|------------------------------------------------------------------------------------------------------|
| sourceCurrency  | User deposited cryptocurrency            | BTC, USDT, ETH                                                                                       |
| targetCurrency  | Merchant balance in Paymero system       | 1. if liquidation is required (EUR, GBP, USD)<br/>2. if liquidation is not required (BTC, USDT, ETH) |
| cashierCurrency | Merchant system cashier balance currency | CNY, MYR, THB, IDR, INR, VND, EUR, GBP, USD                                                          |

More info about cryptocurrency payments can be found [here](https://api-docs.paymero.io/#46946d14-e110-4bc5-8c21-24e7e7e11f13).

#### WITHDRAWAL

To make a cryptocurrency withdrawal using PaymentIQ cashier, user will have to choose Cryptocurrency payment option and specify fiat amount, withdrawal wallet address (it is not the same wallet address generated during deposit flow) and cryptocurrency and press "Withdrawal" like is shown below

![](/img/providers/paymero_003.png)

##### BTC test wallet addresses that can be used for testing

- mg9EdNKdqUEcAGLLivE5KcFJG5zLkxPgad

- 2MxVWwaqS7Eo2BCLpJ372QQHFeAQPs47L6Y
