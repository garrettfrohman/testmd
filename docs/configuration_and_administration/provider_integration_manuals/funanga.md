--- 
id: "funanga" 
title: "Funanga Cash2Code"
hide_title: "true"
---
 
![](/img/providers/logos/cashtocode.png)

# Funanga Cash2Code

## About
CashToCode-light WebClient-API is processed as a Gift-Card (voucher).

| Provider Name                | Funanga Cash2Code                                                               |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.funanga.com/](https://www.funanga.com/)                            |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `FunangaDeposit`                                                                |
| PaymentIQ Configuration File | `FunangaConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.funanga.FunangaConfig>
  <enabled>true</enabled>
  <container>window</container>
  <accounts>
    
    <entry>
      <string>default</string> <!-- Create one MID per Currency -->
      <account>
        <username>??</username> <!-- Authentication username -->
        <password>??</password> <!-- Authentication password -->
        <serviceEndpoint>https://devcode.api.cashtocode.com/</serviceEndpoint>
        <supportedCurrencies>EUR</supportedCurrencies> <!-- Set one Currency per MID, the same currency as set by Cash2Code for that MID -->
        
        <redirectUrl>${baseRedirectUrl}/api/funanga/deposit/redirect/${ptx.txRefId}</redirectUrl>
        <!--<redirectUrl>${baseRedirectUrl}/api/funanga/deposit/redirect/${ptx.txRefId}?txRefId=${ptx.txRefId}&amp;status=success</redirectUrl>-->
        <!--?txRefId=${ptx.txRefId}&amp;status=success-->
        <callbackUrl>${baseCallbackUrl}/api/funanga/deposit/callback/</callbackUrl>
        <repayUrl>${baseCallbackUrl}/api/funanga/deposit/repay/</repayUrl>
       
        <!--callback authorisation details (basic auth)-->
         <brandId>??</brandId> <!-- CashtoCode MID reference -->
        <siteReference>??</siteReference> <!-- Value PaymentIQ set and provide to Funange/Cashtocode. Do not change. -->
        <notificationPassword>??</notificationPassword> <!-- Value PaymentIQ set and provide to Funange/Cashtocode. Do not change. -->
         
      </account>
    </entry>
    
  </accounts>

</com.devcode.paymentiq.integration.funanga.FunangaConfig>
```
</details>

From Funanga side, you need to request API credentials (username and password) for your account. From PaymentIQ BO configuration, you need to ask Funanga team to configure the notification/callback URL at Funanga side. 
Also, please note that the notification URL basic auth credentials (siteReference/notificationPassword) need to be consistent with the ones that are configured at Funanga side. A brand ID should be also configured at Funanga side. This brand ID is tied with your account. In the following configuration it is called “devcode”.

![](/img/providers/funanga01.png)

### Funanga code approval:

In order to approve the voucher code, you will need to simulate that process by using the below credentials on the following URL:
https://faketerminal.nahzahlen.de
User name: devcode
Password: bDg6GkDrMBaLtPc2

Once logged in, follow the below steps to redeem the test voucher:
Step 1
![](/img/providers/funanga02.png)
Step 2
![](/img/providers/funanga03.png)

## Transaction Flow

The following is a test from PaymentIQ's test cashier in order to visualize the purchase steps.

![](/img/providers/funanga04.png)
![](/img/providers/funanga05.png)
![](/img/providers/funanga06.png)
![](/img/providers/funanga07.png)

## Example Routing Rule
![](/img/providers/routing/funanga.png)
## Test Information

The following price points and currencies can be used. Note that the user used must be from the country mentioned before the price point!

- GERMANY: 10€, 25€, 50€, 100€, 200€, 400€
- AUSTRIA: 10€, 25€, 50€, 100€, 200€, 300€, 400€, 500€
- UK: flexible between 20 and 250 GBP

``Note that the above price points may not be the same for you in production nor test if you're not using PaymentIQ provided test credentials``
