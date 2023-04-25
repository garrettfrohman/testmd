--- 
id: "zimpler" 
title: "Zimpler"
hide_title: "true"
---
 
![](/img/providers/logos/zimpler.png)

# Zimpler

## About
Zimpler is a banking provider that offers deposits and withdrawals.

| Provider Name                | Zimpler                                                                                                                                    |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.zimpler.com/](https://www.zimpler.com/)                                                                                       |
| Classification               | Online Banking                                                                                                                             |
| Regions                      | `Sweden`, `Finland`. `Denmark`, `Germany`, `Netherlands`, `Estonia`, `Latvia`, `Lithuania`, `Peru`                                         |
| Currencies                   | `SEK`, `DKK`, `EUR`, `PEN`                                                                                                                 |
| Methods/PaymentTxTypes       | `ZimplerDeposit` <br/> `ZimplerWithdrawal` <br/> *`BankIBANDeposit`* <br/> `BankIBANWithdrawal` <br/> `BankDeposit` <br/> `BankWithdrawal` |
| PaymentIQ Configuration File | `ZimplerConfig`                                                                                                                            |

## Configuration

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.zimpler.ZimplerConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <version>4</version>
        <siteReference>??</siteReference>
        <merchantName>??</merchantName>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
  </accounts>
  <height>700</height>
  <width>600</width>
</com.devcode.paymentiq.integration.zimpler.ZimplerConfig>
```
</details>

### Attributes

#### Root level
| Attribute                            | Default value                           | Description                                                                                                     |
|--------------------------------------|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| forceContainerForMobile              | `true`                                  | Will set container to window on mobile devices since Zimpler requires that mobile devices don't open in iframe. |
| nationalIdentityNumberPatternMapping | `SE\          | SWE->[0-9]{8}-[0-9]{4}` | Pattern for validation of national identity number. Multiple mappings have to be comma separated.               |

#### Account level
| Attribute                       | Default value | Description                                                                                                                      |
|---------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------|
| merchantId                      |               | Account username at Zimpler                                                                                                      |
| apiKey                          |               | Account password at Zimpler                                                                                                      |
| siteReference                   |               | Domain name of the merchant site                                                                                                 |
| merchantName                    |               | Display name of the merchant site                                                                                                |
| sendNationalIdentityNumber      | `false`       | If national identity number should be sent if provided and valid.                                                                |
| useAccountNumberAsMaskedAccount | `false`       | Optional. If set to true, account number (such as IBAN) will be used as masked account if available                              |
| includeAddressInMaskedAccount   | `false`       | Optional. If set to true, user address data will be included in the masked account if available.                                 |
| useHolderFromResponse           | `false`       | Optional. If set to true, account holder name will be used from Zimpler Approve response for defining user account in PaymentIQ. |

### Transaction types

| Country     | Recommended types                           | Also available types                         |
|-------------|---------------------------------------------|----------------------------------------------|
| Sweden      | `ZimplerDeposit` <br/> `ZimplerWithdrawal`  | `BankIBANDeposit` <br/> `BankIBANWithdrawal` |
| Finland     | `ZimplerDeposit` <br/> `ZimplerWithdrawal`  | `BankIBANDeposit` <br/> `BankIBANWithdrawal` |
| Denmark     | `ZimplerDeposit` <br/> `ZimplerWithdrawal`  |                                              |
| Germany     | `ZimplerDeposit` <br/> `BankIBANWithdrawal` | `BankIBANDeposit`                            |
| Netherlands | `BankIBANWithdrawal`                        |                                              |
| Estonia     | `BankIBANWithdrawal`                        |                                              |
| Latvia      | `BankIBANWithdrawal`                        |                                              |
| Lithuania   | `BankIBANWithdrawal`                        |                                              |
| Peru        | `BankDeposit` <br/> `BankWithdrawal`        |                                              |


:::note

Zimpler only supports passing the `bic` (for bank pre-selection) for `BankIBANDeposit`, so any entered IBAN will have to be re-entered by the user once redirected to Zimpler

:::

## Deposit

A deposit can be initiated with or without a stored account. National identification number or Zimpler's user_id will be included (or not included) subject to the rules described [below](#telling-zimpler-which-user-to-use), but neither are required in order to initiate the deposit.

## Withdrawal

When the withdrawal flow is initiated, Zimpler decides if they need to collect more information from the user and in this case there is a redirect to Zimpler. After the user is finished.
In case no more information is needed, the withdrawal is authorized/denied by Zimpler right away.
Either way, once the flow returns to PaymentIQ, the withdrawal is ready to be approved or denied.

### Without stored account

Zimpler withdrawals for Sweden and Finland require either national identification number or Zimpler user_id to be initiated. If a withdrawal is initiated without a PaymentIQ user account, the national identification number has to be supplied (see [below](#using-national-identification-number)). <br/>For Denmark, instead of national identification number, a login is required after the redirect to Zimpler's UI. For testing purposes, any username can be entered and no password is required.<br/>For other markets no such requirements apply.

### With stored account

When using an existing PaymentIQ user account, national identification number does not have to be supplied. If it is missing, PaymentIQ will send the Zimpler user_id instead.

## Telling Zimpler which user to use

### Using national identification number (Sweden and Finland)

The national identification number is sent to Zimpler if:

1. The attribute "nationalIdentificationNumber" is included in the response to theintegration api `verifyUser` request.
2. The national identification number matches the pattern configured in `nationalIdentityNumberPatternMapping` (see [configuration](#root-level))
2. `sendNationalIdentityNumber` is set to `true` on the account, e.g `<sendNationalIdentityNumber>true</sendNationalIdentityNumber>`.

## Using Zimpler's user_id

Zimpler's user_id is saved in the PaymentIQ user account upon a successful deposit transaction. 
If this user_id is available, it will be sent to Zimpler for every transaction where there is not national identity number sent. See the [section above](#using-national-identification-number) for information on when this happens.

1. If the `sendNationalIdentityNumber` tag is true in ZimplerConfig
2. NationalIdentificationNumber is available (and thus included)
3. Country is available (and thus included)

## Test Information

Minimum amount: 0.30 EUR/3 SEK

### Test accounts

PaymentIQ has two preconfigured test accounts available for use with Zimpler's sandbox platform.

| Account name | Product                      | Identification method         |
|--------------|------------------------------|-------------------------------|
| default      | Wallet (Bank, Invoice, Card) | SE: BankId <br/> FI: Mobile   |
| ZIMPLERBANK  | Bank                         | SE: BankId <br/> FI: Signicat |

###  Test personal identity numbers

| Number        | Country |
|---------------|---------|
| 19810101-0000 | Sweden  |
| 180265-019L   | Finland |

### Test IBAN numbers for Zimpler Bank.

| Test IBAN and BIC                 | Country     |
|-----------------------------------|-------------|
| SWEDSESS SE7580000832799737529546 | Sweden      |
| DEUTDEFF DE89370400440532013000   | Germany     |
| NDEAFIHH FI1410093000123458       | Finland     |
| BNPANL2A NLXXXXXXX                | Netherlands |
| HABAEE2X EEXXXXXXX                | Estonia     |
| LACBLV2X LVXXXXXXX                | Latvia      |
| LIABLT2XMSD LTXXXXXXX             | Lithuania   |

###  Test usernames

| User name               | Country |
|-------------------------|---------|
| Anything can be entered | Denmark |
