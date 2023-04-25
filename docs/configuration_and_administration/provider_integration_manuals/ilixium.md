--- 
id: "ilixium" 
title: "Ilixium"
hide_title: "true"
---
 
![](/img/providers/logos/ilixium.png)

# Ilixium

## About
Ilixium is a credit card and wallet provider supporting deposits and withdrawals.

| Provider Name                | Ilixium                                                                                                  |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.ilixium.com/](https://www.ilixium.com/)                                                     |
| Classification               | Debit/Credit Card Processor, Wallet                                                                      |
| Regions                      | `International`                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `WebRedirectDeposit`<br/> `IlixiumWalletWithdrawal` |
| PaymentIQ Configuration File | `IlixiumConfig`                                                                                          |

### PinPay
Ilixium have a wallet solution called PinPay that supports PayPal, Skrill, Ideal, Sofort and Animeexchange.

PaymentIQ currently supports Ideal, Sofort and Animeexchange.

Wallet deposits are made with PaymentTxType WebRedirectDeposit.

Some wallets also supports withdrawals using PaymentTxType IlixiumWalletWithdrawal. To do a wallet withdrawal the user must have done a previous successful deposit. For PIQ to find the correct deposit, the account config parameter `<sourceAccount>` must be set to the name of the account that was used for deposits.

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

Example configuration with both wallet and credit card accounts.

```xml
<com.devcode.paymentiq.integration.ilixium.IlixiumConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <!-- animeexchange account -->
      <string>animeexchange</string>
      <account>
        <accountID>??????</accountID>
        <merchantId>??????</merchantId>
        <password>??????</password>
        <container>iframe</container>
        <supportedCurrencies>JPY</supportedCurrencies>
        <useSimplifiedWalletApi>true</useSimplifiedWalletApi>
        <sourceAccount>animeexchange</sourceAccount>
      </account>
    </entry>
    <entry>
      <!-- ideal wallet account -->
      <string>Ideal</string>
      <account>
        <accountID>??????</accountID>
        <merchantId>??????</merchantId>
        <password>??????</password>
        <container>iframe</container>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <!-- Sofort wallet account -->
      <string>Sofort</string>
      <account>
        <accountID>??????</accountID>
        <merchantId>??????</merchantId>
        <password>??????</password>
        <container>iframe</container>
        <supportedCurrencies>USD|EUR|GBP|CAD</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <!-- credit card non 3DS -->
      <string>N3DS</string>
      <account>
        <accountID>??????</accountID>
        <merchantId>??????</merchantId>
        <password>??????</password>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>
    <entry>
      <!-- credit card 3DS -->
      <string>3DS</string>
      <account>
        <accountID>??????</accountID>
        <merchantId>??????</merchantId>
        <password>??????</password>
        <use3Dsecure>true</use3Dsecure>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ilixium.IlixiumConfig>  
```


</details>

### Attributes

| Attribute                               | Description                                                                                                                                        | Level          | Type       |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------|
| previousAuth                            | If you want PaymentIQ to send reference to the last deposit when doing withdrawal                                                                  | account config | CreditCard |
| txHistoryDelayHours                     | When using previousAuth, you can set how many hours in transaction history you want to STOP search for last deposit. Default is 24, 0 means today. | root           | CreditCard |
| withdrawalCheckDepositAgainstPspAccount | When using previousAuth, you can set a specific PSP account that the deposit should have been done with. Default is empty.                         | root           | CreditCard |
| useSimplifiedWalletApi                  | Use a new faster wallet flow. Default is false.                                                                                                    | account config | Wallet     |
| sourceAccount                           | For wallet withdrawals. Set to the name of the account config that was used for deposits.                                                          | account config | Wallet     |
| handleStatusAsSuccess                   | For wallet deposits. Specify which status numbers should be treated as success.                                                                    | account config | Wallet     |

:::note

It is recommended to use the Ilixium wallet solution inside an iframe.

That's why you need to add configuration `<container>iframe</container>` either on the account level or on the root level.
If you have configuration for both wallet and credit card you should add the container configuration on account level.

This means that you may need to change your cashier to handle the fact that Ilixium needs to be called from an iframe or overlay.

:::

### Wallet configuration

Add this in `MerchantConfig` to get Ideal and Sofort for the Wallet.

```xml
  <entry>
    <string>WEBREDIRECT</string>
    <string>SOFORT|IDEAL</string>
  </entry>
```

## Wallet user information
Ideal users must have the country code NLD.

Sofort users must have the country code DEU.

Animeexchenge users must have country code JPN and use currency JPY.

## Example Routing Rule
![](/img/providers/routing/ilixium.png)

### Example Wallet Routing Rule

![](/img/providers/routing/ilixium_ideal.png)

![](/img/providers/routing/ilixium_sofort.png)

## Test Information

### 3DS Test Cards

| Card number         | description                                                  |
|---------------------|--------------------------------------------------------------|
| 4012001036275556    | No Response From Visa Directory Server                       |
| 4012001038443335    | Cardholder Not Participating                                 |
| 4012001038488884    | Unable to Verify Enrollment                                  |
| 4012001036298889    | Invalid Response from Directory Server                       |
| 4012001036853337    | Invalid ACS Digital Signature                                |
| 4012001036983332    | Expired ACS Signing Certificate                              |
| 4012001037141112    | Successful Authentication via a 16-digit PAN                 |
| 4005559876540       | Successful Authentication via a 13-digit PAN                 |
| 4012010000000000009 | Successful Authentication via a 19-digit PAN                 |
| 4012001037167778    | Successful "Merchant Attempt" via a 16-digit PAN             |
| 4012001037461114    | Authentication Failure                                       |
| 4012001037484447    | Authentication Not Available                                 |
| 4012001037490006    | Invalid Payer Authentication Response                        |
| 4012001037490014    | Valid 3-D Secure Message With Embedded Whitespace Characters |

In order to test a decline response, the amount should be set to 10.00 and the CVV2 value should be 999. Using the value 9.00 will also return a decline response.
Use CVV2 123 for success response.

### Wallet

| Provider | Bank name | Account number | PIN   |
|----------|-----------|----------------|-------|
| Sofort   | 88888888  | 12340987       | 12345 |
| Ideal    | Testbank  | 88888888       | 1234  |

#### Anime Exchange
In test, currency GBP and country GBR must be used.
