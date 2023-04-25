--- 
id: "inpay" 
title: "InPay"
hide_title: "true"
---
 
![](/img/providers/logos/inpay.png)

# InPay

## About
The InPay Merchant Account gives you access to perform local and international Bank withdrawals and Community Bank deposit and withdrawal (both local and international).

| Provider Name                | InPay                                                                           |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.inpay.com/](https://www.inpay.com/)                                |
| Classification               | Online and Community Banking                                                    |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | See [v1-2](#inpay-v1-2) or [v3](#inpay-v3)                                      |
| PaymentIQ Configuration File | `InPayConfig`                                                                   |

## InPay v1-2
### PaymentTxTypes
`CommunityBankDeposit`, `BankIntlWithdrawal`, `BankLocalWithdrawal`

### Configuration Information

#### Attributes

| Attribute               | Description                                                                                                                                                                                                                                                                                             |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId              | Merchant id from InPay                                                                                                                                                                                                                                                                                  |
| secretKey               | Secret key provided by InPay                                                                                                                                                                                                                                                                            |
| version                 | The version of the api that we use. (Default is v1). Set v2 to use the new API for support for AUS.                                                                                                                                                                                                     |
| projectId               | Provided by InPay. Is called processor id in InPay                                                                                                                                                                                                                                                      |
| production              | If validation should be skipped                                                                                                                                                                                                                                                                         |
| bankMapping             | Used for mapping a clearing number or account number to bank information.                                                                                                                                                                                                                               |
| bankName                | Bank of provider (Default: YES BANK)                                                                                                                                                                                                                                                                    |
| bankCode                | Suggested bank code that can be used (if configured) for community bank deposit. Configured bank will be shown first on the UI list.                                                                                                                                                                    |
| minAmount               | It is used for community bank deposit to show amounts bigger then `minAmount` on UI                                                                                                                                                                                                                     |
| maxAmount               | It is used for community bank deposit to show amounts lower then `maxAmount` on UI                                                                                                                                                                                                                      |
| purposeCode             | PC01 - Credit to Non-resident (External) Rupee accounts maintained by Non-resident Indians in Indian Rupees, PC02 - Payments to families of Non-resident Indians, PC06 - Payments of tuition / boarding, examination fee etc. to schools, colleges and other educational institutions (Default is PC01) |
| remitterType            | 1/0. Set 1 the Remitter is Individual, set 0 if the Remitter is Corporate (Default is 1)                                                                                                                                                                                                                |
| sendCountryCodeFromIban | If true and withdrawal to IBAN, country (as sent to InPay) will be determined by IBAN number instead of by verifyUser                                                                                                                                                                                   |
| signingCertificate      | Required to use the Community Payments API                                                                                                                                                                                                                                                              |
| apiToken                | Required to use the Community Payments API, received along with the signing certificate                                                                                                                                                                                                                 |
| forceCountryCode        | If using html template to generate available banks dropdown, you can use this field to force filtering of the banks to the country set here. Use two letter country code format.                                                                                                                        |

#### Example
```xml
<com.devcode.paymentiq.integration.inpay.InPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>TRY</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <!--<bankCode>??</bankCode>-->
        <serviceEndpoint>https://test-admin.inpay.com/api</serviceEndpoint>
        <supportedCurrencies>TRY</supportedCurrencies>
        <version>v2</version>
      </account>
    </entry>
    <entry>
      <string>NOK</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <!--<bankCode>??</bankCode>-->
        <serviceEndpoint>https://test-admin.inpay.com/api</serviceEndpoint>
        <supportedCurrencies>NOK</supportedCurrencies>
        <version>v2</version>
        <!--<minAmount>120</minAmount>-->
        <!--<maxAmount>150</maxAmount>-->
      </account>
    </entry>
    <entry>
      <string>INR</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <serviceEndpoint>https://test-admin.inpay.com/api</serviceEndpoint>
        <supportedCurrencies>INR</supportedCurrencies>
        <version>v2</version>
      </account>
    </entry>
    <entry>
      <string>AUD</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <supportedCurrencies>AUD</supportedCurrencies>
        <version>v2</version>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora payment</defaultDescriptor>
  <bankMappings>
    <!-- Turkey-->
    <bankMapping><countryCode>TUR</countryCode><clearingNumber>TGBATRIS.*</clearingNumber><bankName>TURKIYE GARANTI BANKASI A.S.</bankName></bankMapping>
  </bankMappings>
</com.devcode.paymentiq.integration.inpay.InPayConfig>
```

#### BankIntlWithdrawal
See BankIntlWithdrawal in the front api.

BankIntlWithdrawal should mainly be used for SEPA payouts with currency EUR, but please see notes below for exceptions.

The mandatory parameters with PaymentIQs BankIntlWithdrawal type for regular SEPA with Inpay are `accountNumber` (beneficiaries IBAN) and `bic` (beneficiaries SWIFT/BIC).

Notes for Inpay version 2 accounts using BankIntlWithdrawal:
- For CA country, the user should insert the clearing number (which also called as BSB or branch code) with the account number. This means that the account number field will consist of both of clearing number combined with the account number.
- For AU country, the user should specify swift (`clearingNumber` field), account number (`accountNumber` field) and local branch code (BSB code) (`branchName` field).
- Parameter `branchAddress` is mandatory.
- Parameter `bankName` is mandatory

#### BankLocalWithdrawal
See BankLocalWithdrawal in the front api bank section.

BankLocalWithdrawal should mainly be used for payouts in local currency, with exceptions in notes below. Please see [Inpay's documentation](https://documentation.inpay.com/payout-local/) for the supported countries for which BankLocalWithdrawal should be used.

The mandatory parameters with PaymentIQs BankLocalWithdrawal type for local payouts are `clearingNumber` and `accountNumber`. Depending on the country and Inpay account version, PaymentIQ performs an internal mapping to populate the correct values in the request to Inpay. If it seems like this mapping does not work for a certain country, you can add them under the "bank mappings" tab. Read more about it [here](/docs/configuration_and_administration/system_configuration/bank-mapping )

Notes for Inpay version 2 accounts using BankLocalWithdrawal:
- The BankLocalWithdrawal also works for international bank withdrawals with help of specific configuration of bank mappings in PaymentIQ back office.
- BankLocalWithdrawal allows using Inpay V2 for the following country codes (NO, AU, TR, SE, PL, RO, CA, IN, JP, ZA, BR) with their local currencies.
- Since Inpay doesn’t support local payout for Canada, CA country transactions using BankLocalWithdrawal will be submitted as an international transaction using the bank mappings in PaymentIQ.

#### AUS Withdrawals
For AUS withdrawals a version 2 account with Inpay is needed. Please get more information about it with your account manager at InPay.

#### IND Withdrawals
For IND withdrawals, a version 2 account with Inpay is needed. Please get more information about it with your account manager at InPay.

For IND withdrawals the following attributes can be configured in InPayConfig (if default values is not wanted)
* remitterType (default 1)
* purposeCode (default PC01).

The default values can be overriden on a account level in InPayConfig. See [Attributes](#attributes)

#### JPY Local Withdrawals
Bank code and branch code of the receiving bank account must be submitted through the clearingNumber input field in the format `{bankCode}{branchCode}` where bankCode is 4 digits and branchCode is 3 digits.

JPY Local Withdrawals can be routed to the v2 account on production. No bank mapping is needed but please note that State, Zip and City is needed from the Verify User response from the Merchant Operator Platform.

#### ZAR Local Withdrawals
Account number and local branch code should be submitted in the accountNumber and clearingNumber field respectively with TxType BankLocalWithdrawal.

#### BRL Local Withdrawals
Bank code and branch code should be submitted in the clearingNumber input field in format `{bankCode}{branchCode}` where bankCode is the first three digits and branchCode the rest.

The end-user's National ID number must be included. This value should be sent as the `nationalId` parameter in the BankLocalWithdrawal request, or be provided in the merchant verifyuser response as attribute `nationalIdentificationNumber`.

#### InPay Backoffice

Merchant summary
This view will be shown for when going to the merchant summary.
Here you can see/edit details for you merchant.

![](/img/providers/inpay01.png)

**Notifications**
This is the view for notifications. Here you can see all notifications. Here you can configure email notification or server to server notifications.

![](/img/providers/inpay02.png)

Click 'Add notifications'

![](/img/providers/inpay04.png)

This is the add notifications view.
- Select postback notifications.
- For postback here you can enter the url that you want the notification to be sent to.
- And then select for what events that you want notifications for.
- For CommunityPayments, the notification url has to be set separately

**Base Notification URL**

| TEST | https://test-api.paymentiq.io/paymentiq/api/inpay/callback |
|------|------------------------------------------------------------|
| PROD | https://api.paymentiq.io/paymentiq/api/inpay/callback      |


**Community Payments Notification URL**

| TEST | https://test-api.paymentiq.io/paymentiq/api/communitypayments/callback |
|------|------------------------------------------------------------------------|
| PROD | https://api.paymentiq.io/paymentiq/api/communitypayments/callback      |


## Community Payments

Community Payments is a separate API provided by InPay. To get access to it, you will need a special certificate. This can be obtained by sending to InPay a CSR which PaymentIQ will provide to you.

### Configuration template

#### Attributes

| Attribute          | Description                                                                                                                                                                                                                   |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| signingCertificate | Required to use the Community Payments API                                                                                                                                                                                    |
| apiToken           | Required to use the Community Payments API, received along with the signing certificate                                                                                                                                       |
| fallbackAction     | What action to take on an expired withdrawal. Set to "FALLBACK" to fallback the withdrawal to InPay v3 withdrawal. Alternatively set to "RETURN" (default value) in order to return the withdrawal to merchant on expiration. |

#### Example
```xml
<com.devcode.paymentiq.integration.inpay.InPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>Default</string>
      <account>
          <signingCertificate>-----BEGIN CERTIFICATE-----
              ??
              ??
              ??
              -----END CERTIFICATE-----
          </signingCertificate>
          <fallbackAction>FALLBACK</fallbackAction>
          <apiToken>??</apiToken>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.inpay.InPayConfig>
```

#### Community Payments Withdrawal

Depending on the country, different input is required from the user:

Australia (might not be supported by InPay, please check with them before using): Amount, Account number, bank code, bank branch code (BSB)

India: Amount, Account number, bank code, beneficiary name, bank branch code (BSB)

Norway (might not be supported by InPay, please check with them before using): Amount, Account number, bank code, beneficiary name

Turkey: Amount, Account number, bank code, beneficiary name

Brazil (might not be supported by InPay, please check with them before using): Amount, Account number, bank code, beneficiary name, bank branch code, social security number, account type

The following bank SWIFT/BIC codes can be used to make Community Payments transactions (please check with InPay if it is up to date bank list):

**Turkey**\
`AKBKTRIS`, `DENITRIS`, `TGBATRIS`, `TRHBTR2A`, `INGBTRIS`, `ISBKTRIS`, `KTEFTRIS`, `FNNBTRIS`, `TEBUTRIS`, `TVBATR2A`, `YAPITRIS`, `TCZBTR2A`

**Norway** (might not be supported by InPay, please check with them before using)\
`DNBANOKK`, `NDEANOKK`, `SPRONO22`, `SHEDNO22`, `SPTRNO22`, `SNOWNO22`, `NORVNO21`, `SGFSNO21`, `SBAKNOBB`

**India**\
`ALLAINBB`, `AUBANKXX`, `AXISINBB`, `BKIDINBB`, `MAHBINBB`, `CNRBINBB`, `CBININBB`, `FDRLINBB`, `HDFCINBB`, `ICICINBB`, `PSIBINBB`, `RATNINBB`, `SBININBB`, `SURY0BK0`, `UCBAINBB`, `YESBINBB`

**Australia** (might not be supported by InPay, please check with them before using)\
`ANZBAU3M`, `QBANAU4B`, `BENDAU3B`, `CTBAAU2S`, `IMTIAU21`, `NATAAU33`, `METWAU4B`, `WPACAU2S`

**Brazil** (might not be supported by InPay, please check with them before using)\
`BRASBRRJ`, `BBDEBRSP`, `CEFXBRSP`, `ITAUBRSP`, `BSCHBRSP`

Alternatively, a html template("inpay-communitypayments-select-bank") can be used to dynamically generate the bank dropdown. To set up a template go to Admin > Cashier > Payment Methods and Inputs > Find the payment method "CommunityBankWithdrawal" > Use the field "Input Html Template Name".

In order for it to work, a default account (an account in your InPayConfig named "default") needs to be set-up with community payments credentials.

#### Community Payments Deposit

Please note that to perform a deposit, first there have to be active withdrawals in the queue.

To trigger a Community Payments deposit you will have to select `Communitybank` payment option

![](/img/providers/inpay_cb_deposit_01.png)

After specifying amount (suggested amount) and pressing "Deposit" you will be redirected to the bank selection page where each bank will list available amounts for collection

![](/img/providers/inpay_cb_deposit_02.png)

Please select preferred bank (e.g. Garanti)

![](/img/providers/inpay_cb_deposit_03.png)

and then amount to be collected.  You will be redirected to the bank login page.

![](/img/providers/inpay_cb_deposit_04.png)

After specifying login details you will be prompted that payment processing will take some time

![](/img/providers/inpay_cb_deposit_05.png)

Then you will have to enter a code received via SMS to complete payment

![](/img/providers/inpay_cb_deposit_06.png)

Once payment is completed, you will see a confirmation page

![](/img/providers/inpay_cb_deposit_07.png)

NOTE: in order to return back to the merchant site you will have to press "Back to Merchant" button. Redirection can happen automatically if it is enabled at InPay side

### Fallbacks

Every withdrawal has an expiration date. Upon expiration, InPay CommunityPayments needs to know what to do with that withdrawal.
Currently, there are 2 options:
1. Let the withdrawal expire, returning it to the merchant. This is the default behaviour.
2. Try the same withdrawal, but using InPay v3 withdrawal, not CommunityPayments withdrawal. This happens if you have set "FALLBACK" in your account config.

For InPay CommunityPayments to know which action to take, you will have to provide them a URL in order for them to get this information from our API.

**Community Payments Handle Expiration URL**

| TEST | https://test-api.paymentiq.io/paymentiq/api/inpay/communitypayments/handleExpiration |
|------|--------------------------------------------------------------------------------------|
| PROD | https://api.paymentiq.io/paymentiq/api/inpay/communitypayments/handleExpiration      |

For fallbacks to work, one must configure the account for both CommunityPayments and InPay v3 (check the following chapter, InPay v3).

Currently, the fallback integration has been done only with India and Brazil transactions in mind.

### Example Routing Rule
![](/img/providers/routing/inpay.png)

#### Local JPY Example
![](/img/providers/routing/inpay-jpy.png)

## InPay v3
### PaymentTxTypes
`BankIBANWithdrawal`, `BankIntlWithdrawal`, `BankLocalWithdrawal`, `PixWithdrawal`

### Configuration Information
#### Attributes (v3)
| Attribute    | Description                                                                                                                                                                                                                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountID    | Account id from InPay. Required.                                                                                                                                                                                                                                                                        |
| apiToken     | Authorization token provided by InPay. Required.                                                                                                                                                                                                                                                        |
| accessToken  | X-Auth-Uuid provided by InPay. Required.                                                                                                                                                                                                                                                                |
| merchantName | Organization name. Required.                                                                                                                                                                                                                                                                            |
| groupId      | Business unit from InPay. Optional.                                                                                                                                                                                                                                                                     |
| method       | Instrument Mapping (`LOCAL`, `INTERNATIONAL`, `SEPA` or `INSTANT SEPA`)                                                                                                                                                                                                                                 |
| purposeCode  | PC01 - Credit to Non-resident (External) Rupee accounts maintained by Non-resident Indians in Indian Rupees, PC02 - Payments to families of Non-resident Indians, PC06 - Payments of tuition / boarding, examination fee etc. to schools, colleges and other educational institutions (Default is PC01) |
| remitterType | Set the Remitter as `private` or as `organization` (Default is `private`)                                                                                                                                                                                                                               |

#### Example
```xml
<com.devcode.paymentiq.integration.inpay.InPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>IBAN</string>
      <account>
        <merchantName>??</merchantName>  
        <accountID>??</accountID>
        <groupId>??</groupId>  
        <apiToken>??</apiToken>
        <accessToken>??</accessToken>
        <!--  <method>BE-BANKIBAN->INSTANT SEPA</method>  -->
        <serviceEndpoint>https://test-admin.inpay.com/api</serviceEndpoint>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>IND</string>
      <account>
        <merchantName>??</merchantName>
        <accountID>??</accountID>
        <apiToken>??</apiToken>
        <accessToken>??</accessToken>
        <serviceEndpoint>https://test-admin.inpay.com/api</serviceEndpoint>
        <supportedCurrencies>INR|EUR</supportedCurrencies>
        <purposeCode>PC01</purposeCode>
      </account>
    </entry>
  </accounts>
  <!--  <method>*-BANKIBAN->SEPA</method> -->
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora payment</defaultDescriptor>
</com.devcode.paymentiq.integration.inpay.InPayConfig>
```
### Payment methods

To specify which country should use `LOCAL`, `PIX`, `INTERNATIONAL`, `SEPA` or `INSTANT SEPA` - use `<method>` attribute.

Default mapping:
`PIX->PIX,GBP_BANKLOCAL->LOCAL CLEARING CODE,BANKLOCAL->LOCAL,BANKINTL->INTERNATIONAL,THB_BANKINTL|PHP_BANKINTL|RSD_BANKINTL->LOCAL,BANKIBAN->SEPA,GBP_BANKIBAN|TRY_BANKIBAN|NOK_BANKIBAN|PLN_BANKIBAN|HUF_BANKIBAN|RON_BANKIBAN|CZK_BANKIBAN|BGN_BANKIBAN->LOCAL,AL_BANKIBAN|AZ_BANKIBAN|BY_BANKIBAN|BA_BANKIBAN|BR_BANKIBAN|CR_BANKIBAN|DO_BANKIBAN|GT_BANKIBAN|IL_BANKIBAN|KZ_BANKIBAN|KW_BANKIBAN|MR_BANKIBAN|MU_BANKIBAN|LC_BANKIBAN|ST_BANKIBAN|RS_BANKIBAN|SC_BANKIBAN|TL_BANKIBAN|VG_BANKIBAN->INTERNATIONAL`


#### BankIBANWithdrawal
See BankIBANWithdrawal in the front api.

BankIntlWithdrawal should mainly be used for `SEPA` or `INSTANT SEPA` payouts with currency EUR, but please see notes below for exceptions. Please see [Inpay's documentation](https://test-api.inpay.com/documentation/disbursement/corridors) for the supported countries for which BankIBANWithdrawal should be used.

Notes for InPay version 3 accounts using BankIBANWithdrawal:
- Can be used for `LOCAL` payouts with currency TRY, GBP, NOK, PLN, HUF, RON, CZK and BGN;
- Can be used for `INTERNATIONAL` payouts with currency EUR for countries: AL, AZ, BY, BA, BR, CR, DO, GT, IL, KZ, KW, MR, MU, LC, ST, RS, SC, TL, VG;

#### BankIntlWithdrawal
See BankIntlWithdrawal in the front api.

BankIntlWithdrawal should mainly be used for `INTERNATIONAL` payouts with currency EUR.

Notes for InPay version 3 accounts using BankIntlWithdrawal:
- Can be used for `LOCAL` payouts with currency THB, PHP, RSD.

#### BankLocalWithdrawal
See BankLocalWithdrawal in the front api bank section.

BankLocalWithdrawal should mainly be used for LOCAL payouts with local currency. Please see [Inpay's documentation](https://test-api.inpay.com/documentation/disbursement/corridors) for the supported countries for which BankLocalWithdrawal should be used.

The mandatory parameters with PaymentIQs BankLocalWithdrawal type for local payouts are `clearingNumber` and `accountNumber`. Depending on the country and Inpay account version, PaymentIQ performs an internal mapping to populate the correct values in the request to Inpay. If it seems like this mapping does not work for a certain country, you can add them under the "bank mappings" tab. Read more about it [here](/docs/configuration_and_administration/system_configuration/bank-mapping )

For IND withdrawals the following attributes can be configured in InPayConfig (if default values is not wanted)
* remitterType (default private)
* purposeCode (default PC02).

The default values can be overriden on a account level in InPayConfig. See [Attributes](#attributes-v3)

#### PixWithdrawal
Under Admin->Cashier->Payment Methods and Input you will find PixWithdrawal payment methods with INPAY service. If you need to reconfigure it please contact PaymentIQ technical support.
Please add INPAY service under PIX entry in MerchantConfig:

```xml
<serviceMapping>
    <entry>
        <string>PIX</string>
        <string>INPAY</string>
    </entry>
</serviceMapping>
```

Pix withdrawal should mainly be used for `PIX` payouts with currency BRL.

Much like the PIX payout solution, Inpay will request the end-user if there are any missing parameters. However, to better streamline the payment flow it's recommended to make sure to provide all of the needed data from the beginning. The most important being the PersonalID (CPF/RUT). To make sure that PIQ can send this value directly to Inpay, you as a merchant has to make sure to provide this value as an `attribute` in the verifyuser response of the Integration API.

The attribute value needs to be sent with the parameter `nationalIdentificationNumber` as in the example below (shortened to save space).

```json
{
  "success": true,
  "userId": "user_123",
  "firstName": "John",
  "lastName": "Doe",
  ...
  "attributes": {
    "nationalIdentificationNumber": "86758181650"
  },
  ...
}
```

### Example Routing Rule
![](/img/providers/routing/inpay-v3.png)

![](/img/providers/routing/inpay-v3-iban.png)

### Configuration at provider side

Please ask InPay to configure "callback" URL

#### Callback URL
| Environment | URL                                                           |
|-------------|---------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/v3/inpay/callback |
| PROD        | https://api.paymentiq.io/paymentiq/api/v3/inpay/callback      |

## Test Information

### Test accounts

- Note: To get the final state (refunded for withdrawals) of the transactions.\
Please send an email to technicalsupport@inpay.com with the invoice reference (psp ref id).

### BankLocalWithdrawal

| Clearing number | Account number |
|-----------------|----------------|
| 5255123         | 1234565        |

### BankIntlWithdrawal
BIC: DABADKKK\
IBAN: DE44500105175407324931\
Bank name: Danske Bank\
Bank address: Store Kongensgade 40, 1264, Copenhagen, Denmark

For more information regarding community payments please check this [link](https://documentation.inpay.com/community-payment/?token=de63ff33846b68cb#11---testing-credentials)
