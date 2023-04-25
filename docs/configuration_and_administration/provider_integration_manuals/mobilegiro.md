--- 
id: "mobilegiro" 
title: "MobileGiro"
hide_title: "true"
--- 
# MobileGiro

## About
MobileGiro is a provider that allows doing invoice payments with Bankgiro and Postgiro.

| Provider Name                | MobileGiro                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | -                                                                               |
| Classification               | -                                                                               |
| Regions                      | -                                                                               |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `SweGiroDeposit`                                                                |
| PaymentIQ Configuration File | `MobileGiroConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<com.devcode.paymentiq.integration.mobilegiro.MobileGiroConfig>
   <enabled>true</enabled>
   <useViqProxy>false</useViqProxy>
   <height>800</height>
   <width>500</width>
   <mode>test</mode>
   <container>window</container>
   <testMode>true</testMode>
   <testServiceEndPoint>https://services.paymentiq.io/mobilegiro/merchant</testServiceEndPoint>
   <liveServiceEndPoint>https://services.paymentiq.io/mobilegiro/merchant</liveServiceEndPoint>
   <accounts>
      <entry>
         <string>default</string>
         <account>
            <supportedCurrencies>SEK</supportedCurrencies>
            <beneficiaryLogoUrl>https://static.linkmobility.com\${input.beneficiaryLogoPath}</beneficiaryLogoUrl>
         </account>
      </entry>
   </accounts>
</com.devcode.paymentiq.integration.mobilegiro.MobileGiroConfig>
```
</details>

### Attributes

| Attribute          | Description                                     |
|--------------------|-------------------------------------------------|
| supportedCurrency  | The currency that is supported. Default is SEK. |
| beneficiaryLogoUrl |                                                 |

### Supported bank
The follow banks are supported for the different methods.

#### SweGiro Deposit
- SEB
- Swedbank
- Nordea
- Handelsbanken (SHB)
- Danskebank

## The SweGiro Deposit flow

### Cashier ( SweGiroDeposit method )
![](/img/providers/mobilegiro01.png)

The user doing the deposit from the cashier and the payment iq will send a redirect to SweGiro.
- Iframe and window is supported as a container for the SweGiro integration.

### Select bank ( MobileGiro side )
![](/img/providers/mobilegiro02.png)

This is the first page that the user will land on. This is where the user can select what bank that he/she wants to use. If the user has already used the swegiro service then paymentiq will remember what bank and show the login screen for the user. 

### Login with bank ID
![](/img/providers/mobilegiro03.png)

When the user has selected a bank then he/she will sign in into the bank.

### Invoice details
![](/img/providers/mobilegiro04.png)

When the user has signed in the user will get a confirmation of the invoice. 
- The user can select the account that he/she wants to use. 
	- If only one account exists then that is selected and displayed.
	- If the user has already done a SweGiro deposit before then that account will be preselected. 
- Change the due date when the invoice should be payed.

### Signing the invoice
![](/img/providers/mobilegiro05.png)

When the user has selected to confirm the invoice. Then the user has to sign the invoice in the bank id app.

### Receipt

![](/img/providers/mobilegiro06.png)

This is the receipt page when a invoice was paid successfully. 
The "referencenummer" is the ocr or message of the invoice.

## Example Routing Rule
-
## Test Information
No test accounts are available.