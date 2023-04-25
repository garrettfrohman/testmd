--- 
id: "paywize" 
title: "Paywize"
hide_title: "true"
---
 
![](/img/providers/logos/paywize.png)

# Paywize

:::warning UPDATE

Please note that as of 2021-09-01 Paywize is discontinued.

As Paywize is a whitelable provider for Payneteasy you can potentially continue to use the integration by changing endpoint and credentials. Please check directly with Payneteasy for more information.

Please note that we are currently upgrading our Payneteasy integration to make sure the same txTypes are supported as we did for the Paywize integration.

:::

## About
Paywize is a credit card provider that offers 3DS and N3DS deposit (sale, authorization + capture), recurring, void, refund, withdrawal and status check.

| Provider Name                | Paywize                                                                                                            |
|------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.paywize.com/](https://www.paywize.com/)                                                               |
| Classification               | Debit/Credit Card Processor                                                                                        |
| Regions                      | `International`                                                                                                    |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                    |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Capture`<br/> `Void`<br/> `WebRedirectDeposit` |
| PaymentIQ Configuration File | `PaywizeConfig`                                                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paywize.PaywizeConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>3DS</string>
      <account>
        <username>??</username><!--Login-->
        <password>??</password>
        <merchantCode>??</merchantCode> <!-- Merchant Control -->
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>true</useTokenId>
        <authType>AUTH_CAPTURE</authType>
        <supportedCurrencies>EUR</supportedCurrencies>
        <hasGroupId>true</hasGroupId>
        <groupId>??</groupId><!--Endpoint ID-->
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <username>??</username><!--Login-->
        <password>??</password>
        <merchantCode>??</merchantCode> <!-- Merchant Control -->
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
        <authType>AUTH_CAPTURE</authType>
        <supportedCurrencies>EUR</supportedCurrencies>
        <hasGroupId>true</hasGroupId>
        <groupId>??</groupId><!--Endpoint ID-->
      </account>
    </entry>
    <entry>
      <string>PAYOUT</string>
      <account>
        <username>??</username><!--Login-->
        <password>??</password>
        <merchantCode>??</merchantCode> <!-- Merchant Control -->
        <!--secretKey is required for Payout only-->
        <secretKey>##</secretKey>
        <supportedCurrencies>EUR</supportedCurrencies>
        <hasGroupId>true</hasGroupId>
        <groupId>??</groupId><!--Endpoint ID-->
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <defaultDescriptor>??</defaultDescriptor><!--Order Description-->
</com.devcode.paymentiq.integration.paywize.PaywizeConfig>
```

</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                                                    |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username          | Corresponds to the User Login from Paywize                                                                                                                                                                                     |
| password          | Corresponds to the User Password from Paywize                                                                                                                                                                                  |
| merchantCode      | Corresponds to the Merchant Control from Paywize. It is used to generate request signature                                                                                                                                     |
| groupID           | Corresponds to the End Point ID from Paywize. It is an entry point for incoming Merchant’s transactions                                                                                                                        |
| useTokenId        | To enable recurring please specify `useTokenId=true`                                                                                                                                                                           |
| use3Dsecure       | To enable 3DS please specify `use3Dsecure=true`                                                                                                                                                                                |
| hasGroupId        | Should be set to `true` on account level                                                                                                                                                                                       |
| doDefaultRedirect | Set to true if redirect should not trigger a status check and instead wait for the callback. For WebRedirectDeposit methods (JPay) where the amount might change after initial redirect and needs to be set from the callback. |

### Notes
- Each operation 3DS, N3DS deposit or payout has its own "Endpoint ID"
- For Payout we (not merchant) have to generate RSA public and private keys, then provide public key to Paywize and specify private key instead of "##". It will be used by all the merchants on PROD in order to secure communication between PaymentIQ and Paywize.

### Supported Countries/Currencies
All countries are available. The limitations are configurable at Paywize side (in the BO UI). For currencies - Paywize can configure an additional currency and associate it to the project.

### Min/Max amount
For min/max transaction settings - they are defaulted unrestricted, but can be set based on merchant requirements at Paywize side (in the BO UI).

## Example Routing Rules
![](/img/providers/routing/paywize.png)

### ISignThis
![](/img/providers/routing/paywize02.png)

Note: It's possible that transaction will require KYC verification by uploading additional documents etc.
In this case it's important to ensure possibility of returning to transaction.

Using Bambora Cashier it can be done by navigating to `All transactions` and clicking on `Complete your transaction`

![](/img/providers/routing/paywize_pending.png)

Otherwise, it's possible to fetch `continueLink` through the `User Transaction` API call
```/api/user/transaction/{merchantId}/{userId}?sessionId={sessionId}```

## Test Information

### Credit cards

| Card type | Number              | CVV |
|-----------|---------------------|-----|
| Visa N3DS | 4111 1111 1111 1111 | Any |
| Visa 3DS  | 4455 5555 5555 5544 | Any |


### ISignThis test card

5420223448164060
Exp: 02/22
3DS Scenario: Successful
Reset Identity: Yes
OTP: 1111-1111
