--- 
id: "conectapp" 
title: "ConectApp"
hide_title: "true"
---
 
![](/img/providers/logos/conectapp.png)

# ConectApp

## About
ConectApp is a credit card provider that offers N3DS deposit (sale, authorization + capture) and void (no statuscheck).

| Provider Name                | ConectApp                                          |
|------------------------------|----------------------------------------------------|
| Link                         | [http://www.conectapp.mx](http://www.conectapp.mx) |
| Classification               | Debit/Credit Card Processor                        |
| Regions                      | `International`                                    |
| Currencies                   | `USD`, `EUR`, `MXN`                                |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Refund`, `Capture`, `Void`   |
| PaymentIQ Configuration File | `ConectAppConfig`                                  |
  
## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.conectapp.ConectAppConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username> <!-- user -->
        <password>???</password> <!-- password -->
        <secretKey>???</secretKey> <!-- terminalCode -->
        <merchantCode>???</merchantCode><!-- merchantCode -->
        <supportedCurrencies>USD</supportedCurrencies>
        <authType>AUTH_CAPTURE</authType>
           <!--
        <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType>
        <authType>PRE_AUTH</authType>
        -->
        <storeLocationId>GMT-5</storeLocationId><!--could take GMT+1 as well-->
      </account>
    </entry>
  </accounts>
  <posEnvironment>ecommerce</posEnvironment><!-- posEnvironment -->
</com.devcode.paymentiq.integration.conectapp.ConectAppConfig>
```
</details>

### Attributes

| Attribute    | Description                                                                            |
|--------------|----------------------------------------------------------------------------------------|
| username     | Secret Key provided by ConectApp to be used as a user for Authentication(BasicAuth).   |
| password     | Password provided by ConectApp to be used as a password for Authentication(BasicAuth). |
| secretKey    | Terminal Code provided by ConectApp                                                    |
| merchantCode | Merchant Code provided by ConectApp                                                    |


## Example Routing Rule
![](/img/providers/routing/conectapp.png)

## Test Information

#### Card Number

 - 4444 3333 2222 1111
    - SUCCESS payment
    
 - 4000 0000 0000 0127
    - FAILED payment
    - 500 INTERNAL_SERVER_ERROR reason
    
 - 4000 0000 0000 0077
    - FAILED payment
    - INSUFFICIENT_FUNDS reason
    
 - 4000 0000 0000 0069
    - FAILED payment
    - CARD_EXPIRED reason
    
 - 4000 0000 0000 0119
    - FAILED payment
    - SYSTEM_ERROR reason
  
#### Security Code

Any 3 digits for VISA/MC

#### Expiration Date

Any expiration date

