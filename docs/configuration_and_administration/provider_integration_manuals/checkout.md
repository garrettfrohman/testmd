--- 
id: "checkout" 
title: "Checkout"
hide_title: "true"
---
 
![](/img/providers/logos/checkout.png)

# Checkout

## About
Checkout.com is an international provider of online payment solutions. Checkout.com solutions are built on 100% proprietary technology and handle every part of the payment process.

| Provider Name                | Checkout                                                                                                                                         |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.checkout.com/](https://www.checkout.com/)                                                                                           |
| Classification               | Debit/Credit Card Processor                                                                                                                      |
| Regions                      | `International`                                                                                                                                  |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `CreditcardAccountVerification`<br/> `GooglePayDeposit`<br/> `ApplePayDeposit` |
| PaymentIQ Configuration File | `CheckoutConfig`                                                                                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.checkout.CheckoutConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <secretKey>???</secretKey>
        <!-- <secretKey>Bearer ???</secretKey> Please include "Bearer " infront of your API key if you're using Checkouts new gateway -->

        <supportedCurrencies>USD|EUR|NOK</supportedCurrencies>
        <transactionChannel>card</transactionChannel>
        <authType>PRE_AUTH</authType>
        <!--
           <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType> -->
        
     </account>
    </entry>
    <entry>
     <string>3DS2</string>
     <account>
        <secretKey>???</secretKey>
        <!-- <secretKey>Bearer ???</secretKey> Please include "Bearer " infront of your API key if you're using Checkouts new gateway -->

        <supportedCurrencies>USD|EUR|NOK</supportedCurrencies>
        <transactionChannel>card</transactionChannel>
        
        <!--<authType>PRE_AUTH</authType>
        <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType> -->
        
        <use3Dsecure>true</use3Dsecure>
        <!-- 3DS2 Parameters -->
        <acquirerMerchantId>XXXXXXXX</acquirerMerchantId> <!-- Value received from PSP  -->
        <mcc>7995</mcc> <!-- 7995 for gambling merchants change if this isn't applicable to you -->
        <merchantCountry>XXX</merchantCountry> <!-- Origin country of merchant 3 DIGIT ISO for eaxmple SWE or MLT -->
        <merchantUrl>http://www.example.com</merchantUrl> <!-- URL to your website -->
        <merchantName>XXX</merchantName> <!-- Name of your brand -->
        <!-- End of 3DS2 parameters -->
     </account>
    </entry>
    <entry>
      <string>ACCOUNT_VER</string>
      <account>
         <secretKey>???</secretKey>
        <!-- <secretKey>Bearer ???</secretKey> Please include "Bearer " infront of your API key if you're using Checkouts new gateway -->
        <authType>FINAL_AUTH</authType>
         <supportedCurrencies>USD|EUR|NOK</supportedCurrencies>
         <transactionChannel>card</transactionChannel>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.checkout.CheckoutConfig>
```

</details>

### Attributes

| Attribute          | Description                                     |
|--------------------|-------------------------------------------------|
| transactionChannel | Corresponds to the type of payment source.      |
| publicKey          | Corresponds to the public Api key from Checkout |
| secretKey          | Corresponds to the secret Api key from Checkout |


### Google Pay setup
To setup Google Pay you need to first add a ```GooglePayConfig``` to your MID. It is crucial to set ```<gateway>``` to **checkoutltd** and ```<gatewayMerchantId>``` to your public key generated by Checkout in the ```GooglePayConfig```, i.e.: <br/>

```<gateway>checkoutltd</gateway>``` <br/>
```<gatewayMerchantId>YOUR_CHECKOUT_PUBLIC_KEY_HERE</gatewayMerchantId>```

In your ```CheckoutConfig``` you need to add both your public and secret Checkout keys for an account entry in the configuration, i.e.: <br/>

```<publicKey>YOUR_CHECKOUT_PUBLIC_KEY_HERE</publicKey>``` <br/>
```<secretKey>YOUR_CHECKOUT_PRIVATE_KEY_HERE</secretKey>```

Also add ```<transactionChannel>googlepay</transactionChannel>``` for an account entry.

Lastly make sure that ```<convertHtmlPageToRedirectUrl>``` is set to **false** in your ```MerchantConfig```.


## Example Routing Rule
![](/img/providers/routing/CheckoutRouting.png)

## Test Information

Please check directly with the provider.