--- 
id: "wirecardelastic" 
title: "Wirecard Elastic"
hide_title: "true"
---
 
![](/img/providers/logos/wirecard.png)

# Wirecard Elastic

## About
Wirecard is a creditcard processor and aggregator with support for Deposits, Refunds, Voids, Captures and Partial Capture.

| Provider Name                | Wirecard Elastic                                                                                                                                                                                                         |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.wirecard.com](https://www.wirecard.com)                                                                                                                                                                     |
| Classification               | Aggregator                                                                                                                                                                                                            |
| Regions                      | International                                                                                                                                                                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                        |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `IdealDeposit`<br/> `SofortDeposit`<br/> `GiropayDeposit`<br/> `BankIBANDeposit`<br/> `BankIBANWithdrawal`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `Reversal` |
| PaymentIQ Configuration File | `WirecardElasticConfig`                                                                                                                                                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.wirecardelastic.WirecardElasticConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>3DS</string>
      <account>
        <merchantId>??</merchantId>
        <!-- <resolverName>??</resolverName> activated by Wirecard to bundle MIDs and can then be used instead of merchantId -->
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>GBP|USD|EUR|SEK</supportedCurrencies> <!-- add/remove depending on Merchant's agreement -->
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>true</useTokenId>
        <authType>AUTH_CAPTURE</authType>
        <merchantCountry>${ptx.merchantUserCountry}</merchantCountry>
      </account>
    </entry>
    
    <entry>
      <string>3DS2</string>
      <account>
        <merchantId>??</merchantId>
        <!-- <resolverName>??</resolverName> activated by Wirecard to bundle MIDs and can then be used instead of merchantId -->
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>GBP|USD|EUR|SEK</supportedCurrencies> <!-- add/remove depending on Merchant's agreement -->
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>true</useTokenId>
        <authType>AUTH_CAPTURE</authType>
        <!-- 3DS2 parameters -->
        <acquirerMerchantId>XXXXXXXX</acquirerMerchantId> <!-- Value received from PSP  -->
        <mcc>7995</mcc> <!-- 7995 for gambling merchants change if this isn't applicable to you -->
        <merchantCountry>XXX</merchantCountry> <!-- Origin country of merchant 3 DIGIT ISO for eaxmple SWE or MLT -->
        <merchantUrl>http://www.example.com</merchantUrl> <!-- URL to your website -->
        <merchantName>XXX</merchantName> <!-- Name of your brand -->
        <!-- End of 3DS2 parameters -->
      </account>
    </entry>
    
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>??</merchantId>
        <!-- <resolverName>??</resolverName> activated by Wirecard to bundle MIDs and can then be used instead of merchantId -->
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>GBP|USD|EUR|SEK</supportedCurrencies> <!-- add/remove depending on Merchant's agreement -->
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
        <authType>AUTH_CAPTURE</authType>
        <merchantCountry>${ptx.merchantUserCountry}</merchantCountry>
      </account>
    </entry>
    
    <entry>
      <string>IDEAL</string>
      <account>
        <merchantId>??</merchantId>
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>EUR</supportedCurrencies>  
        <container>window</container>
      </account>
    </entry>    
    <entry>
      <string>SOFORT</string>
      <account>
        <merchantId>??</merchantId>
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>EUR</supportedCurrencies>  
        <container>window</container>
      </account>
    </entry>    
    <entry>
      <string>SEPA</string>
      <account>
        <merchantId>??</merchantId>
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>EUR</supportedCurrencies>  
        <container>window</container>
        <contractNumber>??</contractNumber>
      </account>
    </entry>
    <entry>
      <string>GIRO</string>
      <account>
        <merchantId>??</merchantId>
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>EUR</supportedCurrencies>  
        <container>window</container>
        <financialInstitutionBic>??</financialInstitutionBic>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.wirecardelastic.WirecardElasticConfig>
```

</details>

### Attributes

| Attribute               | Description                                                                                                                          |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| merchantId              | Merchant ID. Provided by Wirecard (not needed for resolver option)                                                                   |
| resolverName            | in case of using resolver.                                                                                                           |
| username                | Provided by Wirecard                                                                                                                 |
| password                | Endpoint differs between Credit Cards and APMs so needs to be set here for non Credit Cards                                          |
| useTokenId              | Send request using stored token instead of credit card details. Required to skip 3ds for enrolled cards                              |
| authType                | Same as other providers.                                                                                                             |
| use3Dsecure             | Same as other providers.                                                                                                             |
| merchantCountry         | Merchant's Country.                                                                                                                  |
| contractNumber          | Use for SEPA service.                                                                                                                |
| financialInstitutionBic | Is going to be use by GIRO.                                                                                                          |
| refundMerchantId        | Used for BankIBANWithdrawal and Refund of IdealDeposit or BankIBANDeposit. Set to the SEPA Credit transfer MAID provided by Wirecard |
| secretKey               | Used for SEPA and for doing Refund on IdealDeposit. Set to SEPA 'Secret Key' provided by Wirecard                                    |

### Notes
- Wirecard can activate resolver option for a merchant which act like a bundle to pack up all MIDs

## Example Routing Rule

![](/img/providers/routing/WirecardElasticCCrouting.png)

## Test Information

For test information follow the link below:
[https://doc.wirecard.com/PaymentMethods.html](https://doc.wirecard.com/PaymentMethods.html)
