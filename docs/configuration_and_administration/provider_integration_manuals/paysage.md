--- 
id: "paysage" 
title: "Paysage"
hide_title: "true"
---
 
![](/img/providers/logos/paysage.png)

# Paysage

## About
Paysage is an aggregator provider offering Credit Card and several Alternative Payment Methods. Credit Card payments supports Deposit, Withdrawal, Refund, Void, Auth and Capture. For Alternatvie Payment Methods it depends on the specific method, where all supports Deposit and some also Withdrawal and Refund. Please check with the provider for more details.


| Provider Name                | Paysage Payments                                                                                         |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| Link                         | [https://paysage.io/](https://paysage.io/)                                                               |
| Classification               | Aggregator                                                                                               |
| Regions                      | International                                                                                            |
| Currencies                   | `EUR`, `USD`                                                                                             |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal`  <br/> `WebRedirectDeposit`<br/>`WebRedirectWithdrawal` |
| PaymentIQ Configuration File | `PaysageConfig`                                                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paysage.PaysageConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>apm</string>
      <account>
        <merchantId>????</merchantId>
        <secretKey>???????</secretKey>
        <supportedCurrencies>INR|USD|EUR|SEK</supportedCurrencies>
        <serviceEndpoint>https://api.paysage.io</serviceEndpoint>
      </account>
    </entry>
    <entry>
      <string>n3ds</string>
      <account>
        <merchantId>????</merchantId>
        <secretKey>???????</secretKey>
        <authType>AUTH_CAPTURE</authType>
        <use3Dsecure>false</use3Dsecure>
        <supportedCurrencies>USD|EUR|SEK</supportedCurrencies>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <string>3ds</string>
      <account>
        <merchantId>????</merchantId>
        <secretKey>???????</secretKey>
        <authType>AUTH_CAPTURE</authType>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>USD|EUR|SEK</supportedCurrencies>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.paysage.PaysageConfig>
```
</details>

### Attributes

| Attribute                  | Description                                                                                             |
|----------------------------|---------------------------------------------------------------------------------------------------------|
| merchantId                 | Shop ID. Provided by Paysage                                                                            |
| secretKey                  | Provided by Paysage                                                                                     |
| serviceEndpoint            | Endpoint differs between Credit Cards and APMs so needs to be set here for non Credit Cards             |
| useTokenId                 | Send request using stored token instead of credit card details. Required to skip 3ds for enrolled cards |
| replacePostRedirectWithGet | Defaults to false. See details below.                                                                   |

### Supported APMs
The table below shows the supported payment methods and the corresponding TxTypes that should be used. The service parameter should be included in the front API request only for the generic WebRedirect\* and Bank\* types.

| Name           | TxType                                   | Service parameter |
|----------------|------------------------------------------|-------------------|
| Astropaywallet | WebRedirectDeposit,WebRedirectWithdrawal | ASTROPAYWALLET    |

### Replace POST redirect with GET
If the APM's redirect is method POST and doesn't allow iframes there have been issues with the redirect using Safari on iOS devices. A workaround have been made that will replace the POST redirect with a GET redirect. Instead of making the POST directly to the provider service this will make a GET request back to PaymentIQ which will respond with a simple HTML page that automatically makes the initial provider POST. To activate this feature add this to the configs account or top level:

`<replacePostRedirectWithGet>true</replacePostRedirectWithGet>`

## Example Routing Rule
![](/img/providers/routing/paysage.png)
![](/img/providers/routing/paysage_webredirect.png)

## Transaction Flow
NOTE: There is only one endpoint for live and test mode. In order to toggle between them, there is attribute testMode in PaysageConfig

### Creditcard 
1. The user enters the amount and the credit card details in the Cashier.
2. PaymentIQ sends a deposit request to the Paysage.
3. Paysage sends back a response with the url that the user is redirected to.
4. PaymentIQ performs a status check and updates the status accordingly. If the status is pending, PaymentIQ awaits for
a callback from Paysage with the updated transaction status and then performs a status check again, updating the status 
   of the transaction accordingly to the response.

### WebRedirect (ASTROPAYWALLET)
Redirect payment solution that redirects to the ASTROPAYWALLET website.
A notification will be sent to PaymentIQ when the payment is done.

## Test Information

### Credit Card

Please check [https://docs.paysage.io/en/test-integration#test-card-number](https://docs.paysage.io/en/test-integration#test-card-number) for up to date test cards.