--- 
id: "ticketpremium" 
title: "Ticket Premium"
hide_title: "true"
---
 
![](/img/providers/logos/ticketpremium.png)

# Ticket Premium

## About
The Ticket Premium Group delivers end-to-end financial solutions enabling international electronic payment processes.

| Provider Name                | Ticket Premium                                                                  |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.tsi-payment.com/en/](http://www.tsi-payment.com/en/)                |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `Europe`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `TicketPremiumDeposit`                                                          |
| PaymentIQ Configuration File | `TicketPremiumConfig`                                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ticketsurf.rest.TicketSurfRestConfig>
<enabled>true</enabled>
<useViqProxy>true</useViqProxy>
<accounts>
  <entry>
    <string>Rest3DS</string>
    <account>
      <merchantId>??</merchantId>
      <merchantName>??</merchantName>
      <apiKey>??</apiKey>
      <secretKey>??</secretKey>
      <useTokenId>true</useTokenId>
    </account>
  </entry>
  <entry>
    <string>RestN3DS</string>
    <account>
      <merchantId>??</merchantId>
      <merchantName>??</merchantName>
      <apiKey>??</apiKey>
      <secretKey>??</secretKey>
      <useTokenId>true</useTokenId>
    </account>
  </entry>
</accounts>
<defaultDescriptor>??</defaultDescriptor>
<testMode>true</testMode>
</com.devcode.paymentiq.integration.ticketsurf.rest.TicketSurfRestConfig>
```
</details>

### Attributes

| Attribute    | Description                |
|--------------|----------------------------|
| merchantId   | Provided by Ticket Premium |
| merchantName | Provided by Ticket Premium |
| apiKey       | Provided by Ticket Premium |
| secretKey    | Provided by Ticket Premium |

## Example Routing Rule
![](/img/providers/routing/ticketpremium.png)

## Test Information

- Try to keep the transaction amount as low as possible.

| Voucher Number   |
|------------------|
| 3135270654215318 |
| 0263592307727584 |
| 7285836431178393 |