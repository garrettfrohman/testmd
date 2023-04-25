--- 
id: "citigate" 
title: "Citigate"
hide_title: "true"
--- 
# Citigate

## About
Citigate is a creditcard processor with support for Deposits, Refunds and Voids.

| Provider Name                | Citigate                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | -                                                                               |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`<br/> `Void`                                   |
| PaymentIQ Configuration File | `CitigateConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.citigate.CitigateConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>3DS</string>
      <account>
        <merchantId>??</merchantId>
        <password>??</password>
        <use3Dsecure>true</use3Dsecure>
        <previousAuth>true</previousAuth>
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>??</merchantId>
        <password>??</password>
        <use3Dsecure>false</use3Dsecure>
        <previousAuth>true</previousAuth>
      </account>
    </entry>
  </accounts>
  <liveServiceEndPoint>https://private.dg-gw.co.uk/orion/interface/xml.ashx</liveServiceEndPoint>		
  <callbackUrl>${baseCallbackUrl}/api/citigate/deposit/callback</callbackUrl>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.citigate.CitigateConfig>
```

</details>

### Attributes

| Attribute    | Description                        | 
|--------------|------------------------------------|
| merchantId   | Merchan ID. Provided by Citiagate. |
| password     | Password. Provided by Citiagate.   |
| previousAuth | -                                  |

## Example Routing Rule
![](/img/providers/routing/citigate.png)
## Test Information

### N3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4918891092804793 | Any | Any         |
| MASTERCARD | 5893628942330835 | Any | Any         |

### 3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4298325607650615 | Any | Any         |
| MASTERCARD | 5267213918783529 | Any | Any         |
