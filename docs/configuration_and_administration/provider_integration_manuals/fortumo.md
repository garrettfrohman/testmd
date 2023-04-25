--- 
id: "fortumo" 
title: "Fortumo"
hide_title: "true"
---
 
![](/img/providers/logos/fortumo.png)

# Fortumo

## About
Fortumo is connected to more than 350 mobile operator networks in 100 countries. Our platform processes millions of payments each day, which means we have extensive data about user profiles and payment preferences around the world.

| Provider Name                | Fortumo                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://fortumo.com](https://fortumo.com)                                      |
| Classification               | Mobile Payment                                                                  |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `FortumoDeposit`                                                                |
| PaymentIQ Configuration File | `FortumoConfig`                                                                 |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.fortumo.FortumoConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>test</string>
      <account>
        <username>??</username>
        <password>??</password>
        <redirectUrl>https://test-api.paymentiq.io/paymentiq/api/fortumo/deposit/redirect/${ptx.txRefId}/STATUS</redirectUrl>
        <secretKey>??</secretKey>
        <service>??</service>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
    <entry>
      <string>MANUAL-UK</string>
      <account>
         <username>??</username>
         <password>??</password>
         <redirectUrl>https://test-api.paymentiq.io/paymentiq/api/fortumo/deposit/redirect/${ptx.txRefId}/STATUS</redirectUrl>
         <secretKey>??</secretKey>
         <successUrl>${successUrl}</successUrl>
         <failureUrl>${failureUrl}</failureUrl>
         <useTokenId>false</useTokenId>
      </account>
    </entry>
  </accounts>
   <!--  ServicePackConfig  -->
  <servicePack>
    <entry>
      <string>FN 5</string>
      <fortumoServicePack>
        <name>test pack</name>
        <amount>5.20 EUR</amount>
        <serviceId>??</serviceId>
      </fortumoServicePack>
    </entry>
    <entry>
      <string>SE 100</string>
      <fortumoServicePack>
        <name>test pack</name>
        <amount>5.20 EUR</amount>
        <serviceId>??</serviceId>
      </fortumoServicePack>
    </entry>
    <entry>
      <string>UK 30</string>
      <fortumoServicePack>
        <name>UK test pack</name>
        <amount>30 GBP</amount>
        <serviceId>??</serviceId>
      </fortumoServicePack>
    </entry>
  </servicePack>
</com.devcode.paymentiq.integration.fortumo.FortumoConfig>
```
</details>

### Attributes

-

## Example Routing Rule

![](/img/providers/routing/fortumo.png)

## Test Information
No test informationa available.
