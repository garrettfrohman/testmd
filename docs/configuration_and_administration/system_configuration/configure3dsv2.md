---
id: "configure3dsv2"
---

# Configure 3DS2

To enable 3DS2 these steps will need to be done in PaymentIQ

:::warning
Please make sure that your developer team have made the required IntegrationAPI and FrontAPI changes before proceeding
:::

1. Add Routing for 3DS2 under **Rules > Routing > 3DS2 Provider**
2. Set up the required Data on the Provider Accounts that should be used for 3DS2
3. If a custom DecisionTableConfig is used, add 3DS2 data.
4. Some providers require specific additional configuration.


## 1 - Adding 3DS2 routing

The routing for 3DS 2 is configured in a separate section under **Rules > Routing > 3DS2 Provider**.

If there is no matching routing for a transaction, it will fall back to become a 3DS 1 transaction.

![](/img/3dsv2/3ds2routing.png)

## 2 - Configuring Provider Accounts

For all Provider Accounts that should run with 3DS2 some additional fields are needed.


```xml

<acquirerMerchantId>${ptx.txAmount.currencyCode;map(AUD->11111111,EUR->22222222,SEK->33333333)}</acquirerMerchantId> 
<mcc>7995</mcc> 
<merchantCountry>SWE</merchantCountry>
<merchantUrl>http://www.example.com</merchantUrl>
<merchantName>Test merchant</merchantName>

```

These additional fields need to be added to an existing provider `<account>` within a providerConfig. The fields that are not mentioned above are specific to the provider:

```xml
<accounts>
   <entry>
      <string>3DS</string>
      <account>
         <merchantId>??</merchantId>
         <accountID>??</accountID>
         <secretKey>??</secretKey>
         <deviceCategory>0</deviceCategory>
         <useTokenId>false</useTokenId>
         <use3Dsecure>true</use3Dsecure>
         <!-- 3DS2 mapping -->
         <acquirerMerchantId>123456</acquirerMerchantId>
         <mcc>7995</mcc>
         <merchantCountry>MLT</merchantCountry>
         <merchantUrl>http://www.MerchantURL.com</merchantUrl>
         <merchantName>MerchantName</merchantName>
         <threeDSRequestorName>Name</threeDSRequestorName>
         <merchantThreeDSRequestorId>Merchant3DSRequestorID</merchantThreeDSRequestorId>
         <!-- End of 3DS2 mapping -->
      </account>
   </entry>
</accounts>
```

## Attributes

| Attribute                  | Description                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| acquirerMerchantId         | Acquirer-assigned Merchant identifier. This may be the same value that is used in authorisation requests sent on behalf of the 3DS Requestor and is represented in ISO 8583 formatting requirements. Please note as per the example that Merchants have the options to specify different acquirerMerchantId on different currencies.                                                                       |
| merchantId                 | Alias for acquirerMerchantId used for some providers. If set `acquirerMerchantId` is optional                                                                                                                                                                                                                                                                                                              |
| mcc                        | The merchants category code. MCC 7995 is for Betting/Online Gaming.                                                                                                                                                                                                                                                                                                                                        |
| merchantCode               | Alias for mcc used for some providers. If set `mcc` is optional.                                                                                                                                                                                                                                                                                                                                           |
| merchantCountry            | Country Code of the Merchant. This value correlates to the Merchant Country Code as defined by each Payment System or DS. <br/><br/>**Length: 3 characters**<br/><br/>**ISO 3166-1 numeric three-digit country code**                                                                                                                                                                                      |
| merchantUrl                | Fully qualified URL of 3DS Requestor website or customer care site. <br/> This data element provides additional information to the receiving 3-D Secure system if a problem arises and should provide contact information. <br/><br/>**Length: Variable, maximum 2048 characters** <br/> <br/>**Value accepted:** <br/>**Fully qualified URL** <br/>**For example:** <br/>**http://server.domainname.com** |
| merchantName               | Merchant name assigned by the Acquirer or Payment System.                                                                                                                                                                                                                                                                                                                                                  |
| challengeWindowSize        | Optional parameter to specify challengeWindowSize. See 'Verify User Parameters Full Set' for available options. If it is not specified here or via Verify User it will default to option 04.                                                                                                                                                                                                               |
| threeDSRequestorName       | Optional parameter. If not added it will default to MerchantName.                                                                                                                                                                                                                                                                                                                                          |
| merchantThreeDSRequestorId | Optional parameter. If not added then the system generates an ID.                                                                                                                                                                                                                                                                                                                                          |

