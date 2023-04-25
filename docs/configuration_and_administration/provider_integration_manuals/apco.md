--- 
id: "apco" 
title: "APCOPAY"
hide_title: "true"
---
 
![](/img/providers/logos/apco.png)

# APCOPAY

## About
### APCOPAY's FASTPAY
APCO's FastPay hosted payment page provides a secure yet simple means of authorizing credit/debit card transactions, E-wallets and prepaid card schemes from your online portal.

The FastPay system provides a straightforward payment interface for the customer, and handles the complete process for the online transaction including the data collection, encrypted storage of credit/debit card details and the communication process, eliminating the security implications of holding such sensitive information on your own servers.

### DIRECTCONNECT
The Direct Connect API makes it possible to send credit card deposits and withdrawals directly to Apco without going through their hosted payment page. 3DS, refund, void and capture are also supported.

| Provider Name                | Apco                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Links                        | [http://www.apcopay.eu/](http://www.apcopay.eu/)<br/>[Apco back office](https://www.apsp.biz/)                                                                                                                                                                                                                                                                                                                                   |
| Classification               | Aggregator                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                                                                                                                                                  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `ICardWithdrawal`, `ApcoDeposit`, `ApcoWithdrawal`, `IdealDeposit`, `ICardDeposit`, `PaykasaDeposit`, `PayPalDeposit`, `EcoPayzDeposit`, `PayPalWithdrawal`, `SofortDeposit`, `GiropayDeposit`, `SkrillDeposit`, `SkrillWithdrawal`, `VenusPointDeposit`, `VenusPointWithdrawal`, `InovapayWalletDeposit`, `MuchBetterDeposit`, `MuchBetterWithdrawal`, `Refund`, `Void`, `Capture` |
| PaymentIQ Configuration File | `ApcoConfig`                                                                                                                                                                                                                                                                                                                                                                                                                     |

## Configuration Information

You need to contact APCO and order FastPay and Direct-Connect credentials. Also, make sure that you have asked APCO in order to activate the desired payment methods and services.

### Attributes

| Attribute           | Description                                                                                                                                                                                                                                                                                                                                                            |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| profileId           | Corresponds to the Profile ID value received from Apco                                                                                                                                                                                                                                                                                                                 |
| profilePassword     | Corresponds to the hashed secret word received from Apco                                                                                                                                                                                                                                                                                                               |
| username            | Corresponds to the Direct Connect Merchant code value received from Apco                                                                                                                                                                                                                                                                                               |
| password            | Corresponds to the Direct Connect password value received from Apco                                                                                                                                                                                                                                                                                                    |
| forceMid            | Add this tag to the provider account in order to force the gateway routing platform to select the specified merchant account when using IdealDeposit.                                                                                                                                                                                                                  |
| useIcePay           | Enable IcePay as the main acquirer                                                                                                                                                                                                                                                                                                                                     |
| forcePayment        | Force which payment method to be used. Available codes are shown in below tables                                                                                                                                                                                                                                                                                       |
| forceBank           | Add this tag to the provider account in order to send the `ForceBank` parameter to Apco                                                                                                                                                                                                                                                                                |
| skrillMethod        | Add this tag to the provider account in order to send the `ShowSkrillMethod` parameter to Apco with the value of an alternate method. Used when using forcePayment MBKR (Skrill) to process the payment with a specific Skrill method (see available methods [here](/docs/configuration_and_administration/provider_integration_manuals/apco#skrill-payment-methods)). |
| sendName            | Set to false to not send the `<RegName>` parameter to Apco. (Default: true)                                                                                                                                                                                                                                                                                            |
| txHistoryDelayHours | The delay PIQ should find a previous reference transaction, used for example in ICardWithdrawal. Example: `5`. Default is `0` hours.                                                                                                                                                                                                                                   |

You will receive a Profile ID and a hashed secret word in order to have access to their FastPay services.

```xml
<profileId>2234DTGEA3614DA4B8D0EASD9878SAS9A</profileId>
<profilePassword>876asd97as9d</profilePassword>
```

Also, you will need to request a Merchant Code and Password for Direct-Connect service and in order to be able to fetch the status of the transaction.

```xml
<username>82347</username>
<password>fasd6uasdi</password>
```

In PaymentIQ ApcoConfig, you can configure forcing the specific payment method you want by using the tag `<forcePayment>` and using one of the following codes hereunder. By default, it is empty where the end-user will be redirected to APCO main page which will display all available payment methods.

### Credit Card through Fastpay

APMs PurplePay, RaveDirect, Ikajo, Asiapay, and CavPay are used for credit card processing with PaymentIQ's transaction type CreditcardDeposit, then routing to a specific PSP account in the configuration.

| Method                   | Code       |
|--------------------------|------------|
| PurplePay                | PVISA      |
| RaveDirect (Flutterwave) | RAVEDIRECT |
| Ikajo [*]                | IKAJO      |
| CavPay [*][**]           | CAVPAY     |
| Asiapay [*]              | APGDIRECT  |

[\*] Ikajo, CavPay and Asiapay need both forcePayment and forceBank values.

[\*\*] Only deposits are supported for CavPay currently

### Regular Apco Fastpay methods

Following are the current APMs supported in PIQ and that are used with transaction type ApcoDeposit (and ApcoWithdrawal for some), except for some exceptions where it's possible to use the specific transaction types for these methods (noted in the table). See the Front API for more information on these additional transaction types.

| Method             | Code             | Optional transaction type                       |
|--------------------|------------------|-------------------------------------------------|
| Paykasa            | PAYKASA          | PaykasaDeposit                                  |
| Neteller [*]       | NT               | NetellerDeposit, NetellerWithdrawal             |
| Paysafecard        | PAYSAFECARD      | --                                              |
| Eco Card Wallet    | ECOW             | --                                              |
| Ecopayz            | ECOPAYZ          | EcoPayzDeposit                                  |
| PayPal [*]         | PAYPAL           | PayPalDeposit, PayPalWithdrawal                 |
| Icard [*]          | ICARD            | ICardDeposit, ICardWithdrawal                   |
| Sofort             | SOFORT           | SofortDeposit                                   |
| Skrill [*]         | SKRILL           | SkrillDeposit, SkrillWithdrawal                 |
| GiroPay            | GIROPAY          | GiropayDeposit                                  |
| iDeal              | IDEAL            | IdealDeposit                                    |
| Processing.com     | PROCESSINGCOM    | --                                              |
| Elegro             | ELEGROCRYPTO     | CryptoCurrencyDeposit, CryptoCurrencyWithdrawal |
| VenusPoint         | VENUSPOINT       | VenusPointDeposit, VenusPointWithdrawal         |
| Inovapay Gateway   | INOVAPAY         | --                                              |
| Inovapay Wallet    | INOVAPAYWALLET   | InovapayWalletDeposit, InovapayWalletWithdrawal |
| Paydoo             | PAYDOO           | --                                              |
| APG                | APG              | --                                              |
| APG Direct         | APGDIRECT        | --                                              |
| WonderlandPay      | WONDERLANDPAY    | --                                              |
| XPATE              | XPATE            | --                                              |
| Xentum             | XENTUM           | --                                              |
| Straal             | STRAAL           | --                                              |
| Flexepin           | FLEXEPIN         | --                                              |
| Neosurf            | NEOSURF          | NeosurfVoucherWithdrawal                        |
| JNET               | JNET             | --                                              |
| Interac            | INTERAC          | --                                              |
| Interac E-Transfer | INTERACETRANSFER | --                                              |
| MuchBetter [*]     | MUCHBETTER       | MuchBetterDeposit, MuchBetterWithdrawal         |
| Directa24          | DIRECTA24        | AstroPayBankWithdrawal                          |
| Coindirect         | COINDIRECT       | CryptoCurrencyWithdrawal                        |
| PayRetailers       | PAYRETAILERS     | PayRetailersWithdrawal                          |
| JPAY               | JPAY             | --                                              |
| PAY4FUN            | PAY4FUN          | --                                              |

[\*] Note that for withdrawals to work, a previous deposit with the same method has to have been performed to be used as a reference.

#### Additional notes about specific APMs
* **Elegro** - Type CryptoCurrencyWithdrawal is required for Elegro withdrawals since a wallet address is needed as an input parameter. See the front api cryptocurreny section for endpoint and parameters. Also, the amount value may differ from the amount originally requested. Kindly make sure that the amount used is the one sent by PIQ in the transfer request and not the amount sent in the initial request.
* **VenusPoint** - Type VenusPointWithdrawal is required for VenusPoint withdrawals since a username and password is needed as input parameters. See the front api wallet section for endpoint and parameters.
* **Straal** - Has to be opened with container window (not iframe). Set tag `<container>window</container>` on your Straal account inside the `ApcoConfig`.
* **Flexepin** - Since Flexepin uses the full voucher amount of the voucher code entered, the value may differ from the amount originally requested. Kindly make sure that the amount used is the one sent by PIQ in the transfer request and not the amount sent in the initial request.
* **Neosurf** - The Neosurf wallet email when performing payouts is either taken from the merchant user information if you are using `ApcoWithdrawal`, or if you are using `NeosurfVoucherWithdrawal` it is taken from the input parameter `email`. See the front api voucher section for endpoint and parameters.
* **Skrill** - Skrill support the use of additional payment options. This is enabled by adding the `skrillMethod` entry with the specific payment code value to the Skrill account of the ApcoConfig. Example: `<skrillMethod>OBT</skrillMethod>` to enable Rapid Transfer. See the table below for the available methods.
* **Coindirect** - Type CryptoCurrencyWithdrawal is required for Coindirect withdrawals since a wallet address is needed as an input parameter. 
* **Directa24** - Type AstroPayBankWithdrawal is required for Directa24 withdrawals since a document type, document number and others inputs are needed as an input parameters. 
* **PayRetailers** - Type PayRetailersWithdrawal is required for PayRetailers withdrawals since a document type, document number and others inputs are needed as an input parameters. 

### Skrill payment methods

| Method         | Code |
|----------------|------|
| AliPay         | ALI  |
| Przelewy24     | PWY  |
| Trustly        | GLU  |
| Paysafecard    | PSC  |
| Neteller       | NTL  |
| Sofort         | SFT  |
| Rapid Transfer | OBT  |

### Apco ICEPAY methods

ICEPAY is a payment service provider through PSP Apco that provides payment solutions to business of all sizes through its multichannel transaction platform.

| Method          | Code        | Optional transaction type |
|-----------------|-------------|---------------------------|
| Achterafbetalen | ABETALEN    | --                        |
| Paysafecard     | PAYSAFECARD | --                        |
| PayPal          | PAYPAL      | PayPalDeposit             |
| Sofort          | DIRECTEBANK | SofortDeposit             |
| GiroPay         | GIROPAY     | GiropayDeposit            |
| iDeal           | IDEAL       | IdealDeposit              |
| Visa Card       | IVISA       | --                        |
| MasterCard      | IMASTERC    | --                        |
| ELV             | DDEBIT      | --                        |
| Mistercash      | MISTERCASH  | --                        |
| EPS             | EPS         | --                        |

#### Enabling ICEPAY

In order to use IcePay as the MainAcquirer with Apco in PIQ, add the following tag to either the main level or the account config level in the ApcoConfig.

`<useIcePay>true</useIcePay>`

It is disabled by default.

### Using the service parameter
In case you are using the parameter ‘service’ together with the ApcoDeposit method, you may want to enable specific payment methods in PaymentIQ which is a combination of the base method, i.e. ApcoDeposit, together with service parameter e.g. ‘GIROPAY’.

To enable this, a mapping is required in the MerchantConfig.

![](/img/providers/apco02.png)

This will enable a new payment method option in the Payment methods rules.

![](/img/providers/apco03.png)

This will make sure that when you call PaymentIQ to fetch the available payment methods, the Apco method will be present with the parameter 'service' and correct value.

![](/img/providers/apco04.png)

### DirectConnect
To enable DirectConnect set the version either at main level or account level in ApcoConfig as the example below.

`<version>DIRECTCONNECT</version>`

It is possible to force the acquirer on Apco's side by setting the forceBank tag on account config leve. For example:

`<forceBank>PAGOS24</forceBank>`

## Example Routing Rule

### Example of a basic routing rule using the 'ApcoDeposit' method.
![](/img/providers/routing/apco.png)

### Example of a basic routing rule using the 'SofortDeposit' method.
![](/img/providers/routing/apco2.png)

## Test Information

Some payment methods need certain test data to perform tests.

### Icard

| Card number      | Expiry                             | CVV | Description      |
|------------------|------------------------------------|-----|------------------|
| 4444444444444444 | 12/yy where yy is the current year | 444 | CVV   Successful |
| 1111111111111111 | 12/yy where yy is the current year | 444 | Rejected         |
| 4444444444442228 | 12/yy where yy is the current year | 444 | Successful   3DS |

### Processing.com / Paydoo

Once the transaction is initiated and the Apco card frame is displayed, one of the cards below has to be entered:

| Card number      | Expiry              | CVV | Description     |
|------------------|---------------------|-----|-----------------|
| 4444444444444444 | Any (in the future) | 123 | Successful Card |
| 5555555555555555 | Any (in the future) | 123 | Successful Card |

### PayPal

| Email              | Password |
|--------------------|----------|
| apco_test@mail.com | ApcoTest |

### EcoPayz
EcoPayz allows you to pay online in a simple and secure way, just as if you were using ordinary cash. Just purchase a prepaid ecoVoucher PIN and use it to pay online at websites accepting ecoVoucher. You don't need a bank account or credit card, so anyone can use it.

### GiroPay

| BIC         | BIN                    |
|-------------|------------------------|
| GENODETT488 | DE07444488880123456789 |


### Skrill

| Email          | Password   |
|----------------|------------|
| ms@apco.com.mt | Skri11test |


### PurplePay

- Currency: EUR or SEK

| Card Brand | Account          | CVV | Expiry date | Result/Info  |
|------------|------------------|-----|-------------|--------------|
| VISA       | 4012888888881881 | Any | Any         | APPROVED     |
| VISA       | 4242424242424242 | Any | Any         | DECLINED     |
| VISA       | 4900000000000086 | Any | Any         | NOT ENROLLED |
| MASTERCARD | 5500000000000004 | Any | Any         | APPROVED     |
| MASTERCARD | 5200000000000007 | Any | Any         | DECLINED     |
| MASTERCARD | 5200000000000080 | Any | Any         | NOT ENROLLED |
| MAESTRO    | 6799851000000032 | Any | Any         | APPROVED     |
| MAESTRO    | 6759000000000018 | Any | Any         | DECLINED     |
| MAESTRO    | 6759000000000026 | Any | Any         | DECLINED     |

### RaveDirect

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| VISA       | 4242424242424242 | Any | Any         | APPROVED    |
| MASTERCARD | 5438898014560229 | Any | Any         | APPROVED    |

Enter 1234 as PIN when requested.

### APG

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| MASTERCARD | 5111111111111111 | 189 | 12/22       | APPROVED    |

### APG Direct

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| VISA       | 4444444444444444 | 123 | 1/22        | APPROVED    |

### Elegro

Since APCOPAY cannot perform the actual transfers, the merchant needs to contact APCOPAY to manually process test transactions to simulate a complete successful payment

### VenusPoint

- Currency: USD

| Username | Password            |
|----------|---------------------|
| U000073  | UTestAPCOPAY4819$$. |

### Inovapay

- Currency: BRL
- Min amount: 50
- User Country: BRA

Testing Inovapay Gateway with `ApcoDeposit`:
| CPF         |
|-------------|
| 54351436832 |

Testing Inovapay Wallet with `InovapayWalletDeposit` and `InovapayWalletWithdrawal`:
| userlogin | usersecureid |
|-----------|--------------|
| 182895    | 811283       |

### DirectConnect

| Card Number      | CVV | Expiry date | Result/Info |
|------------------|-----|-------------|-------------|
| 4444444444444444 | 444 | 12/yy       | Success     |
| 5555555555555557 | 444 | 12/yy       | Reject      |
| 4444444444442228 | 444 | 12/yy       | 3DS Success |

### IKAJO

| Card Number      | CVV | Expiry date | Result/Info |
|------------------|-----|-------------|-------------|
| 4111111111111111 | 123 | 05/2020     | Confirmed   |
| 4111111111111111 | 123 | 06/2020     | Declined    |

### CavPay

| Card Number      | CVV | Expiry date | Result/Info |
|------------------|-----|-------------|-------------|
| 4242424242424242 | 100 | 12/2025     | Success     |

### Interac / Interac E-Transfer
- Currency: CAD

### Asiapay

| Card Number      | CVV | Expiry date |
|------------------|-----|-------------|
| 4444444444444444 | 123 | 01/2022     |