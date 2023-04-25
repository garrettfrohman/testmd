--- 
id: "maxpay" 
title: "Maxpay"
hide_title: "true"
---
 
![](/img/providers/logos/maxpay.png)

# Maxpay

## About
Maxpay is a financial ecosystem for real-time payment processing.

PaymentIQ support 4 Maxpay flows:
1. SEPA payouts (`MaxpayBankIBANWithdrawal`) allows possibility to withdraw funds from Maxpay account.
2. H2H: Host to host API (`CreditcardDeposit`, `Refund`, `Void`, `Capture`). Full card integration with 2D and 3DS flows and authorization options.
3. HPP: Hosted payment pages (`WebRedirectDeposit`, `Refund`). Allows possibility to deposit account using Maxpay Payment form.  
4. Credit card withdrawals (`CreditcardWithdrawal`) allows possibility to withdraw funds from Maxpay account.

| Provider Name                | Maxpay                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://maxpay.com/](https://maxpay.com/)                                                                                                         |
| Classification               | Wallet                                                                                                                                             |
| Regions                      | `International`                                                                                                                                    |
| Currencies                   | `EUR`, `USD`, `GBP`                                                                                                                                |
| Methods/PaymentTxTypes       | `MaxpayBankIBANWithdrawal`<br/> `WebRedirectDeposit`<br/> `CreditcardDeposit`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `CreditcardWithdrawal` |
| PaymentIQ Configuration File | `MaxpayConfig`                                                                                                                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.maxpay.MaxpayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>SEPA</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
      </account>
    </entry>
    <entry>
      <string>OCT</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <useTokenId>???</useTokenId>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
      </account>
    </entry> 
    <entry>
      <string>H2H</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <useTokenId>true</useTokenId>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
      </account>
    </entry>
    <entry>
      <string>HPP</string>
      <account>
        <productName>name_to_display</productName>
        <supportedCurrencies>EUR</supportedCurrencies>
        <secretKey>???</secretKey>
        <pspPublicKey>???</pspPublicKey>
        <refundSecretKey>???</refundSecretKey>
        <container>window</container>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.maxpay.MaxpayConfig>
```

</details>

### Attributes

| Attribute            | Description                                                                                                                                                                                |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username             | merchant account(Provided by Maxpay)                                                                                                                                                       |
| password             | merchant password(Provided by Maxpay)                                                                                                                                                      |
| secretKey(SEPA, H2H) | secret key(Provided by Maxpay). Used for callback signature validation. If blank - signature validation will be skipped                                                                    |
| useTokenId           | boolean that allows payment by token for stored user accounts. When set to ```true``` value could be that in case successful 3DS payment next payment will be by token without 3DS actions |
| productName          | name of product that will be displayed on payment form. If blank - defaults to transaction ID                                                                                              |
| secretKey(HPP)       | secret key(Maxpay Merchant Portal: ```Payment Pages>Payment Page>General```). See below detailed ```HPP setup``` instruction                                                               |
| pspPublicKey         | public key(Maxpay Merchant Portal: ```Payment Pages>Payment Page>General```). See below detailed ```HPP setup``` instruction                                                               |
| refundSecretKey      | secret key for refunds (Maxpay Merchant Portal: ```Payment Pages>Payment Forms>Edit (Embed Code section)```). See below detailed ```HPP setup``` instruction                               |
| transactionLength    | period after transaction will be settled on Maxpay side. Applyible for HPP Authorization API. Value is in ```Days```. Defaults to 1. More info under ```HPP setup``` instruction           |

### HPP setup

Note: HPP works with```<container>window</container>```. 
1. To use HPP merchants have to be registered on Maxpay Merchant portal https://my.maxpay.com/.
2. Navigate to Payment pages section and create new instance
3. Under Settings populate all required fields. <br/>
   Important: Callback URLs should be:<br/>
   Production: ``` https://api.paymentiq.io/paymentiq/api/maxpay/hpp/callback``` <br/>
   Test: ``` https://test-api.paymentiq.io/paymentiq/api/maxpay/hpp/callback```. <br/>
   Redirect URL's:<br/>
   Production: ```https://api.paymentiq.io/paymentiq/api/maxpay/redirect``` <br/> 
   Test: ```https://test-api.paymentiq.io/paymentiq/api/maxpay/redirect``` <br/>
4. On the next page you generate the public and secret key to use in the config fields as ```pspPublicKey``` and ```secretKey```.
5. Navigate to Payment forms and create a new one. Here you can configure view of Payment form
6. Under ```EMBED CODE``` section you will find signature that has to be set as ```refundSecretKey```

Note: HPP uses custom product API (product name can be configured using ```productName```) with possibility to enable Authorization API by ```authType``` property .
Due to limitations (not possible to get updates from Maxpay side about next SETTLE/VOID actions) Authorization API allows only SETTLE that will happen after ```transactionLength```.
In case of success transaction using Authorization API PaymentIQ will consider transaction as successful and finalized. Maxpay is responsible for transaction ```SETTLE``` after ```transactionLength```
Refunds, using Authorization API, will be possible only from Maxpay Merchant portal as PaymentIQ won't have info about settled transaction ID.


## Example Routing Rule
### SEPA
![](/img/providers/routing/maxpay.png)

### H2H
![](/img/providers/routing/maxpay_h2h.png)

### HPP
![](/img/providers/routing/maxpay_hpp.png)


## Test Information

SEPA payout doesn't have test environment

Test cards for HPP and H2H

| Card Brand | Supporting Flow | Card number      | CVV                   | Expiry Date                                 |
|------------|-----------------|------------------|-----------------------|---------------------------------------------|
| Visa       | 2D              | 4111111111111111 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |
| Mastercard | 2D              | 5555555555554444 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |
| Visa       | 3D              | 4012000300001003 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |
| Mastercard | 3D              | 5191330000004415 | 123 [3 digits random] | MM - [from 01 to 12]; YYYY- 2020 or greater |