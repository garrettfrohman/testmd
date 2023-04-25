---
id: "mobilepay"
title: "MobilePay (via a card acquirer)"
hide_title: "true"
---

![](/img/providers/logos/mobilepay.png)

# MobilePay (via a card acquirer)

## About
MobilePay is a mobile wallet solution which securely stores credit cards that can be used for payments through a card acquirer.

| Provider Name                | MobilePay                                                        |
|------------------------------|------------------------------------------------------------------|
| Link                         | [https://www.mobilepay.dk/about](https://www.mobilepay.dk/about) |
| Classification               | Wallet                                                           |
| Regions                      | `Denmark`                                                        |
| Currencies                   | `DKK`                                                            |
| Methods/PaymentTxTypes       | `MobilePayDeposit`                                               |
| PaymentIQ Configuration File | `MobilePayConfig`                                                |

### Additional Links
[Additional information from the provider (in Danish)](https://www.mobilepay.dk/erhverv/abonnementer-og-fakturering/mobilepay-it-integrator)

## Configuration Information
<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.mobilepay.MobilePayConfig>
  <enabled>true</enabled>
  <shopName>Test Shop</shopName>
  <shopUrl>https://www.sunset-boulevard.dk/</shopUrl>
  <shopCountryCode>DK</shopCountryCode>
  <shopLogoUrl>http://www.sunset-boulevard.dk/sb_250.png</shopLogoUrl>
  <shopId>xxxx-xxxxx-xxxxx</shopId>
  <apiVersion>v3</apiVersion>
</com.devcode.paymentiq.integration.mobilepay.MobilePayConfig>
```

</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                                                                                                                |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| shopName                     | Name of the shop/merchant. Visible in MobilePay app.                                                                                                                                                                                                                       |
| shopUrl                      | URL to merchant. Mandatory for v3.                                                                                                                                                                                                                                         |
| shopLogoUrl                  | URL to merchant shop logo. Visible in MobilePay app. The logo must be 250x250 pixel in .png format and the URL must never be changed. If the shop wants a new (or more than one) logo, a new ShopLogoURL must be used. The logo must be hosted on a HTTPS (secure) server. |
| shopCountryCode              | 2 character code, ISO 3166-1 Alpha-2.                                                                                                                                                                                                                                      |
| container                    | Container of redirect page, iframe/window. Defaults to iframe.                                                                                                                                                                                                             |
| width                        | Width of redirect container.                                                                                                                                                                                                                                               |
| height                       | Height of redirect container.                                                                                                                                                                                                                                              |
| usePhoneNumberFromVerifyUser | If set to true, the phone number field in redirect page will be prepoulated with value from verifyUser (can still be changed on the page).                                                                                                                                 |
| acceptedCards                | List of accepted cards. Defaults to accept all cards.                                                                                                                                                                                                                      |
| lightBox                     | Sets the background of the redirect page. Defaults to "0".                                                                                                                                                                                                                 |
| shopId                       | Ask PaymentIQ support to provide shopId.                                                                                                                                                                                                                                   |
| apiVersion                   | Set the version to use. Should be at least "v2". Latest version is v3                                                                                                                                                                                                      |
| checkout                     | Set "true" to use MobilePay checkout feature. Optional                                                                                                                                                                                                                     |
| selectProviderAfterCallback  | Set "true" for provider routing to be done after callback from MobilePay is received. If Dankort should be processed as a regular card this option must not be used or set to false. See details below                                                                     |

### Automatic signup of sub-merchants

Automatic signup of sub-merchants happens when a sub-merchant does their first MobilePay transaction. In order to allow it in PaymentIQ, you will need:

1. Configure **MobilePayMasterConfig** with: `<autoCreateSubMerchants>true</autoCreateSubMerchants>`
2. Include the following attributes in the `MerchantAuthorizeTxRes`:
  * subMerchantId - this id is used to map the sub-merchant to the created MobilePay merchantID
  * subMerchantCountry - must be a valid country
  * subMerchantName
  * merchantMcc - merchant category code (MCC). If it is missing, PaymentIQ will look for `mcc` parameter in merchant's provider account config.<br/>
**Notes:**
    * PaymentIQ will decline payment if MCC is missing (either in the `MerchantAuthorizeTxRes` or in the provider account config);
    * Every unique combination of MID and `subMerchantId` will create a new merchant at MobilePay
3. Make regular `MobilePayDeposit` transactions (needs **MobilePays** test app).<br/>
If a subMerchant is used, the info column is populated with "subMerchantId: {the id}" and if the merchant was created (first time only), info is also populated with "Created new MobilePay merchant".

### Accepted cards
#### Card types
| Card                                                     | Type        |
|----------------------------------------------------------|-------------|
| MasterCard Debit                                         | MC-DEBIT    |
| MasterCard Credit                                        | MC-CREDIT   |
| Maestro Debit                                            | MTRO-DEBIT  |
| VISA Electron Debit                                      | ELEC-DEBIT  |
| VISA Debit (and Visa-Dankort if Dankort is not accepted) | VISA-DEBIT  |
| VISA Credit                                              | VISA-CREDIT |
| Dankort                                                  | DANKORT     |

#### Country codes
| Country                 | Code |
|-------------------------|------|
| All countries           | 10   |
| All countries except DK | 11   |
| All countries except NO | 12   |
| All countries except FI | 13   |
| Denmark                 | DK   |
| Norway                  | NO   |
| Finland                 | FI   |

<details>
<summary>Click to view example</summary>
<br/>

```xml
<acceptedCards>
  <card>
    <type>MC-DEBIT</type>
    <countryCode>10</countryCode>
  </card>
  <card>
    <type>MC-CREDIT</type>
    <countryCode>11</countryCode>
  </card>
</acceptedCards>
```

</details>

### Lightbox
| Background  | Value |
|-------------|-------|
| White       | 0     |
| Dark        | 1     |
| Transparent | 2     |

### Routing based on card type
MobilePay sends the type of the card in the callback to PaymentIQ. To be able to use the card type in routing rules one must first add the following configuration:

`<selectProviderAfterCallback>true</selectProviderAfterCallback>`

And then use the condition "Bin card brand". See example below.

![](/img/providers/routing/mobilepay-dankort.png)

Note: If Dankort be should be processed as a regular card this option must not be used or set to false.

### Process Dankort as regular Visa

If Dankort should processed as a regular Visa card (i.e not through Nets), it needs to be removed from the accepted cards in the MobilePayConfig:
```xml
<acceptedCards>
  <card>
    <type>MC-DEBIT</type>
    <countryCode>10</countryCode>
  </card>
  <card>
    <type>MC-CREDIT</type>
    <countryCode>10</countryCode>
  </card>
  <card>
    <type>MTRO-DEBIT</type>
    <countryCode>10</countryCode>
  </card>
  <card>
    <type>ELEC-DEBIT</type>
    <countryCode>10</countryCode>
  </card>
  <card>
    <type>VISA-DEBIT</type>
    <countryCode>10</countryCode>
  </card>
  <card>
    <type>VISA-CREDIT</type>
    <countryCode>10</countryCode>
  </card>
</acceptedCards>
```

### 3DS Fallback

If the acquirer rejects the authorization with status code ERR_DECLINED_SCA_REQUIRED_BY_ISSUER, the transaction should fallback to do a 3DS authentication and then try again to authorize with the acquirer.

This can be done with the following example fallback rule:
![](/img/providers/mobilepay-3ds-fallback.png)

#### 3DSv1

The provider config's 3DS PSP account must be configured to do 3DS through Ingenico's MPI by adding the following settings:

```xml
<use3Dsecure>true</use3Dsecure>
<mpi>ig</mpi>
<merchantCountry>???</merchantCountry>
<merchantUrl>https://????????</merchantUrl>  
<merchantName>????????</merchantName>
<threeDS2TemplateName>3ds2_force_challenge</threeDS2TemplateName> <!-- Issuer may respond with frictionless unless this is set and this can cause issues-->
```

#### 3DS2

3DS2 routing should be setup the same way as for regular cards transactions.

### Dynamic merchant name and logo

Merchant name and logo URL are usually set by the configs `shopName` and `shopLogoUrl` in MobilePayConfig. They can also be set dynamically per transaction by sending the values as attributes in the merchant authorize response. The attribute names are `subMerchantName` and `subMerchantLogoUrl`. If these attributes are sent for a transaction they will be used instead of the configured values.

## Example Routing Rules

![](/img/providers/routing/mobilepay.png)

## Test Information

MobilePay provides a development app that can be found [here](https://developer.mobilepay.dk/docs/online/development-guide/test#test-app).<br/>
If you have your own test login credentials those can be used. If not, we have a common login that are already configured with test cards that can be used to test different acquirers / 3DS Servers. Keep in mind that this test login is used by many different people, sometimes at the same time, so transactions that you did not initialize might show up. Please do not approve transactions that you did not initialize.

Once in the APP, press "Log on (existing user)" and enter the details below.

| Phone number (DK) | PIN  | Activation code |
|-------------------|------|-----------------|
| +45 60620847      | 1234 | 123456          |

### SSN

| DK CPR      | FI Henkilötunnus  |
|-------------|-------------------|
| 000000-0000 | 00000000000 (11x) |

Note that the PSP (acquirer) response is mocked by default in test mode. Then it doesn't matter what card number is used. Mocked responses will be successful when amount is bigger than 10, otherwise declined. It is also not possible to do only auth when using mocked responses.

To disable mocked PSP responses in test, add the following line to the PSP config (e.g. BamboraGaConfig):
`<mockMobilePayResponse>false</mockMobilePayResponse>`

When testing 3DS2 the response from the 3DS Server is never mocked, which means that a valid test card number for the 3DS Server must be used. See the 3DS2 testing page for more info: [https://docs.paymentiq.io/europe/3ds2/testing/testing3ds2staging](https://docs.paymentiq.io/europe/3ds2/testing/testing3ds2staging)