## 3 - Updating DecisionTableConfig

Most Merchants will not use a custom DecisionTableConfig file, but it needs to be updated for 3DS2 for those that do.

Please contact our Technical Support to assist with this.

## 4 - Provider Specific Configuration

### Payvision

The merchant should contact Payvision and request the SchemeId’s that relate to the merchants Payvision memberId. The memberID is a Payvision ID and can be used to link to several scheme MIDs based on a number of conditions. Ensure that Payvision specify what conditions link the memberId to the SchemeIds. As an example, this could be based on currency, like;
- AUD: 750xxx01
- CAD: 750xxx02
- EUR: 750xxx03
- GBP: 750xxx04

Mapping for these values should then be added to the Payvision config in the PSP account that you'll use for 3DS2 transactions, as in this example;

```xml
<!-- 3DS2 mapping -->
    <acquirerMerchantId>${ptx.txAmount.currencyCode;map(AUD->750xxx01,EUR->75xxx03,CAD->750xxx02,GBP->750xxx04)}</acquirerMerchantId>  <!-- Might be simple, can be complex like here -->
    <mcc>7995</mcc> <!-- the MCC code, 7995 for gambling -->
    <merchantCountry>MLT</merchantCountry> . <!-- The registered country of the processing entity (merchant) -->
    <merchantUrl>http://www.yourbrand.com</merchantUrl> . <!-- The URL that processes on this MID -->
    <merchantName>MerchantName</merchantName>
    <threeDSRequestorName>The actual name that Payvision use for the merchant</threeDSRequestorName> .    <!-- This could be ContractualEntity Ltd.  etc. -->
    <merchantThreeDSRequestorId>VISA->10066528*${ptx.txAmount.currencyCode;map(AUD->AUD->750xxx01,EUR->75xxx03,CAD->750xxx02,GBP->750xxx04)},MASTERCARD->${ptx.txAmount.currencyCode;map(AUD->750xxx01,EUR->75xxx03,CAD->750xxx02,GBP->750xxx04)}</merchantThreeDSRequestorId> .   <!-- Might be simple, can be complex like here -->
<!-- End of 3DS2 mapping -->
```

### Worldpay

The merchant should contact Worldpay and request the acquirer MerchantID values for their processing currencies that relate to the merchants Worldpay merchantCode (from the WorldpayConfig). You must also request that Worldpay enable the third party MPI for the merchantCodes. There will be different acquirer MerchantID values for each processing currency. For example;
- SEK: 1845xxxx
- EUR: 1853xxxx
- CAD: 1853xxxx
- USD: 1853xxxx
- GBP: 1853xxxx

Mapping for these values should then be added to the 3DS2 config, as in this example;

```xml
<!-- 3DS2 mapping -->
    <acquirerMerchantId>${ptx.txAmount.currencyCode;map(SEK->1845xxxx,EUR->1853xxxx,CAD->1853xxxx,GBP->1853xxxx,USD->1853xxxx)}</acquirerMerchantId>    <!-- Might be simple, can be complex like here -->
    <mcc>7995</mcc> <!-- the MCC code, 7995 for gambling -->
    <merchantCountry>MLT</merchantCountry> . <!-- The registered country of the processing entity (merchant) -->
    <merchantUrl>http://www.yourbrand.com</merchantUrl> . <!-- The URL that processes on this MID -->
    <merchantName>MerchantName</merchantName>
    <threeDSRequestorName>The actual name that Worldpay use for the merchant</threeDSRequestorName> .    <!-- This could be ContractualEntity Ltd.  etc. -->
<!-- End of 3DS2 mapping -->
```

## Attribute Inheritance

Please note that whilst these attributes can be specified as above, they can also be provided in several different ways. The priority they are picked up in is:

1. Via VerifyUser (Integration API) as outlined in that documentation.
2. Via Authorize (Integration API)
   ```
   Example format:
   
   "subMerchantId" 
   "merchantMcc"
   "subMerchantCountry"
   "subMerchantName"
   "subMerchantURL"
   "subMerchantThreeDSRequestorId"
   "subMerchantThreeDSRequestorName"
   ```
3. Via the Provider Configuration file (see example in the above section)
