--- 
id: "dimoco" 
title: "Dimoco"
hide_title: "true"
---
 
![](/img/providers/logos/dimoco.png)

# Dimoco

## About
Dimoco is a revolutionary mobile payments gateway service. Dimoco enables businesses to receive payments from their customers via mobile money.

| Provider Name                | Dimoco                                   |
|------------------------------|------------------------------------------|
| Link                         | [https://dimoco.eu/](https://dimoco.eu/) |
| Classification               | Carrier Billing                          |
| Regions                      | `Austria`, `Great Britain`, `Sweden`     |
| Currencies                   | `SEK`, `GBR`, `EUR`                      |
| Methods/PaymentTxTypes       | `DimocoDeposit`                          |
| PaymentIQ Configuration File | `DimocoConfig`                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.dimoco.DimocoConfig>
 <enabled>true</enabled>
  
  <accounts>

    <entry>
      <string>AT</string> <!-- Used for AUT -->
      <account>
       <merchantId>??</merchantId> <!-- MerchantID -->
       <accountID>??</accountID>   <!-- AppID _ OrderID -->
       <secretKey>??</secretKey>  <!-- Merchant PW -->
       <container>window</container>
       <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  
    <entry>
      <string>UK</string> <!-- Used for GBR -->
      <account>
       <merchantId>??</merchantId> <!-- MerchantID -->
       <accountID>??</accountID>   <!-- AppID _ OrderID -->
       <secretKey>??</secretKey>  <!-- Merchant PW -->
       <container>window</container>
       <supportedCurrencies>GBP</supportedCurrencies>
      </account>
    </entry>
   
    <entry>
      <string>SE</string> <!-- Used for SWE -->
      <account>
       <merchantId>??</merchantId>
       <accountID>??</accountID>
       <secretKey>??</secretKey> 
       <supportedCurrencies>SEK</supportedCurrencies>
      </account>
    </entry> 
  
 </accounts>
 
 <!-- Enable operator lookup, disabled by default
 <doOperatorLookup>true</doOperatorLookup> -->
 
</com.devcode.paymentiq.integration.dimoco.DimocoConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                                                           |
|-------------------------|-------------------------------------------------------------------------------|
| merchantId              | merchant_id – merchant identification provided by DIMOCO during service setup |
| accountID               | order_id – service identification provided by DIMOCO during service setup     |
| secretKey               | Merchant password provided during service setup by DIMOCO                     |

### Example
```xml
<com.devcode.paymentiq.integration.dimoco.DimocoConfig>
 <enabled>true</enabled>
  <accounts>
   <entry>
     <string>default</string>
     <account>
       <merchantId>XXXXXX</merchantId> <!-- merchant_id -->
       <accountID>XXXXXX</accountID>   <!-- order_id -->
       <secretKey>XXXXXXXXXXXXXXX</secretKey>  <!-- Merchant PW -->
     </account>
   </entry>
 </accounts>
</com.devcode.paymentiq.integration.dimoco.DimocoConfig>
```

### Enable Operator Lookup

It's possible to enable an Operator Lookup request that provides which MNO (mobile number operator) a phone number is connected to. This will in turn be provided to Dimoco in the payment request.

This feature is by default disabled since Dimoco will perform this action themselves, but if it proves necessary to use in the future it can be enabled with the following configuration tag:

`<doOperatorLookup>true</doOperatorLookup>`

## Example Routing Rule
![](/img/providers/routing/dimoco.png)

## Test Information

The phone number value is first and foremost taken from the `mobile` parameter of the user account information received from the merchant, however, if wanted it's also possible to provide the number as the `phoneNumber` input parameter in the deposit request.

### AUT

- Phone number: `+436644669971`
- Amount: 1 EUR

### GBR and SWE

Testing has to be done together with Dimoco, where they provide you with a valid phone number to use. After a transaction is initiated you will be prompted to enter a PIN code which the agent at Dimoco will provide.
