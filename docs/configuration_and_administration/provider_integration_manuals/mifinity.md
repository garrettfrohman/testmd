---
id: "mifinity"
title: "MiFinity"
hide_title: "true"
---

![](/img/providers/logos/mifinity.png)

# MiFinity

## About
MiFinity is a payment provider offering Creditcard withdrawals, Bank Withdrawals as well as an eWallet solution (deposit and withdrawal).

| Provider Name                | MiFinity                                                                                                                                                                                       |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.mifinity.com](https://www.mifinity.com)                                                                                                                                           |
| Classification               | Debit/Credit Card Processor, Online Banking, Wallet                                                                                                                                            |
| Regions                      | `International`                                                                                                                                                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                |
| Methods/PaymentTxTypes       | `CreditcardWithdrawal` <br/> `MiFinityEWalletDeposit` <br/> `MiFinityEWalletWithdrawal` <br/> `BankDomesticWithdrawal` <br/> `BankLocalWithdrawal` <br/> `BankIBANWithdrawal` <br/> `Reversal` |
| PaymentIQ Configuration File | `MiFinityConfig`                                                                                                                                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.mifinity.MiFinityConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy><!--needed for Creditcard transactions -->
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>??</username>
        <password>??</password>
        <accountID>??</accountID>
        <merchantName>??</merchantName>
        <apiKey>??</apiKey>
        <payMyCard>false</payMyCard>
        <sourceAccount>??</sourceAccount>
        <forceCountryCode>FROM_IBAN</forceCountryCode>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>ACC2</string>
      <account>
        <accountID>??</accountID><!--Account Holder Id-->
        <merchantName>??</merchantName>
        <apiKey>??</apiKey>
        <payMyCard>false</payMyCard>
        <sourceAccount>??</sourceAccount>
        <method>TEST_METHOD</method>
        <logoUrl>https://some.location.com/logo.png</logoUrl>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>iframe</container>
  <width>800</width>
  <height>650</height>
  <defaultDescriptor>Operation description goes here</defaultDescriptor>
  <bankMappings>
    <!--Malta-->
    <bankMapping><countryCode>MLT</countryCode><bic>VALLMTMT.*</bic><bankName>Bank of Valletta</bankName><branchCode>Valletta</branchCode></bankMapping>
    <bankMapping><countryCode>MLT</countryCode><bic>MMEBMTMT.*</bic><bankName>HSBC Malta</bankName><branchCode>###</branchCode></bankMapping>

    <!--Mapping for other countries if required-->
	</bankMappings>
  <apiVersion>1</apiVersion>
  <redirectionHtmlTemplateName>mifinity-init-wallet-template</redirectionHtmlTemplateName>
  <defaultBankFieldsMapping>??</defaultBankFieldsMapping>
  <fieldMappings>
    <!--Malta-->
    <com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
      <countryCode>MT|CY</countryCode>
      <currency>EUR</currency>
      <txType>BankIBANWithdrawalInput</txType>
      <bankFields>BANK_NAME->\${bankMapping.bankName}</bankFields>
    </com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>

    <!--Mapping for other countries if required-->
  </fieldMappings>
</com.devcode.paymentiq.integration.mifinity.MiFinityConfig>

```

</details>

### Attributes

| Attribute                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username            | Corresponds to the MiFinity account username that is used to access their back office.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| account.password            | Corresponds to the MiFinity account password that is used to access their back office. It is also used to generate a `validationKey` for eWallet operations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| account.accountID           | Corresponds to the MiFinity **Account Holder Id** that is required to initiate eWallet payment. That parameter can be retrieved from the MiFinity back office.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| account.merchantName        | Corresponds to the client ID that is defined in MiFinity system.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| account.apiKey              | Corresponds to the **API Key** from MiFinity that is used to authenticate requests.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| account.payMyCard           | It is used to enable **Pay My Card** option. By default **Pay Any Card** is enabled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| account.sourceAccount       | It is used to define a MiFinity **Source Account Number** (Account number from which the amount of money will be debited) for PAC, PAB and eWallet withdrawals. For eWallet deposit it is used to define a **Destination Account Number** (Merchant’s account number to collect payment).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| account.forceCountryCode    | It is used to define a strategy to resolve country code that is required to retrieve all required fields in order to make bank payout. Possible values are: `FROM_IBAN`, two letters country code (`IT`), blank or missing.<br/>- `forceCountryCode=FROM_IBAN`: it is useful to make payment in IBAN country (if user is from France (FR) and wants to use his/her Great Britain (GB) IBAN). In that case country code will be retrieved from the provided IBAN. This is useful in case of `BankIBANWithdrawal` tx type.<br/>- `forceCountryCode=IT`: it can be used to force user to make bank payout in any non user country. In that case user will have to provide his/her Italian bank details in order to make a payout.<br/>- blank/missing `forceCountryCode`: bank payout will be made in user's country. |
| account.language            | Optional 2-character string indicating the language in which the eWallet iframe will be initialized. If no `language` parameter is defined in the config, it will be taken from the user context.<br/>Possible values are: `BR`, `CN`, `DE`, `DK`, `EN`, `ES`, `FI`, `FR`, `GR`, `HR`, `IT`, `LA`, `NL`, `PL`, `PT`, `SE`, `RU`, `ZH`.<br/>If not provided, the iFrame is presented in English.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| account.brandId             | 3-digit ID parameter provided by MiFinity which indicates through which brand is the call being made.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| account.method              | eWallet Payment method for the iframe to be initialized with. It can also be specified using `service` parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| account.logoUrl             | Optional parameter, that is used to define a displaying brand logo in the eWallet iframe.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| defaultDescriptor           | It is used to define an operation description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| bankMappings                | Bank mapping configurations that can be used to resolve bank name, code, branch, address, SWIFT, ... based on provided user information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| redirectionHtmlTemplateName | It is used to define MiFinity eWallet initialization HTML template name (see HTML template below).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| defaultBankFieldsMapping    | Default bank fields mapping for payout operations:<br/>`BIC->\${input.bic},IBAN->\${input.iban},ACCOUNT_NUMBER->\${input.accountNumber},BANK_NAME->\${if input.bankName}\${input.bankName}\${else}\${bankMapping.bankName}\${end},CUSTOMER_NAME->\${ptx.merchantUser.name},CUSTOMER_CITY->\${ptx.merchantUser.city},CUSTOMER_ADDRESS->\${ptx.merchantUser.addressAsOneLine},CUSTOMER_ZIP->\${ptx.merchantUser.zip},CUSTOMER_STATE->\${ptx.merchantUser.state(NA)},CUSTOMER_PHONE->\${ptx.merchantUser.mobileDigits},BENEFICIARY_ADDRESS_COUNTRY_ISO_CODE->\${ptx.merchantUser.countryCode.twoAlphaCode},ACCOUNT_TYPE->\${input.accountType},PERSONAL_ID_NUMBER->\${input.nationalId}`.                                                                                                                             |
| fieldMappings               | It is used to specify a transaction type input (`BankDomesticWithdrawalInput`, `BankLocalWithdrawalInput`, `BankIBANWithdrawalInput`) for bank payout operation for a specific country and currency.<br/>There is also a possibility to override a specific bank fields mappings via `bankFields` parameter e.g. `<bankFields>BANK_NAME->\${bankMapping.bankName}</bankFields>`.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| apiVersion                  | It is used to define `x-api-version` request header.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

### Service Endpoints

- TEST: https://demo.mifinity.com
- LIVE: https://secure.mifinity.com

### Login URL for the users upon login to their merchant account
- TEST: https://businessdemo.mifinity.com/
- LIVE: https://business.mifinity.com/

### Authenticate Request

Any request sent to MiFinity should be Authenticated. It can be done by sending token with `authorization` header

```json
“authorization”: “{token}”
```

or ApiKey with - `key` header

```json
“key”: “{apiKey}”.
```

Token can be received by sending POST request to https://demo.mifinity.com/api/oauth/token with Basic "authorization" header.<br/>
ApiKey can be configured for your merchant account at MiFinity back office (see [Login URL for the users upon login to their merchant account](#mifinity-backoffice-urls) above).

### Handle Callback Notifications

Please contact MiFinty and ask them to configure the below URL's for you.

- TEST: https://test-api.paymentiq.io/paymentiq/api/mifinity/callback
- LIVE: https://api.paymentiq.io/paymentiq/api/mifinity/callback

### MiFinity Wallet initialization HTML template

```html
<html>
  <head>
    <meta charset="utf-8" />
    <title>MiFinity</title>
    <style>
      iframe {
        min-height: 97vh !important;
      }
      #widget-container {
        margin: 0;
      }
      #widget-container div {
        height: auto !important;
      }
    </style>
    <script src="${serviceEndpoint}/widgets/sgpg.js?58190a411dc3"></script>
  </head>
  <body>
    <div id="widget-container"></div>
    <script>
      var pegasus_widget = nxsgpgc3("widget-container", {
        accountHolderId: "${accountHolderId}",
        token: "${initializationToken}",
        processors: ["NXAQCR"],
        amount: "${ptx.txAmount.amount}",
        currency: "${ptx.txAmount.currencyCode}",
        description: "Deposit of ${ptx.txAmount.amount} ${ptx.txAmount.currencyCode}",
        merchant: "${accountConfig.merchantName}",
        fail: function () {
          window.location =
            "${baseRedirectUrl}/api/mifinity/deposit/redirect/${ptx.txRefId}/${validationKey}";
        },
        success: function () {
          window.location =
            "${baseRedirectUrl}/api/mifinity/deposit/redirect/${ptx.txRefId}/${validationKey}";
        },
      });

      function setInnerIframeAttrb() {
        var innerIframe = document.querySelector(".__paymentIframe_iframe");
        if (innerIframe) {
          innerIframe.style =
            "border: 3px solid #eee;box-sizing: border-box;width: 1px;min-width: 98vw;";
        } else {
          setTimeout(setInnerIframeAttrb, 500);
        }
      }
      setInnerIframeAttrb();
    </script>
  </body>
