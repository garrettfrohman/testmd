--- 
id: "yacare" 
title: "Yacare"
hide_title: "true"
---
 
![](/img/providers/logos/yacare.png)

# Yacare

## About
Yacare is an Argentinian provider that provides WebRedirectDeposits for Argentina.

| Provider Name                | Yacare                                     |
|------------------------------|--------------------------------------------|
| Link                         | [https://yacare.com/](https://yacare.com/) |
| Classification               | Wallet                                     |
| Regions                      | `Argentina`                                |
| Currencies                   | `ARS`                                      |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                       |
| PaymentIQ Configuration File | `YacareConfig`                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.yacare.YacareConfig>
    <enabled>true</enabled>
    <expirationTimeInMinutes>??</expirationTimeInMinutes>
    <accounts>
        <entry>
            <string>YACARE_TEST</string>
            <account>
                <merchantId>??</merchantId>
                <defaultDescriptor>??</defaultDescriptor>
                <apiToken>??</apiToken>
                <supportedCurrencies>ARS</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.yacare.YacareConfig>
```

</details>

### Attributes

| Attribute                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| expirationTimeInMinutes     | Defines expiration time in minutes - if the payment order has not been paid by the end of the expiration time, the transaction status can change to two different values. If the order received payment attempts but these were rejected by management entities of said payment means, the status changes to rejected ‘Rechazada’, if it didn’t receive any payment attempts then the status changes to expired ‘Expirada’ automatically. <br/> The default value is set to 5 minutes. |
| account.merchantId          | It is used as a query param while sending deposit requests. This value is provided by Yacare for each merchant individually.                                                                                                                                                                                                                                                                                                                                                           |
| account.defaultDescriptor   | It is used in requests as "items.name" parameter and can be an arbitrary string.                                                                                                                                                                                                                                                                                                                                                                                                       |
| account.apiToken            | It is used in requests as an authorization header - the details about obtaining it are described below this table.                                                                                                                                                                                                                                                                                                                                                                     |
| account.supportedCurrencies | Yacare works only with ARS, therefore it is important to set ARS here.                                                                                                                                                                                                                                                                                                                                                                                                                 |

### Note
In order to obtain your apiToken, please follow these steps:

1. Log in to your Yacare merchant account - for production environment use https://apps.yacare.com/#/login and for test
environment https://demo.yacare.com.ar/yacare-web/#/login.
2. Click on "Mi perfil".
3. Your API key is located in the "Código de seguridad" section - please copy it and use it as your apiToken in the configuration.

## Provider Configuration

1. Run PaymentIQ and add the aforementioned Point66Config under Admin -> Configuration.
2. Add Yacare to the `<psp>` section in MerchantConfig under Admin -> Configuration.
3. Add routing rules - see example below.
4. Enable WEBREDIRECT deposit method in Rules -> Payment methods.

## Example Routing Rule

![](/img/providers/routing/yacare.png)

## Transaction Flow

In order to make a deposit, the user has to have a registered Yacare user's account and your merchant Yacare account has
to be active. The user's email address has to match with the one that is registered in her/his Yacare account.

1. The user enters the amount in the Cashier.
2. PaymentIQ sends a deposit request to the PSP.
3. In case the request has been processed successfully, the user gets redirected to the Yacare dashboard where he/she
   follows the instructions to complete the payment.
4. The user gets redirected back to the Cashier.
5. PaymentIQ checks the transaction status against the PSP's API.
6. In case the transaction is pending, PaymentIQ awaits for a callback from Yacare. Once it has arrived and valid, 
   PaymentIQ checks the transaction status against the PSP's API again and updates the status accordingly to the result.

## Test Information

The credentials for Yacare dashboard should be provided by Yacare's technical support.
Two types of accounts have to be provided:
1. A merchant's account - this type of account will be used by the merchant to manage and review transactions.
2. A customer's account - this type account will be used by the customer to manage her/his own transactions.
