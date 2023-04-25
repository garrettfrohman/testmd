--- 
id: "paylevo" 
title: "Paylevo"
hide_title: "true"
---
 
![](/img/providers/logos/paylevo.png)

# Paylevo

## About
Paylevo is a invoice provider with support for Deposits.

| Provider Name                | Paylevo                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://paylevo.com/en/](http://paylevo.com/en/)                                |
| Classification               | Invoice                                                                         |
| Regions                      | `Sweden`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `PaylevoDeposit`                                                                |
| PaymentIQ Configuration File | `PaylevoConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paylevo.PaylevoConfig>
   <enabled>true</enabled>
   <accounts>
      <entry>
         <string>default</string>
         <account>
            <merchantId>??</merchantId>
            <redirectUrl>https://test-api.paymentiq.io/paymentiq/api/paylevo/deposit/redirect</redirectUrl>
            <successUrl>${successUrl}</successUrl>
            <failureUrl>${failureUrl}</failureUrl>
         </account>
      </entry>
   </accounts>
   <disableSSLCertificate>true</disableSSLCertificate>
   <checkUrl>https://api.stage.kriita.com/player/{merchantId}/{playerId}</checkUrl>
   <sessionUrl>https://api.stage.kriita.com/session/{merchantId}/deposit-ui</sessionUrl>
   <creditApprovalUrl>https://test-api.paymentiq.io/paymentiq/api/paylevo/deposit/creditApproval</creditApprovalUrl>
   <successCallbackUrl>https://test-api.paymentiq.io/paymentiq/api/paylevo/deposit/callback</successCallbackUrl>
   <failCallbackUrl>https://test-api.paymentiq.io/paymentiq/api/paylevo/deposit/callback</failCallbackUrl>
   <sessionControl>{"forceKyc":"true"}</sessionControl>
</com.devcode.paymentiq.integration.paylevo.PaylevoConfig>

```

</details>

### Attributes

| Attribute  | Description        |
|------------|--------------------|
| merchantId | Provide by Paylevo |

## Example Routing Rule

![](/img/providers/routing/paylevo.png)

## Test Information

Please contact the Provider directly.