</html>
```

### Retrieve all available banks for a specific country and currency

To retrieve available banks the following `GET` request should be executed:

```
https://demo.mifinity.com/api/payer?country={country}&currency={currency}
```

If PaymentIQ Cashier is used, it can be easily configured in the Cashier Payment Method-settings by setting `Input Html Template Name` to `mifinity-banks` (see [Bank Payout Configuration Information](#bank-payout-configuration-information) below).<br/>
Also it is required to define a "default" account in your **MiFinityConfig** as it will be used to make a request to MiFinity and retrieve available banks.

## SEPA Bank Payout Configuration Information

### Andorra, Austria, Belgium, Bulgaria, Croatia (HR/EUR), Cyprus, Czech Republic, Denmark (DK/EUR), Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Italy, Latvia, Liechtenstein, Lithuania, Luxembourg, Malta, Netherlands, Norway, Poland, Portugal, Romania, Slovakia, Slovenia, Sweden (SE/EUR), Switzerland, Spain

It can be used for all countries for which `IBAN` is required only.<br/>

`BankIBANWithdrawalInput` with "service" parameter should be used to handle such operations. In such case `bankBic` parameter is not needed (it can be hidden in PaymentIQ Cashier or sent as blank).

1. **MerchantConfig**: configure a specific service for BANKIBAN provider type e.g. `MIFINITY_BANKDIBAN_SEPA_01`:
```xml
<entry>
  <string>BANKIBAN</string>
  <string>...|MIFINITY_BANKIBAN_SEPA_01</string><!--you can define any name-->
