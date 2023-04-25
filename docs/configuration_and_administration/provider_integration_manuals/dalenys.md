--- 
id: "dalenys"
title: "Dalenys"
hide_title: "true"
---

![](/img/providers/logos/dalenys.png)

# Dalenys

## About
Dalenys is a credit card provider that supports deposits, captures, withdrawals, refunds and voids.

| Provider Name                | Dalenys                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.dalenys.com/](https://www.dalenys.com/)                                                                                                                                                                                                                                                                                                                                                                                            |
| Classification               | Debit/Credit Card Processor                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Regions                      | `Australia`, `Canada`, `Switzerland`, `Czech Republic`, `Denmark`, `Andorra`, `Austria`, `Belgium`, `Cyprus`, `Estonia`, `Finland`, `France`, `Germany`, `Greece`, `Ireland`, `Italy`, `Latvia`, `Lithuania`, `Luxemburg`, `Malta`, `Monaco`, `Montenegro`, `Netherlands`, `Portugal`, `Slovakia`, `Slovenia`, `Spain`, `UK`, `Hong-Kong`, `Norway`, `New Zealand`, `Poland`, `Romania`, `Sweden`, `Singapore`, `Turkey`, `USA`, `South Africa` |
| Currencies                   | `EUR`, `GBP`, `USD`, `CAD`, `CHF`, `AUD`, `HKD`, `SEK`, `DKK`, `NOK`, `NZD`, `ZAR`, `SGD`, `PLN`, `RON`, `TRL`, `CZK`                                                                                                                                                                                                                                                                                                                           |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `Capture` <br/> `Refund` <br/> `Void`                                                                                                                                                                                                                                                                                                                                                    |
| PaymentIQ Configuration File | `DalenysConfig`                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### Note
Currencies availabilities is subjected to each merchant activity and local regulations.
If the Payment Transaction is processed in a currency not listed onto the aforementioned list of the supported currencies, the Payment Transaction amount will be converted and paid in euros by the card scheme.
For example, if the Payment Transaction is processed in THB,
the Payment Transaction shall be converted and settled by default in EUR.

Before enabling Dalenys as your payment provider, please contact Dalenys tech support to make sure that the country and
the currency is supported for your use case.

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.dalenys.DalenysConfig>
  <testMode>true</testMode>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <use3Dsecure>true</use3Dsecure>
        <defaultDescriptor>DEPOSIT</defaultDescriptor>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <authType>AUTH_CAPTURE</authType>
        <supportedCurrencies>GBP|EUR</supportedCurrencies>
        <mcc>??</mcc>
        <merchantCountry>??</merchantCountry>
        <merchantUrl>??</merchantUrl>
        <merchantName>??</merchantName>
      </account>
    </entry>
    <entry>
      <string>no_auto_capture</string>
      <account>
        <use3Dsecure>true</use3Dsecure>
        <defaultDescriptor>DEPOSIT</defaultDescriptor>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <authType>PRE_AUTH</authType>
        <supportedCurrencies>GBP|EUR</supportedCurrencies>
        <mcc>??</mcc>
        <merchantUrl>??</merchantUrl>
        <merchantCountry>??</merchantCountry>
        <merchantName>??</merchantName>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.dalenys.DalenysConfig>
```

</details>

### Attributes

| Attribute                   | Description                                                                                                                                                                              |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| use3Dsecure                 | Mandatory and should be set to true as Dalenys supports only 3DSecure payments.                                                                                                          |
| defaultDescriptor           | Mandatory. Corresponds to the order description.                                                                                                                                         |
| account.merchantId          | Mandatory. It is an individual merchant id that should be provided by Dalenys.                                                                                                           |
| account.apiKey              | Mandatory. An individual key provided by Dalenys that is used for creating request signatures.                                                                                           |
| account.authType            | This parameter determines whether PaymentIQ should automatically perform a capture request after a successful authorization request. More on that in the 'Direct Capture' section below. |
| account.supportedCurrencies | Mandatory. A list of currencies that are supported for the account in use - it should be confirmed with Dalenys.                                                                         |
| account.mcc                 | Mandatory - a merchant category code used by 3DS servers.                                                                                                                                |
| account.merchantUrl         | The URL that processes on this MID.                                                                                                                                                      |
| account.merchantCountry     | Country that account is bound to. Can be name of the country, 3-alpha CountryCode, 2-alpha CountryCode or 3-digit CountryCode.                                                           |
| account.merchantName        | Merchant name rendered in the payment sheet.                                                                                                                                             |

### Direct Capture
Based on whether the authType parameter is present and its value in the account configuration, PaymentIQ will either 
perform the capture request directly after a successful authorization request or the capture should be performed from 
the PaymentIQ's backoffice.

The capture will be automatically launched after a successful authorization when authType is not present or set to
'AUTH_CAPTURE'.
For the values 'FINAL_AUTH' or 'PRE_AUTH' the capture action should be performed from PaymentIQ's backoffice.

## Provider Configuration

For all the payment methods, please make sure to follow these steps to configure Payper:

1. Run PaymentIQ and add the aforementioned DalenysConfig under Admin -> Configuration.
2. Add Dalenys to the `<psp>` section in MerchantConfig under Admin -> Configuration.
3. Depending on the credit card brands that is intent to be used, enable the following deposit and withdrawal methods
   in Rules -> Payment methods. <br/>
   CREDITCARD-CB <br/>
   CREDITCARD-VISA <br/>
   CREDITCARD-VPAY <br/>
   CREDITCARD-ELECTRON <br/>
   CREDITCARD-MASTERCARD <br/>
   CREDITCARD-MAESTRO <br/>

## Example Routing Rule

![](/img/providers/routing/dalenys.png)

## Transaction Flow

### Deposits
1. The user enters the amount to be deposited along with the credit card number in the cashier and clicks on "deposit".
2. PaymentIQ sends an authorization request to Dalenys API.
3. After a successful response, depending on conditions mentioned in the 'Direct Capture' the transaction is either 
   authorized and should be captured in the PaymentIQ's backoffice if needed or PaymentIQ automatically sends a capture request
   to Dalenys.
4. In case of automatic capture, PaymentIQ receives a response from Dalenys API and updates the transaction status accordingly.

### Withdrawals
Note: withdrawals can only be executed on a successfully captured transaction and at least one successful deposit made
by the user is required in order to proceed with the withdrawal.
1. The user enters the amount to be withdrawn along with the credit card number in the cashier and clicks on "withdraw".
2. After the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to Dalenys and 
   updates the status of the transaction in accordance with the direct response from Dalenys.
   
### Refunds
Note: refunds can only be executed on a successfully captured transaction.
1. A refund is being initiated from the PaymentIQ's backoffice and results in a new transaction.
2. After that PaymentIQ sends a refund request to Dalenys and updates the status of the transaction in accordance
   with the direct response from Dalenys.
   
### Voids
Note: voids can only be performed on a transaction that has not been captured yet.
1. A void is being initiated from the PaymentIQ's backoffice and results in a new transaction.
2. After that PaymentIQ sends a void request to Dalenys and updates the status of the transaction in accordance
   with the direct response from Dalenys.

## Test Information

Please check directly with the provider.