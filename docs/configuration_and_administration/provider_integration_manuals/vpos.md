--- 
id: "vpos" 
title: "VPos"
hide_title: "true"
---
 
![](/img/providers/logos/vpos.png)

# VPos

## About
Finance Incorporated(VPos) is a card processor offering 3DS/N3DS Deposits, Refunds and Voids.

| Provider Name                | VPos                                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.financeincorp.com](https://www.financeincorp.com)                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`<br/> `Capture`<br/> `Void`                    |
| PaymentIQ Configuration File | `VPosConfig`                                                                    |
  
## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vpos.VPosConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <supportedCurrencies>USD|EUR|JPY</supportedCurrencies>
        <use3Dsecure>true</use3Dsecure><!-- true/false-->
        <authType>PRE_AUTH</authType>
           <!--
        <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType>
        <authType>PRE_AUTH</authType>
        -->
      </account>
    </entry>
  </accounts>
  <pspTimeZone>GMT+03:00</pspTimeZone> <!-- GMT+03:00 for test env / GMT+02:00 for production -->
</com.devcode.paymentiq.integration.vpos.VPosConfig>

```
</details>

### Attributes

| Attribute   | Description                                                                                                                          |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| apiKey      | Api_Key provided by Finance Incorporated (VPos) to be used for Authentication.                                                       |
| secretKey   | SecretKey generated from Finance Incorporated (VPos) dashboard.                                                                      |
| pspTimeZone | The time zone of the provider server. It takes the value of GMT+03:00 for test environment and GMT+02:00 for production environment. |

### Generate secret key
1. Log in to your customer account on Finance Incorporated (VPos) dashboard.
2. Go to Admin > Merchant Transactions > Secret Key
3. Click the `+` sign on the top right corner. 
4. Enter the secret key Name and choose your merchant, terminal and the methods that the key will be used for.
5. Enter the IP addresses that the requests will be send from. PaymentIQ IP addresses can be found [here](https://github.com/devcode-git/dev-portal-backend/blob/master/content/europe/providerintegrationmanuals/general/provider_ip_whitelist.md)                          
6. Click "add".
7. Copy the secret key and paste it to the secretKey variable in your PIQ VPosConfig.
8. Click "Save" at the bottom of the page.

## Example Routing Rule
![](/img/providers/routing/vpos.png)

## Test Information

| Card Brand | 3DS | Card Number      | CVV | Expiry Date | Result/Info                                                            |
|------------|-----|------------------|-----|-------------|------------------------------------------------------------------------|
| MASTERCARD | yes | 5265448007549389 | 950 | 05/24       | Approved                                                               |
| MASTERCARD | yes | 5265447549051474 | 808 | 05/24       | Simulates the situation where cancellation or wrong validation is made |
| MASTERCARD | no  | 5460550223332202 | 808 | 05/24       | Approved                                                               |