</entry>
```
2. **Rules > Payment Methods**: enable `BANKIBAN-MIFINITY_BANKIBAN_SEPA_01` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--BANKIBAN SEPA-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>AD|AT|BE|BG|HR|CY|CZ|DK|EE|FI|FR|DE|GR|HU|IS|IE|IT|LV|LI|LT|LU|MT|NL|NO|PL|PT|RO|SK|SI|SE|CH|ES</countryCode>
  <currency>EUR|CZK|HUF|NOK|PLN</currency>
  <txType>BankIBANWithdrawalInput</txType>
  <bankFields>CUSTOMER_NAME->\${input.beneficiaryName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod1.png)

### Denmark (DK/DKK), Monaco

It can be used for all countries for which `BIC` and `IBAN` are required.<br/>

`BankIBANWithdrawalInput` with "service" parameter should be used to handle such operations.

1. **MerchantConfig**: configure a specific service for BANKIBAN provider type e.g. `MIFINITY_BANKDIBAN_SEPA_02`:
```xml
<entry>
  <string>BANKIBAN</string>
  <string>...|MIFINITY_BANKIBAN_SEPA_02</string><!--you can define any name-->
</entry>
```
2. **Rules > Payment Methods**: enable `BANKIBAN-MIFINITY_BANKIBAN_SEPA_02` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--BANKIBAN SEPA-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>DK|MC</countryCode>
  <currency>EUR|DKK</currency>
  <txType>BankIBANWithdrawalInput</txType>
  <bankFields>CUSTOMER_NAME->\${input.beneficiaryName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod2.png)

### United Kingdom (GB/EUR)

It can be used for all countries for which `BIC`, `IBAN` and `BANK_NAME` are required.<br/>

`BankIBANWithdrawalInput` with "service" parameter should be used to handle such operations. In such case `bankName` should be configured in the Cashier Payment Method-settings.

1. **MerchantConfig**: configure a specific service for BANKIBAN provider type e.g. `MIFINITY_BANKIBAN_SEPA_03`:
```xml
<entry>
  <string>BANKIBAN</string>
  <string>...|MIFINITY_BANKIBAN_SEPA_03</string><!--you can define any name-->
