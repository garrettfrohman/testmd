--- 
id: "unlimint" 
title: "Unlimint (formerly CardPay)"
hide_title: "true"
---
 
![](/img/providers/logos/unlimint.png)

# Unlimint

## About
Unlimint is a credit-card processor with support for Deposit, Withdrawal, refund and APMs (v3).

| Provider Name                | Unlimint                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.unlimint.com/](https://www.unlimint.com/)                          |
| Classification               | Debit / Credit Card Processor                                                   |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | See [v2](#cardpay-v2) or [v3](#cardpay-v3)                                      |
| PaymentIQ Configuration File | `CardPayRestConfig`                                                             |

### Prerequisites
* Unlimint has one deprecated config `CardPayConfig` and one current `CardPayRestConfig`. To route and use the new `CardPayRestConfig` we will have to add a `Action` called `PSP Version` with the value `REST`.  Example of this can be found in the [routing section](#example-routing-rule-v3) for the
* For v3, each payment method has to be enabled from Unlimint side
* For v3, n3ds for bankcard must be enabled from Unlimint side
* For v3, for each currency a new wallet / terminal must be configured at PaymentIQ side.
* For v3 supports 3ds2 if the merchant is in s2s mode.

## CardPay v2

### PaymentTxTypes
`CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`

### Configuration Information CardPayConfig

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.cardpay.CardPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username>
        <password>???</password>
        <merchantId>???</merchantId>
        <secretKey>???</secretKey> <!-- aka CardPay's secret word -->
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
        <supportedCurrencies>USD|GBP|EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
  <dynamicDescriptor>Bambora Payment dynamic</dynamicDescriptor>
</com.devcode.paymentiq.integration.cardpay.CardPayConfig>
```
</details>

#### Configuration Attributes

| Attribute         | Description                            |
|-------------------|----------------------------------------|
| username          | Unlimint username                      |
| merchantId        | Unlimint merchant Id                   |
| password          | Unlimint passwrord                     |
| secretKey         | Unlimint secret word                   |
| defaultDescriptor | Sent to Unlimint as description        |
| dynamicDescriptor | Sent to Unlimint as dynamic_descriptor |


#### Callback

Before testing the merchant needs to set callback URL (ask Unlimint to do it):

| Environment | URL                                                                          |
|-------------|------------------------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/cardpay/callback/{number}/{note} |
| PROD        | https://api.paymentiq.io/paymentiq/api/cardpay/callback/{number}/{note}      |

#### Callback for v3

For version 3 the callback URLs has to be slightly alterned as the mappings on the provider end has changed.

| Environment | URL                                                                                     |
|-------------|-----------------------------------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/cardpay/callback/{merchant_order_id}/{note} |
| PROD        | https://api.paymentiq.io/paymentiq/api/cardpay/callback/{merchant_order_id}/{note}      |

### Example Routing Rule v2
![](/img/providers/routing/cardpay.png)

## CardPay v3

### PaymentTxTypes
`CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`, `Void`, `CreditcardAccountVerification`, `Capture`, `BoletoBancarioDeposit`, `LotericaDeposit`, `PagoEfectivoDeposit`, `OxxoDeposit`, `WebRedirectDeposit`, `BankDeposit`, `ThreeDS2Authentication`

### Configuration Information CardPayRestConfig

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.cardpay.rest.CardPayRestConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>BRL</string>
      <account>
        <password>???</password>
        <terminal>???</terminal>
        <secretKey>???</secretKey>
        <supportedCurrencies>BRL</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>EUR</string>
      <account>
        <password>???</password>
        <terminal>???</terminal>
        <secretKey>???</secretKey>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.cardpay.rest.CardPayRestConfig>
```
</details>

#### Configuration Attributes

| Attribute           | Description                                              |
|---------------------|----------------------------------------------------------|
| password            | password of terminal (terminal password)                 |
| terminal            | terminal_code of Unlimint of specific currency           |
| secretkey           | callback secret                                          |
| supportedCurrencies | currency of that specific terminal_code                  |
| services            | service mapping of PaymentIQ service to Unlimint service |
| bankMappings        | bank mapping used for DEPOSITEXPRESSBRL                  |
| defaultDescriptor   | Sent to Unlimint as description                          |
| dynamicDescriptor   | Sent to Unlimint as dynamic_descriptor                   |

#### Terminal / Wallets

* Each terminal / wallet supports a specific currency and APMs. Each terminal / wallet has a specific `callback secret` and `password`.
* Each `currency` that will be a used then a new wallet has to be configured, routed to.
* The `terminal password` and `callback secret` can be found in Unlimint BO but will only be shown once (After that Unlimint support must be contacted to get them).

#### Callback

Before testing the merchant needs to set callback URLs. Can be done from Unlimint backoffice or Unlimint support can add it. Each terminal / wallet has a callback url.

| Environment | URL                                                                                   |
|-------------|---------------------------------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/cardpay/rest/callback/{merchant_order_id} |
| PROD        | https://api.paymentiq.io/paymentiq/api/cardpay/rest/callback/{merchant_order_id}      |

### Modes
Cardpay v3 has 3 modes (gateway, payment page and s2s).
PaymentIQ supports gateway and s2s mode. 
The mode is administrated from Unlimint side. So please contact Unlimint support to change mode.

#### Gateway
Supports Apm, Creditcard payments, n3ds, 3ds1 (cardpay mpi)

##### s2s
Supports Apm, Creditcard payments, n3ds, 3ds1 (cardpay mpi), 3ds1 (external mpi), 3ds2 (external mpi)

### APMs

| APM                    | TxType                                  | Service           |
|------------------------|-----------------------------------------|-------------------|
| Boleto                 | BoletoBancarioDeposit                   | BOLETO            |
| Loterica               | LotericaDeposit                         | LOTERICA          |
| Oxxo                   | OxxoDeposit                             | OXXO              |
| Direct Banking Europe  | BankDeposit                             | DIRECTBANKINGEU   |
| Deposit Express Brasil | BankDeposit                             | DEPOSITEXPRESSBRL |
| Bankcard               | CreditcardDeposit, CreditcardWithdrawal | BANKCARD          |
| Paynet                 | WebRedirectDeposit                      | PAYNET            |
| WebMoney               | WebRedirectDeposit                      | WEBMONEY          |
| PagoEfectivo           | PagoEfectivoDeposit                     | PAGOEFECTIVO      |

More services can be used by adding more services to the `services` attribute in CardPayRestConfig. The one added in config will be merged with the defaults.
This services can then be used with `bankDeposit` or `webRedirectDeposit`

Please contact your AM if you want to add a service that is not listed above that Unlimint can offer.

### BankMappings (used for DEPOSITEXPRESSBRL)

This mapping is added by default. More can be added in the `bankMappings` attribute in CardPayRestConfig. The defaults will be merged with the customs.

| Country | Bank name       | Card pay bank code |
|---------|-----------------|--------------------|
| BRA     | ITAU            | itau               |
| BRA     | Santander       | santander          |
| BRA     | Bradesco        | bradesco           |
| BRA     | Banco do Brasil | banco-do-brasil    |

List of bank codes for DEPOSITEXPRESSBRL can be found [here](https://integration.cardpay.com/#bank-codes-depositexpressbrl)

### Sending `identity` value to Unlimint for credit card deposits

This value is used for 'Latin America' customer's and it corresponds to the personal identification number: 'CPF' or 'CNPJ' for Brazil, 'DNI' for Argentina and ID for other countries.

To provide this value to PIQ you can collect this from the end-user in the cashier and send it in the parameter `nationalId` in the CreditcardDeposit request.

If you as a merchant is using PIQ's standardized cashier, you will have to add this specific `nationalId` input to the Cashier Payment Method-settings. Please contact the support for assistance.

### Example Routing Rule v3
![](/img/providers/routing/cardpayv3.png)

## Test Information

### Creditcard

#### 3DS

| Card Brand | Account          | CVV | Expiry date | Outcome   |
|------------|------------------|-----|-------------|-----------|
| VISA       | 4000000000000002 | Any | Any         | CONFIRMED |
| VISA       | 4000000000000044 | Any | Any         | PENDING   |
| MASTERCARD | 5555555555554444 | Any | Any         | DECLINED  |

#### 3DS2

| Card Brand | Account          | CVV | Expiry date | Outcome   |
|------------|------------------|-----|-------------|-----------|
| VISA       | 4000000000000093 | Any | Any         | CONFIRMED |
| VISA       | 4000000000000069 | Any | Any         | CONFIRMED |
| VISA       | 4000000000000085 | Any | Any         | CONFIRMED |

#### N3DS

| Card Brand | Account          | CVV | Expiry date | Outcome   |
|------------|------------------|-----|-------------|-----------|
| VISA       | 4000000000000077 | Any | Any         | CONFIRMED |
| VISA       | 4000000000000051 | Any | Any         | PENDING   |
| MASTERCARD | 5555555555554477 | Any | Any         | DECLINED  |

### Paynet

| Email               | Outcome   |
|---------------------|-----------|
| decline@decline.com | DECLINED  |
| Any valid           | CONFIRMED |
