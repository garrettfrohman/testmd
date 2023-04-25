--- 
id: "pmi" 
title: "PMI"
hide_title: "true"
---
 
![](/img/providers/logos/pmi.png)

# PMI

## About
PMI is a payment provider offering credit card deposit, online and direct bank deposit, cash deposit and status check.<br/>

| Provider Name                | PMI                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------|
| Link                         | [https://www.tadapayments.com/](https://www.tadapayments.com/)                                    |
| Classification               | Aggregator of different payment options: Debit/Credit Card Processor, Online/Manual Banking, Cash |
| Regions                      | Brazil, Chile, Colombia, Ecuador, Mexico, Peru, Salvador                                          |
| Currencies                   | `USD`, `BRL`, `CLP`, `COP`, `MEX`, `PEN`, `SVC`                                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`BankDeposit`<br/>`PmiCashDeposit`<br/>`WebRedirectDeposit`               |
| PaymentIQ Configuration File | `PmiConfig`                                                                                       |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pmi.PmiConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>M#########</merchantId>
        <merchantName>Bambora Test</merchantName>
        <apiKey>??</apiKey>
        <productId>1234</productId>
        <defaultDescriptor>Test Product</defaultDescriptor>
        <transactionChannel>1</transactionChannel><!--Channel to be paid for (1 => Online, 2 => Cash)-->
        <shopName>Test Shop</shopName><!--Required for MXN cash payment only-->
        <sendEmail>false<sendEmail>
        <!--<forceCountryCode>MEX</forceCountryCode>--><!--PER|MEX-->
        <supportedCurrencies>BRL|PEN|MXN|USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>iframe</container>
</com.devcode.paymentiq.integration.pmi.PmiConfig>
```
</details>

### Attributes

| Attribute                  | Description                                                                                                                                                 |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId         | Corresponds to the unique identifier of the merchant.                                                                                                       |
| account.merchantName       | Corresponds to the merchant name from PMI. Required for `cash` and `online banking` operations.                                                             |
| account.apiKey             | Corresponds to the unique token api of the trade.                                                                                                           |
| account.productId          | Corresponds to the unique identifier of the product.                                                                                                        |
| account.defaultDescriptor  | Corresponds to the product description.                                                                                                                     |
| account.transactionChannel | Corresponds to the channel to be paid for (1 => Online, 2 => Cash). Required for `direct banking` and `get banks` operations.                               |
| account.shopName           | Corresponds to the store name from PMI. Required for `create reference` and `generate reference` operations.                                                |
| account.forceCountry       | It is used to specify country in which payment should be made. It is useful in case user is from one country and payment should be made in another country. |
| account.sendEmail          | It is used to identify if a ticket is generated and sent to the customer's email.                                                                           |

### Notes
- PMI collects payments in local currencies (see supported currencies above) and settles in USD or EUR
- All transactions have a payment deadline, which is 3 days. When the 3 days (4313 minutes) have passed, PaymentIQ can clean such tx if a corresponding job is configured.
- notification URL can only be configured by the provider. Notifications are sent only for paid transactions. Declined or failed transactions are expired in 3 days

TEST: https://test-api.paymentiq.io/paymentiq/api/pmi/callback<br/>
PROD: https://api.paymentiq.io/paymentiq/api/pmi/callback

- PMI will provide all required information (in the table above) to the merchant directly.

### Service Mapping

| PaymentIQ Tx Type  | PSP Service    | Comment                         |
|--------------------|----------------|---------------------------------|
| CreditcardDepost   |                |                                 |
| PmiCashDeposit     |                | non MEX cash payment            |
| BankDeposit        | ONLINE_BANKING | non MEX online banking payments |
| BankDeposit        | DIRECT_BANKING | non MEX direct banking payments |
| WebRedirectDeposit | CASH_REDIRECT  | MEX cash payment                |
| WebRedirectDeposit | SPEI           | MEX bank payment                |

## Example Routing Rule
![](/img/providers/routing/pmi.png)

## Retrieve Available Banks

To retrieve available banks (in case merchant doesn't use PaymentIQ Cashier) you will need to use below `GET` API. \
Please also note, that you will need to have an account with name `default` in your **PmiConfig** in order to use below API. Note, you can have multiple accounts in your config, but `default` account is a must.

TEST: https://test-api.paymentiq.io/paymentiq/api/pmi/banks/{countryCode}?merchantId=${merchantId}<br/>
PROD: https://api.paymentiq.io/paymentiq/api/pmi/banks/{countryCode}?merchantId=${merchantId}

where

`countryCode` - is a 3-letters country code,
`merchantId` - PaymentIQ merchant ID.

## Test Information

### Test Cards

| Card Number      | Expiry Date | CVV |
|------------------|-------------|-----|
| 6371373500000087 | Any         | Any |
| 4915667419153137 | Any         | Any |
| 5221300103137945 | Any         | Any |
| 4027665302766648 | Any         | Any |

### National ID

CPF (for individuals): 11-digit number in the format 000.000.000-00 (26658083827) \
CNPJ (for companies): consists of a 14-digit number formatted as XX.XXX.XXX/0001-XX (28693915000149)
