--- 
id: "adyen" 
title: "Adyen"
hide_title: "true"
---
 
![](/img/providers/logos/adyen.png)

# Adyen

## About
Adyen is a global payment company that allows businesses to accept e-commerce, mobile, and point-of-sale payments.

| Provider Name                | Adyen                                                                                                                                                                                                                                                                                                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.adyen.com/](https://www.adyen.com/)                                                                                                                                                                                                                                                                                                                        |
| Classification               | Aggregator                                                                                                                                                                                                                                                                                                                                                              |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                         |
| Currencies                   | `SEK`, `EUR`                                                                                                                                                                                                                                                                                                                                                            |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `IdealDeposit`<br/> `SofortDeposit`<br/> `EpsDeposit`<br/> `BankDeposit`<br/> `BankLocalWithdrawal`*<br/> `BankIBANWIthdrawal`**<br/> `TrustlyDeposit`<br/> `PaysafecardDeposit`<br/> `GiropayDeposit`<br/> `SwishDeposit`<br/> `ApplePayDeposit`<br/> `GooglePayDeposit` |
| PaymentIQ Configuration File | `AdyenConfig`                                                                                                                                                                                                                                                                                                                                                           |

\* BankLocalWithdrawal is available in USA  
\** BankIBANWIthdrawal is available for [selected SEPA countries](https://docs.adyen.com/online-payments/online-payouts#supported-countries)

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.adyen.AdyenConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <liveServiceEndPoint>https://[random]-[company name]-checkout-live.adyenpayments.com/checkout/v64</liveServiceEndPoint>
  <paymentsEndpoint>https://[random]-[company name]-pal-live.adyenpayments.com/pal/servlet/Payment/v64</paymentsEndpoint>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <useHosted>false</useHosted>
        <merchantId>???</merchantId> <!-- merchantAccount -->
        <secretKey>???</secretKey> <!-- HMAC key for callback notifications -->
        <apiKey>???</apiKey>
        <!-- Only needed for BankLocalWithdrawal and BankIBANWIthdrawal -->
        <!--<storePayoutApiKey>???</storePayoutApiKey>
        <reviewPayoutApiKey>???</reviewPayoutApiKey>-->
      </account>
    </entry>
    <entry>
      <string>creditcard</string>
      <account>
        <useHosted>false</useHosted>
        <merchantId>???</merchantId> <!-- merchantAccount -->
        <secretKey>???</secretKey> <!-- HMAC key for callback notifications -->
        <apiKey>???</apiKey>
        <!-- <supportedCurrencies>USD|EUR</supportedCurrencies> -->
        <!-- <useTokenId>true</useTokenId> -->
        <!-- <use3Dsecure>true</use3Dsecure> -->
        <!--Options: AUTH_CAPTURE/FINAL_AUTH/PRE_AUTH-->
        <authType>AUTH_CAPTURE</authType>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.adyen.AdyenConfig>
```
</details>

### Checkout API
#### Attributes
| PaymentIQ Configuration | Provider Credential                                                                                                             |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| merchantId              | merchantAccount                                                                                                                 |
| useHosted               | Set this variable to false to use the new checkout API                                                                          |
| apiKey                  | Generated in Adyen Backoffice. Used in requests to Adyen                                                                        |
| secretKey               | Generated in Adyen Backoffice. Used by Adyen to sign callbacks                                                                  |
| storePayoutApiKey       | Generated in Adyen Backoffice. Used by Adyen to submit bank payouts                                                             |
| reviewPayoutApiKey      | Generated in Adyen Backoffice. Used by Adyen to confirm or decline bank payouts                                                 |
| routingFlag             | Optional. Set to the value that should be sent as the `customRoutingFlag` parameter to Adyen. Can only be used on account level |
| waitForCallback         | Optional. Set to true if PIQ should wait for the callback from Adyen before sending the transfer request to the merchant        |
| liveServiceEndPoint     | Provided in Adyen Backoffice.*                                                                                                  |
|                         | https://[random]-[company name]-checkout-live.adyenpayments.com/checkout/v64                                                    |
| paymentsEndpoint        | Provided in Adyen Backoffice.*                                                                                                  |
|                         | https://[random]-[company name]-pal-live.adyenpayments.com/pal/servlet/Payment/v64                                              |

\* In production, each company account is provided with a unique hostname to communicate with Adyen's APIs, these must be configured in PIQ. To get your live endpoints, log in to your live Customer Area and go to Account > API URLs.



#### Adyen configurations
##### Setup notifications
Merchant needs to set up the notification URLs to PIQ in the Adyen Customer Area. Follow these steps once logged in:

1. Go to your Customer Area > Account >  Server communication.
2. Next to Standard Notification, click Add.
3. Enter the notification URL. Depends on environment. See below.
4. Make sure "Method" is set to JSON.
5. Make sure that the "Active" checkbox is checked.
6. Under "Additional Settings", click "Generate new HMAC key". Copy the key and paste it to the secretKey variable in your PIQ AdyenConfig.
7. Click "Save Configuration".

| Environment | Notification URL                                           |
|-------------|------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/adyen/callback |
| PROD        | https://api.paymentiq.io/paymentiq/api/adyen/callback      |

##### Create API Key/storePayoutApiKey/reviewPayoutApiKey
1. Go to your Customer Area > Account > API credentials.
2. Click the user for the specific key, for example  ws@Company.[YourCompanyAccount] for API key.
3. Under Authentication, click "Generate New API Key".
4. Copy the key and paste it to the apiKey/storePayoutApiKey/reviewPayoutApiKey variable in your PIQ AdyenConfig.
5. Click "Save" at the bottom of the page.

##### For Creditcard payments
- Contact Adyen tech support and request that sending raw card data is enabled.  
- To be able to use CreditcardWithdrawal, the merchant needs to contact Adyen support and request the enabling of "instant card payouts". This involves an approval process by the underwriter team at Adyen.  
- Make sure the setting "Capture Delay" is set to "manual" in Adyen Customer Area so that the configuration of FINAL_AUTH/AUTH_CAPTURE can be handled in PIQ instead.

### Legacy API, "Hosted Payment Page"
#### Attributes
| PaymentIQ Configuration | Provider Credential     |
|-------------------------|-------------------------|
| merchantId              | merchantAccount         |
| projectId               | skinCode                |
| username                | Username for basic auth |
| password                | Password for basic auth |
| secretKey               | signature/secret        |

#### The information below shows how to configure the Adyen integration in Adyen Backoffice.

##### Adyen sites:
TEST: [https://ca-test.adyen.com/ca/ca/login.shtml](https://ca-test.adyen.com/ca/ca/login.shtml)

PROD: [https://ca-live.adyen.com/ca/ca/login.shtml](https://ca-live.adyen.com/ca/ca/login.shtml)

##### Notification URLs
Merchant needs to set-up the notification URLs to PIQ in the Adyen Customer Area (links above under "Adyen sites"). Follow these steps once logged in:

1. Go to your Customer Area > Account >  Server communication.
2. Next to Standard Notification, click Add.
3. Under Transport, enter your server's:
    * URL
    * SSL Version
    * Communication Method (JSON).
4. Click Save Configuration.

| Environment | Notification URL                                                   |
|-------------|--------------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/adyen/deposit/callback |
| PROD        | https://api.paymentiq.io/paymentiq/api/adyen/deposit/callback      |

##### Skins
Skins are used by client to display payment options to end-user, and should be created by merchant. Each skin has a Skin Code that needs to be added in AdyenConfig as projectId and it's Valid Account added as merchantId.
![](/img/providers/adyen01.png)

### Issuer IDs
For some payment methods it is required to send an issuer id parameter and for some it's optional to skip the selection in the redirect page. The issuerId parameter is taken from the input's service parameter. See the default mapping in the table below.

| Method | Mapping keys                                                                                                                                                                                |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| IDEAL  | ABN_AMRO, ASN, ING, FREISLAND, RABOBANK, SNS, SNS_REGIO, TRIODOS, VAN_LANSCHOT, KNAB, BUNQ, MONEYOU                                                                                         |
| EPS    | DOLOMITENBANK, RAIFFEISSEN_BANKENGRUPPE, HYPO_TIROL_BANK, SPARDA_BANK_WIEN, SCHOELLERBANK, VOLKSBANK, IMMO_BANK, BANK_AUSTRIA, EASYBANK, VR_BANKBRAUNAU, VOLKSKREDITBANK, ERSTE_BANK, BAWAG |

## Example Routing Rule
![](/img/providers/routing/adyen.png)

## Test Information
The user must have the correct country code set depending on what payment method is used.

| Method | Supported country codes            |
|--------|------------------------------------|
| Ideal  | NL                                 |
| Sofort | AT, BE, CH, DE, ES, GB, IT, NL, PL |

Please use the following link for information regarding Adyen test cards:

[https://docs.adyen.com/development-resources/test-cards/test-card-numbers](https://docs.adyen.com/development-resources/test-cards/test-card-numbers)
