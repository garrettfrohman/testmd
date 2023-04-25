--- 
id: "payop" 
title: "Payop"
hide_title: "true"
---
 
![](/img/providers/logos/payop.png)

# Payop

## About
Payop is a provider that offers credit card deposits, refunds, withdrawal, as well as APM deposits.

APMs currently supported in PaymentIQ: VOLT

| Provider Name                | Payop                                                                                      |
|------------------------------|--------------------------------------------------------------------------------------------|
| Link                         | [https://payop.com/en](https://payop.com/en)                                               |
| Classification               | Debit/Credit Card and APM Processor                                                        |
| Regions                      | International                                                                              |
| Currencies                   | `USD`, `EUR`, `RUB`                                                                        |
| Limits                       | Deposit - 0.1 USD; Withdrawal - 10 USD                                                     |
|                              | Deposit - 0.1 EUR; Withdrawal - 10 EUR                                                     |
|                              | Deposit - 0.1 RUB; Withdrawal - 10 USD (equivalent sum in RUB)                             |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `BankDeposit`, `Refund`, `CreditcardWithdrawal`, `WebRedirectDeposit` |
| PaymentIQ Configuration File | `PayopConfig`                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payop.PayopConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEPOSIT</string>
      <account>
        <pspPublicKey>??</pspPublicKey>
        <secretKey>??</secretKey>
        <accessToken>??</accessToken>
        <productId>1</productId><!-- "-1" if not specified -->
        <productName>test name</productName><!-- "none" if not specified -->
        <method>381</method><!-- 381 - International Cards, 480 - Local UA cards, 481 - Local RU cards -->
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>WITHDRAWAL</string>
      <account>
        <pspPublicKey>??</pspPublicKey>
        <secretKey>??</secretKey>
        <accessToken>??</accessToken>
        <method>2</method><!-- 2 - International Cards; 3 - Visa/MasterCard (UA cards); 4 - Visa/MasterCard (RU cards) -->
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
        <signingCertificate>??</signingCertificate>
        <commissionType>1</commissionType><!-- 1 - take commission from wallet; 2 - take commission from money (for withdrawal only) -->
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <redirectMaxWaitInSeconds>5</redirectMaxWaitInSeconds>
  <defaultDescriptor>Bambora payment</defaultDescriptor>
</com.devcode.paymentiq.integration.payop.PayopConfig>
```
</details>

### Attributes

| Attribute          | Description                                                                                                                                                                                                                                                                             |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| pspPublicKey       | Corresponds to Public Key from Payop. It is used as a "publicKey" parameter in "create invoice" request                                                                                                                                                                                 |
| secretKey          | Corresponds to Secret Key from Payop. It is used to create a signature                                                                                                                                                                                                                  |
| accessToken        | JWT token that can be received from Payop back office. It is used to authorize each request to Payop                                                                                                                                                                                    |
| method             | Method identifier deciding which payment method to process, e.g 381 for International cards. See supported methods in the table below.                                                                                                                                                  |
| signingCertificate | HEX string, received after converting certificate file **x25519.pub** to byte array and then to Hex string (see below how to convert it). **x25519.pub** is used to encrypt/decrypt a WITHDRAWAL request. Certificate file **x25519.pub** can be downloaded from the Payop back office. |

### Supported methods

| Identifier | Name/Type                     | Payment method       |
|------------|-------------------------------|----------------------|
| 381        | International Cards           | CreditcardDeposit    |
| 480        | Local UA Cards                | CreditcardDeposit    |
| 481        | Local RU Cards                | CreditcardDeposit    |
| 2          | International Cards           | CreditcardWithdrawal |
| 3          | Visa/MasterCard (UA cards)    | CreditcardWithdrawal |
| 4          | Visa/MasterCard (RU cards)    | CreditcardWithdrawal |
| 2801       | VOLT                          | BankDeposit          |
| 200007     | Neosurf Canada                | WebRedirectDeposit   |
| 200008     | Neosurf Europe                | WebRedirectDeposit   |
| 200009     | Neosurf Australia             | WebRedirectDeposit   |
| 200010     | Neosurf                       | WebRedirectDeposit   |
| 1101       | Pagaqui                       | WebRedirectDeposit   |
| 1104       | ABANCA                        | WebRedirectDeposit   |
| 3803       | German Banks                  | BankDeposit          |
| 3804       | Italian Banks                 | BankDeposit          |
| 13020      | PayDo Trustly Netherlands     | BankDeposit          |
| 13019      | PayDo Trustly Poland          | BankDeposit          |
| 13017      | PayDo Trustly Slovakia        | BankDeposit          |
| 13013      | PayDo Trustly Czech           | BankDeposit          |
| 13012      | PayDo Trustly Spain           | BankDeposit          |
| 13011      | PayDo Trustly Germany         | BankDeposit          |
| 13010      | PayDo Trustly Austria         | BankDeposit          |
| 13009      | PayDo Trustly Denmark         | BankDeposit          |
| 13008      | PayDo Trustly Norway          | BankDeposit          |
| 13003      | PayDo Trustly Finland         | BankDeposit          |
| 13002      | PayDo Trustly Sweden          | BankDeposit          |
| 13005      | PayDo Trustly DACH Country's  | BankDeposit          |
| 13006      | PayDo Trustly Eastern Europa  | BankDeposit          |
| 13007      | PayDo Trustly Southern Europe | BankDeposit          |
| 13101      | PayDo iDEAL (Netherlands)     | BankDeposit          |
| 717381     | PayDo cards                   | WebRedirectDeposit   |
| 717001     | PayDo cards                   | WebRedirectDeposit   |
| 717382     | PayDo cards (no VISA)         | WebRedirectDeposit   |

### Convert x25519.pub to HEX String

Please use below terminal command to convert certificate file **x25519.pub** to HEX string:
```
cat file "/{path to file}/x25519.pub" | xxd -pp -g0 -c 64
```

### Callback URL

The callback URL for PaymentIQ Production is: https://api.paymentiq.io/paymentiq/api/payop/callback
The callback URL for PaymentIQ Test is: https://test-api.paymentiq.io/paymentiq/api/payop/callback

### Country whitelisting

In order to make a credit card payment, the user's country should be whitelisted at Payop side and card BIN should be from the whitelisted country (card BIN should match user's IP). In other case transaction will be blocked.

#### List of blocked countries

`Algeria`, `Angola`, `Benin`, `Botswana`, `Burkina Faso`, `Burundi`, `Gabon`, `Gambia`, `Ghana`, `Guinea`, `Guinea-Bissau`, `Congo`, `Democratic Republic of the, Djibouti`, `Egypt`, `Zambia`, `Zimbabwe`, `Cape Verde`, `Cameroon`, `Kenya`, `Comoros`, `Congo`, `Cote dIvoire`, `Lesotho`, `Liberia`, `Libyan Arab Jamahiriya`, `Mauritius`, `Mauritania`, `Madagascar`, `Malawi`, `Mali`, `Morocco`, `Mozambique`, `Namibia`, `Niger`, `Nigeria`, `Rwanda`, `Sao Tome and Principe`, `Swaziland`, `Seychelles`, `Senegal`, `Somalia`, `Sudan`, `Sierra Leone`, `Tanzania`, `United Republic Of Togo`, `Tunisia`, `Uganda`, `Central African Republic`, `Chad`, `Equatorial Guinea`, `Eritrea`, `Ethiopia`, `South Africa`, `South Sudan`, `Argentina`, `Belize`, `Bolivia`, `Brazil`, `Chile`, `Colombia`, `Costa Rica`, `Cuba`, `Dominican Republic`, `Ecuador`, `El Salvador`, `Guatemala`, `Haiti`, `Honduras`, `Mexico`, `Nicaragua`, `Panama`, `Paraguay`, `Peru`, `Uruguay`, `Venezuela`, `United States`, `Canada`, `Japan`, `Turkey`.


## Example Routing Rule

![](/img/providers/routing/payop.png)

## Test Information

NOTE: Payop doesn't have a test environment