</entry>
```
2. **Rules > Payment Methods**: enable `BANKIBAN-MIFINITY_BANKIBAN_SEPA_03` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--BANKIBAN SEPA-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>GB</countryCode>
  <currency>EUR</currency>
  <txType>BankIBANWithdrawalInput</txType>
  <bankFields>CUSTOMER_NAME->\${input.beneficiaryName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod3.png)

### Sweden (SE/SEK), United Kingdom (GB/GBP)

It can be used for all countries for which `ACCOUNT_NUMBER`, `BANK_CODE/BANK_SORT_CODE` and `BANK_NAME` are required.<br/>

`BankILocalWithdrawalInput` with "service" parameter should be used to handle such operations. In such case we will use "clearingNumber" field as a `BANK_CODE/BANK_SORT_CODE` and `bankName` should be configured in the Cashier Payment Method-settings.

1. **MerchantConfig**: configure a specific service for BANKLOCAL provider type e.g. `MIFINITY_BANKLOCAL_SEPA`:
```xml
<entry>
  <string>BANKLOCAL</string>
  <string>...|MIFINITY_BANKLOCAL_SEPA</string><!--you can define any name-->
</entry>
```
2. **Rules > Payment Methods**: enable `BANKLOCAL-MIFINITY_BANKLOCAL_SEPA` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--BANKLOCAL SEPA-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>SE|GB</countryCode>
  <currency>SEK|GBP</currency>
  <txType>BankLocalWithdrawalInput</txType>
  <bankFields>BANK_CODE->\${input.clearingNumber}</bankFields>
  <!--<bankFields>BANK_SORT_CODE->\${input.clearingNumber}</bankFields>-->
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod4.png)

## Bank Payout Configuration Information

### Turkey, Pakistan

It can be used for all countries for which `IBAN` and `BANK_NAME` are required.<br/>

`BankIBANWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` should be configured in the Cashier Payment Method-settings and `bankBic` should be hidden.

1. **MerchantConfig**: configure a specific service for BANKIBAN provider type e.g. `MIFINITY_BANKDIBAN`:
```xml
<entry>
  <string>BANKIBAN</string>
  <string>...|MIFINITY_BANKIBAN</string>
</entry>
```
2. **Rules > Payment Methods**: enable `BANKIBAN-MIFINITY_BANKDIBAN` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Turkey-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>TR</countryCode>
  <currency>TRY</currency>
  <txType>BankIBANWithdrawalInput</txType>
  <bankFields>CUSTOMER_NAME->\${input.beneficiaryName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod5.png)

### Canada

It can be used for all countries for which `ACCOUNT_NUMBER`, `BANK_NAME` and `ROUTING_NUMBER` are required.<br/>

`BankLocalWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` should be configured in the Cashier Payment Method-settings and the `clearingNumber` input will be used as ROUTING_NUMBER.

1. **MerchantConfig**: configure a specific service for BANKLOCAL provider type e.g. `MIFINITY_BANKLOCAL`:
```xml
<entry>
  <string>BANKLOCAL</string>
  <string>...|MIFINITY_BANKLOCAL</string>
