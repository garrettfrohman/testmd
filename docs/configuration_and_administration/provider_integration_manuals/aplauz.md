--- 
id: "aplauz" 
title: "Aplauz"
hide_title: "true"
---
 
![](/img/providers/logos/aplauz.png)

# Aplauz

## About
Aplauz is prepaid payment method that consists of a 16-digit code representing a specific denomination and currency.
The Aplauz product is purchased at local convenience stores and can be used to make online payments at the participating online Merchants.

| Provider Name                | Aplauz                                     |
|------------------------------|--------------------------------------------|
| Link                         | [https://aplauz.com/](https://aplauz.com/) |
| Classification               | Voucher                                    |
| Regions                      | Switzerland and EU                         |
| Currencies                   | `CHF`                                      |
| Methods/PaymentTxTypes       | `AplauzDeposit`                            |
| PaymentIQ Configuration File | `AplauzConfig`                             |

## Configuration Information


<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.aplauz.AplauzConfig>
<enabled>true</enabled>
<testMode>true</testMode>
  <accounts>
    <entry>
     <string>default</string>
     <account>
       <apiKey>???</apiKey>
       <channelId>???</channelId>
       <supportedCurrencies>CHF</supportedCurrencies>
       <secretKey>???</secretKey>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.aplauz.AplauzConfig>
```

</details>

### Attributes
| Attribute | Description                                                                                                   |
|-----------|---------------------------------------------------------------------------------------------------------------|
| apiKey    | Api key provided by Aplauz. It is a value that uniquely identifies the merchant company on the provider side. |
| channelId | Channel id or (UUid) provided by Aplauz. It is the Aplauz id of the merchant.                                 |
| secretKey | The generated Rsa private key.                                                                                |

### How to generate RSA keys
 Please reach out to our technical support if you need help with this.
 1.  Merchant needs to generate a RSA keyPair.                                                                                                 
   - Generate a RSA key pair using the command:  
     
     `openssl genrsa -out private_key.pem 4096 `                                                                    
   - Generate the RSA public key from your private key using the command:
    
     `openssl rsa -pubout -in private_key.pem -out public_key.pem`                   
 2. Send  the public key pem file to Aplauz team
 3. Paste the content of the private key into secretKey attribute in AplauzConfig.

## Example Routing Rules
![](/img/providers/routing/aplauz.png)

 
## Test Information

### Deposits
- Ask Aplauz team to provide codes for test. 
- To initiate a payment the user need to enter at least one 16 digit code. If the user want to use more than one code then he need to click on the plus sign button 
 to open a new input field to enter another 16 digit code. 
 Note: maximun number of coupon code the user can use in one payment is 5 codes.
### Settlements and invoicing
- After successful payment transactions have been made, funds are settled according to the agreed payment schedule.
   Invoices are sent via email to the authorized person you have specified during your onboarding.





