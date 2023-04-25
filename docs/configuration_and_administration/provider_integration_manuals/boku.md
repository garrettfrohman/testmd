--- 
id: "boku" 
title: "Boku"
hide_title: "true"
---
 
![](/img/providers/logos/boku.png)

# Boku

## About
In simple terms Boku allows people to make purchases using their mobile telephone number, the charge goes directly to their mobile phone bill.

Please see the following videos:

[https://www.youtube.com/watch?v=rO57dqUDrsY](https://www.youtube.com/watch?v=rO57dqUDrsY)
[https://www.youtube.com/watch?v=ndMTOSnP1zc](https://www.youtube.com/watch?v=ndMTOSnP1zc)

| Provider Name                | Boku                                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.boku.com/](https://www.boku.com/)                                  |
| Classification               | Mobile Payment                                                                  |
| Regions                      | `United Kingdom`                                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BokuDeposit`                                                                   |
| PaymentIQ Configuration File | `BokuConfig`                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.boku.BokuConfig>
<enabled>true</enabled>
<accounts>
    <entry>
     <string>default</string>
     <account>
       <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <redirectUrl>${baseRedirectUrl}/api/boku/deposit/redirect/${ptx.txRefId}</redirectUrl>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
     </account>
    </entry>
  </accounts>
  <services>
    <entry>
      <string>??</string>
      <bokuService>
          <name></name>
          <serviceId>??</serviceId>
       </bokuService>
       </entry>
       <entry>
      <string>??</string>
      <bokuService>
          <name></name>
          <serviceId>??</serviceId>
       </bokuService>
       </entry>
        <entry>
      <string>??</string>
      <bokuService>
          <name></name>
          <serviceId>??</serviceId>
       </bokuService>
       </entry>
       <entry>
      <string>??</string>
      <bokuService>
          <name></name>
          <serviceId>??</serviceId>
       </bokuService>
       </entry>
  </services>
  <callbackUrl>${baseCallbackUrl}/api/boku/deposit/callback?transId=${ptx.txRefId}</callbackUrl>
  <defaultDescriptor>Account Deposit</defaultDescriptor>
</com.devcode.paymentiq.integration.boku.BokuConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential |
|-------------------------|---------------------|
| merchantId              | Merchant ID         |
| secretKey               | API Security Key    |

### How to call Boku and make a deposit via a certain service Id at Boku

There are two ways to use this provider and its services, the merchant can use a fixed amount corresponding a service Id at Boku.

Example request for fixed amount, some attributes should be exactly corresponded:

User country : GBR
Amount : 20.00
Currency : GBP

```xml
<services>
    <entry>
      <string>GB 20.00 GBP</string>
      <bokuService>
          <name></name>
          <serviceId>8230f20156dace9a82de657f</serviceId>
       </bokuService>
       </entry>
</services>
```

Or the merchant need to send in the process request a attribute “serviceKey”.
then PaymentIQ will pick the corresponded service for the request to make the transaction:

ex :  “serviceKey = GBP service 1”

```xml
<services>
<entry>
      <string>GBP service 1</string>
      <bokuService>
          <name></name>
          <serviceId>8230f20156dace9a82de657f</serviceId>
       </bokuService>
     </entry>
 </services>
```
## Example Routing Rule
![](/img/providers/routing/boku.png)

## Test Information

Since our test account only works for GBP currency, the user country should be UK.

- Currency: GBP
- User country: GBR
- Phone number: GB00
- Amount: 12, 14 GBP
- (E.g TEST_GBP as mock user)
- Select network in the iframe
