--- 
id: "sirumobile" 
title: "Siru Mobile"
hide_title: "true"
---
 
![](/img/providers/logos/sirumobile.png)

# Siru Mobile

## About
Siru Mobile is a technical service provider of mobile payments. By using Siru Mobile services, customers can easily purchase products and services with their mobile phones.

Siru uses different "Variants" as they call it, which are different solutions to their mobile payments gateway. A merchant needs to know which variants they are going to process for their markets.

### Variant 1
Payment by calling is the choice for older mobile phones (feature phones), or for regions where IP payment is not available. The customer may use either a full fledged smartphone or a desktop browser. The only features required from the phone are capability to a) receive SMS's and b) make calls to premium rate numbers.

The customer is redirected to a web page where he is asked to call a telephone number in order to confirm his purchase. After the call is either completed, canceled or failed, customer is redirected back to the merchant's service.

### Variant 2
* Note, This method is not available for gambling merchants.

IP Payment is for smart phones and is currently only available in Finland.

The flow is very quick and simple. The merchant creates a purchase via our API and the user is redirected to Siru's payment page. User just clicks to confirm payment and we bill the customer's mobile subscription. User is then redirected back to the merchant's system. This requires a mobile internet connection.

* WARNING!
If one opens up an insecure mobile tethering hotspot, other people can connect it and make purchases.

### Variant 3
This is a digital wallet where customer can deposit money with various means (Siru Mobile payment gateway, for example) and use it everywhere where the wallet is an accepted payment method.

### Variant 4
Variant 4 uses external payment gateway for each country(currently only for UK).

Payment flow may differ for each country. Most common payment flow is where merchant creates a purchase via merchant API and the user is redirected to Siru payment page. User will confirm purchase and is then redirected back to merchant website. The payment confirmation will often require entering a PIN code that is automatically sent to user's mobile phone.

### Variant limitations

| Variant  | Limitations                                                                                                                                                                                   |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Variant1 | Countries FI, SE and NO.   You must use a mobile phone subscription from selected country and you can not be roaming. This variant may not be available in Norway depending on your business. |
| Variant2 | Countries FI       You must use a mobile connection for variant   2 to work.                                                                                                                  |
| Variant3 | Countries FI, SE, NO and GB                                                                                                                                                                   |
| Variant4 | Countries GB                                                                                                                                                                                  |


| Provider Name                | Siru Mobile                                        |
|------------------------------|----------------------------------------------------|
| Link                         | [https://sirumobile.com/](https://sirumobile.com/) |
| Classification               | Mobile Payment                                     |
| Regions                      | `Finland`, `Sweden`, `Norway`, `UnitedKingdom`     |
| Currencies                   | `SEK`, `EUR`                                       |
| Methods/PaymentTxTypes       | `SiruDeposit`                                      |
| PaymentIQ Configuration File | `SiruConfig`                                       |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.siru.SiruConfig>
  <enabled>true</enabled>
  <accounts>
      <entry>
        <string>variant1</string>
        <account>
          <serviceEndpoint>https://payment.sirumobile.com</serviceEndpoint>
          <secretKey>??</secretKey>
          <merchantId>??</merchantId>
          <successUrl>${successUrl}</successUrl>
          <failureUrl>${failureUrl}</failureUrl>
          <version>variant1</version>
        </account>
      </entry>
      
      <entry>
        <string>variant3</string>
        <account>
          <serviceEndpoint>https://payment.sirumobile.com</serviceEndpoint>
          <secretKey>??</secretKey>
          <merchantId>??</merchantId>
          <successUrl>${successUrl}</successUrl>
          <failureUrl>${failureUrl}</failureUrl>
          <version>variant3</version>
        </account>
      </entry>
      
      <entry>
        <string>variant4</string>
        <account>
          <serviceEndpoint>https://payment.sirumobile.com</serviceEndpoint>
          <secretKey>??</secretKey>
          <merchantId>??</merchantId>
          <successUrl>${successUrl}</successUrl>
          <failureUrl>${failureUrl}</failureUrl>
          <version>variant4</version>
        </account>
      </entry>
  </accounts>
  <notificationUrl>${baseCallbackUrl}/api/siru/deposit/callback</notificationUrl>
  <returnUrl>${baseRedirectUrl}/api/siru/deposit/redirect/${ptx.txRefId}/</returnUrl>
  <taxClass>2</taxClass>
  <serviceGroup>2</serviceGroup>
  <isIframe>true</isIframe>
  <defaultDescriptor>??</defaultDescriptor> <!-- This value translates to "title" parameter and is required when making variant4 payments -->
  <submerchantReference>??</submerchantReference>
</com.devcode.paymentiq.integration.siru.SiruConfig>
```

</details>

### Attributes

| Attribute  | Description      |
|------------|------------------|
| secretKey  | Provided by Siru |
| merchantId | Provided by Siru |

## Example Routing Rule
![](/img/providers/routing/sirumobile.png)

## Test Information

### Variant1 (Traditional)
- Must user Swedish or Finnish user
- For Swedish users the initial basePrice (amount) must be 2.50, 5.00 or 10.00
- For Finnish users the initial basePrice (amount) must be 2.50, 5.00, 10.00 or 15.00
- For Norway and Finland, you can use your swedish number in the staging environment.

### Variant3 (Wallet)
- Must use a Norwegian user
- If wallet runs out of money, contact Siru at https://sirumobile.com/dev

Phone number	Password
4771111111		96130842

### Variant4 (UK)
To test payments, you either need your own UK mobile subscription or you can use one the test numbers. No actual charges will be made.

Phone number	Expected result
440000000001	Simulates successful payment
440000000017	Simulates successful payment
440000000002	Simulates invalid phone number error