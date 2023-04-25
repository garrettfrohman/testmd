--- 
id: "jeton" 
title: "Jeton"
hide_title: "true"
---
 
![](/img/providers/logos/jeton.png)

# Jeton

## About
Jeton is E-Wallet provider that offers deposit, withdrawal either through their Jeton Wallet service or JetonGo, that provides instant international banking details to receive / send money across the globe.

| Provider Name                | Jeton                                                                           |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.jeton.com](https://www.jeton.com)                                  |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `JetonDeposit` <br/> `JetonWithdrawal`                                          |
| PaymentIQ Configuration File | `JetonConfig`                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.jeton.JetonConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>JETON_TEST</string>
      <account>
        <merchantId>100</merchantId>
        <apiKey>53e1dc890b7e4308b43aef8b8cdf50f2</apiKey>
        <!-- Optional, used for defaulting if the parameter "service" is not provided in the front API request to PIQ.
        	 Possible values: CHECKOUT|QR|JETGO.
        	 For withdrawal, JETGO will translate to "JetonGo Payout" anything else will be considered "Wallet Payout"
        <service>JETGO</service>-->
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>iframe</container>
  <width>600</width>
  <height>630</height>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.jeton.JetonConfig>
```

</details>

### Attributes

| PaymentIQ Backoffice | Description                                                                                                                      |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------|
| apiKey               | Will be provided by Jeton Technical Team to secure payment initialization.                                                       |
| MerchantID           | Will be provided by Jeton Technical Team.                                                                                        |
| service              | Optional accounts configuration, used for defaulting if the parameter "service" is not provided in the front API request to PIQ. |

### Configuring the merchant's Jeton account
To configure the Jeton account an e-mail must be sent to Jeton support requesting to:
* Get the API key.
* Get access to merchant panel.
* Whitelist [PaymentIQ IP addresses](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist).
* Configure the callback URL to:

Test: https://test-api.paymentiq.io/paymentiq/api/jeton/callback

Production: https://api.paymentiq.io/paymentiq/api/jeton/callback

## Payment Flow

Select Jeton payment option and optional service in PaymentIQ Cashier and enter some amount like is shown below.

![](/img/providers/jeton01.png)

Depending on the service selected, you will either be redirected to the Jeton login dialog where username and password should be specified, or presented with a QR-code to be scanned with Jeton Wallet mobile application.

| Checkout                        | JetonGo / QR                    |
|---------------------------------|---------------------------------|
| ![](/img/providers/jeton02.png) | ![](/img/providers/jeton05.png) |

For Checkout in test, the log in details are email `udo@jeton.com` and password `P@ssw0rd`, and then enter SMS PIN code `123456`. For JetonGo/QR service follow the instructions in the mobile application.

![](/img/providers/jeton03.png)

Press Pay button to complete payment and return back to PaymentIQ Cashier

![](/img/providers/jeton04.png)

## Example Routing Rule
![](/img/providers/routing/jeton.png)

## Test Information

- UserId: 05250831
- Password: P@ssw0rd
- Code: 123456