</entry>
```
2. **Rules > Payment Methods**: enable `BANKLOCAL-MIFINITY_BANKLOCAL` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Canada-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>CA</countryCode>
  <currency>CAD</currency>
  <txType>BankLocalWithdrawalInput</txType>
  <bankFields>ROUTING_NUMBER->\${input.clearingNumber}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod6.png)

### China

It can be used for all countries for which `ACCOUNT_NUMBER`, `BIC`/`SWIFT` and `BANK_NAME` are required.<br/>

`BankLocalWithdrawalInput` can be used to handle such operation:
- `BankLocalWithdrawalInput` with bank mapping can be used. In such case `bankName` should be resolved from bank mapping (defined in the **MiFinityConfig**) and  `input.clearingNumber` field will be used as BIC/SWIFT.
- `BankLocalWithdrawalInput` with "service" parameter can be used. In such case `bankName` should be configured in the Cashier Payment Method-settings and `input.clearingNumber` field will be used as BIC/SWIFT (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKLOCAL provider type e.g. `MIFINITY_BANKLOCAL`:
```xml
<entry>
  <string>BANKLOCAL</string>
  <string>...|MIFINITY_BANKLOCAL</string>
</entry>
```
2. **Rules > Payment Methods**: enable `BANKLOCAL-MIFINITY_BANKLOCAL` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--China-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>CN</countryCode>
  <currency>USD</currency>
  <txType>BankLocalWithdrawalInput</txType>
  <bankFields>BIC->\${input.clearingNumber}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod6.png)

Notes:

- to resolve bank name from bank mapping (defined in the **MiFinityConfig**), please comment both, `<string>bankName</string>` and `<inputHtmlTemplateName>mifinity-banks</inputHtmlTemplateName>`.

### Hong Kong, Indonesia, Kenya, South Korea, Sri Lanka, Malaysia, Nigeria, Nepal, Philippines, Rwanda, Singapore, Thailand, Tanzania, Vietnam, South Africa

It can be used for all countries for which `ACCOUNT_NUMBER` and `BANK_NAME` are required.<br/>

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` should be configured in the Cashier Payment Method-settings.

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKDOMESTIC`:
```xml
<entry>
  <string>BANKDOMESTIC</string>
  <string>MIFINITY_BANKDOMESTIC</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKDOMESTIC` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Thailand-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>TH</countryCode>
  <currency>THB</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields/>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod7.png)

### Japan, Bangladesh

It can be used for all countries for which `ACCOUNT_NUMBER`, `BANK_NAME` and `BRANCH_CODE` are required.<br/>

`BankLocalWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` should be configured in the Cashier Payment Method-settings and `input.clearingNumber` field will be used as BARNCH_CODE.

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` and `branchName` should be configured in the Cashier Payment Method-settings (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKDOMESTIC`:
```xml
<entry>
  <string>BANKDOMESTIC</string>
  <string>...|MIFINITY_BANKDOMESTIC</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKDOMESTIC` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Japan-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>JP</countryCode>
  <currency>JPY</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields>BRANCH_CODE->\${input.branchName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod8.png)

### Australia

It can be used for all countries for which `ACCOUNT_NUMBER`, `BANK_NAME` and `BSB` are required.<br/>

`BankLocalWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` should be configured in the Cashier Payment Method-settings and `input.clearingNumber` field will be used as BSB code.

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` and `branchName` should be configured in the Cashier Payment Method-settings (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKDOMESTIC`:
```xml
<entry>
  <string>BANKDOMESTIC</string>
  <string>...|MIFINITY_BANKDOMESTIC</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKDOMESTIC` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Australia-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>AU</countryCode>
  <currency>AUD</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields>BSB->\${input.branchName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod8.png)

### Peru
Countries for which `BANK_NAME`, `ACCOUNT_NUMBER` and `ACCOUNT_TYPE` are required

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName` and `accountType` should be configured in the Cashier Payment Method-settings (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKLATAM`:
```xml
<entry>
    <string>BANKDOMESTIC</string>
    <string>...|MIFINITY_BANKLATAM</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKLATAM` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Peru-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>PE</countryCode>
  <currency>PEN</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields/>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethodinput1.png)
![](/img/providers/mifinity-paymentmethod9.png)

### Chile

Countries for which `BANK_NAME`, `ACCOUNT_NUMBER`, `ACCOUNT_TYPE` and `PERSONAL_ID_NUMBER` are required.

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName`, `accountType` and `nationalId` should be configured in the Cashier Payment Method-settings (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKLATAM`:
```xml
<entry>
    <string>BANKDOMESTIC</string>
    <string>...|MIFINITY_BANKLATAM</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKLATAM` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Chile-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>CL</countryCode>
  <currency>CLP</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields/>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethodinput2.png)
![](/img/providers/mifinity-paymentmethod10.png)

### Brazil

Countries for which `BANK_NAME`, `BRANCH_CODE`, `ACCOUNT_NUMBER`, `ACCOUNT_TYPE` and `PERSONAL_ID_NUMBER` are required.

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName`, `bankBranchName`, `accountNumber`, `accountType` and `nationalId` should be configured in the Cashier Payment Method-settings (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKLATAM`:
```xml
<entry>
    <string>BANKDOMESTIC</string>
    <string>...|MIFINITY_BANKLATAM</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKLATAM` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Brazil-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>BR</countryCode>
  <currency>BRL</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields>BRANCH_CODE->\${input.branchName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethod11.png)

### Colombia

Countries for which `BANK_NAME`, `ACCOUNT_NUMBER`, `BENEFICIARY_DOCUMENT_TYPE`, `BENEFICIARY_DOCUMENT_NUMBER` and `ACCOUNT_TYPE` are required.

`BankDomesticWithdrawalInput` with "service" parameter can be used to handle such operation. In such case `bankName`, `accountNumber`, `nationalIdType`, `nationalId` and `accountType` should be configured in the Cashier Payment Method-settings (see configuration details below).

1. **MerchantConfig**: configure a specific service for BANKDOMESTIC provider type e.g. `MIFINITY_BANKLATAM`:
```xml
<entry>
    <string>BANKDOMESTIC</string>
    <string>...|MIFINITY_BANKLATAM</string>
 </entry>
```
2. **Rules > Payment Methods**: enable `BANKDOMESTIC-MIFINITY_BANKLATAM` as a withdrawal payment option.
3. **MiFinityConfig**: add MiFinity field mapping:
```xml
<!--Colombia-->
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
  <countryCode>CO</countryCode>
  <currency>COP</currency>
  <txType>BankDomesticWithdrawalInput</txType>
  <bankFields>BENEFICIARY_DOCUMENT_TYPE->\${input.nationalIdType},BENEFICIARY_DOCUMENT_NUMBER->\${input.nationalId},ACCOUNT_TYPE->\${input.accountType}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```
4. Configure the Cashier Payment Method-settings accordingly:

![](/img/providers/mifinity-paymentmethodinput3.png)
![](/img/providers/mifinity-paymentmethod12.png)

### Notes
- To enable available banks dropdown, remove `bankName` as an input to the payment method and add `mifinity-banks` in the `Input Html Template Name` field. It is valid for any country.

## FAQ

### Create new API Key for Merchant

1. Login to MiFinity back office (see [Login URL for the users upon login to their merchant account](#mifinity-backoffice-urls) above) using your DEMO merchant account credentials (e.g. roman.voloshyn@devcode.se)
2. Select an account (e.g. 5001000001021839)
3. Select API Keys and press "Create New API Key"
4. Specify any name for API Key (e.g. ewallet_eur_api_key) and press "Create New API Key"

### What to use API Key or Authorization?

For any of our products .. you can use in the header either Authorisation token or API key ... whilst Authorisation token it make use of username and password - encoded in base64 but it expires every 90 days ... hence merchants must change the password every 90 days.<br/>
If the merchant account is in password expired status no transaction will be processed unless merchant logs in our UI and change the password.<br/>
The only API that you cannot use the API key is when you get the token: https://demo.mifinity.com/oauth/token. There you always need the username and password base64 encoded.<br/>
Response to `../oauth/token` request will contain **accountHoldeId** that will be stored in the system for later usage (**accountHolderId** is required to use API key for wallet deposit).<br/>
We suggest you always use API key as it never expires.<br/>
In PaymentIQ it works in the following way: username and password will be required to execute `../oauth/token` request to get **accountHolderId**. Once it is received (it will happen when user will make first successful payment), PaymentIQ stores it in the system/DB and for all subsequent payments API Key will be used (username and password will not be required).

### Get all Merchant’s accounts

1. call the authentication api
2. get accounts for that merchant by calling api https://demo.mifinity.com/account-holders/{accountHolderId}/accounts.
   accountHolderId you get it from step 1

### Bank Fields Mappings

Bank name is a required parameter for bank operations and it is not always provided in the merchant's request. In such case bank name will be retrieved from the preconfigured bank fields mappings. To allow it, it must be configured in the MiFinityConfig e.g.

`<defaultBankFieldsMapping>BANK_NAME->${bankMapping.bankName},...</defaultBankFieldsMapping>`

or in the field mapping section for a specific country:

```xml
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
    <countryCode>XX</countryCode>
    <currency>ZZZ</currency>
    <txType>BankIBANWithdrawalInput</txType>
    <bankFields>BANK_NAME->${bankMapping.bankName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```

If bank name is present in the merchant's request, we will use that bank name to send in the payment request to MiFinity. In such case you should have

`<defaultBankFieldsMapping>BANK_NAME->${input.bankName},...</defaultBankFieldsMapping>`

or

```xml
<com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
    <countryCode>XX</countryCode>
    <currency>ZZZ</currency>
    <txType>BankIBANWithdrawalInput</txType>
    <bankFields>BANK_NAME->${input.bankName}</bankFields>
</com.devcode.paymentiq.integration.mifinity.MiFinityFieldMapping>
```

in your MiFinityConfig.<br/>
You can also have a default setting

`<defaultBankFieldsMapping>BANK_NAME->${bankMapping.bankName},...</defaultBankFieldsMapping>`

and just redefine a bank name for a specific country.

## Transaction flow: E-Wallet

### Withdrawal

- To do a withdrawal please specify amount and account from [Testing Information](#testing-information) section.
  NOTE: as account you can specify either Destination Account Number or Email Address

### Deposit

1. Specify amount and initiate the deposit. Then press login

   ![](/img/providers/mifinity01.png)

2. You will need a client account to make payment. Please note it is another account than is configured in the MiFinityConfig. <br/>
For testing purposes you can create your own or use our test client account. <br/>
You can create a new TEST client account here: [https://businessdemo.mifinity.com/auth/signup](https://businessdemo.mifinity.com/auth/signup).

#### Payment IQ test client account

| Login              | Password           |
|--------------------|--------------------|
| payment@devcode.se | piqTestClient2o23! |

3. Enter credentials and login for appropriate client account.

   ![](/img/providers/mifinity02.png)

4. Enter [credit card info](#e-wallet-deposit-card-info) in loaded iframe and press "Pay"

   ![](/img/providers/mifinity03.png)

5. Verify payment

   ![](/img/providers/mifinity04.png)

## Example Routing Rule

![](/img/providers/routing/mifinity.png)

## Test Information

### CreditCard

- Only withdrawal is supported.
- Set “useViqProxy=true” in **MiFinityConfig** only for credit card payments.

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| VISA       | 4207327228854659 | 123 | 12/22       |             |

### Bank

- Only withdrawal to bank account is supported.

#### BankIBANWithdrawal

| BIC         | IBAN                            |
|-------------|---------------------------------|
| VALLMTMT    | MT90VALL22013000000040022530424 |
| BCYPCY2N    | CY17002001280000001200527600    |
| RABONL2UXXX | NL75RABO0315142490              |

### E-Wallet

- The following operations are possible: deposit & withdrawal.

#### E-Wallet Deposit Card Info

- Player name should be “Roman Voloshyn” in MockMerchantConfig if you are using Merchant ABC test account.

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4207327228854659 | 123 | 12/2022     |
| MC         | 5223450000000007 | 090 | 12/2025     |

#### E-Wallet Withdrawal account

| Account          |
|------------------|
| 5001000001033008 |
