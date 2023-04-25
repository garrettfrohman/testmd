--- 
id: "securetrading"
title: "Secure Trading (Trust Payments)"
hide_title: "true"
---

![](/img/providers/logos/securetrading.png)

# Secure Trading (Trust Payments)

## About
Secure-Trading is a Payment Solution Provider which is one of the worldwide market leaders in online prepaid payment methods At the time SecureTrading provides creditcard and APM solutions.

| Provider Name                | Trust Payments                                                                                                                                             |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.securetrading.com](https://www.securetrading.com)                                                                                             |
| Classification               | Debit/Credit Card Processor, Aggregator                                                                                                                    |
| Regions                      | `International`                                                                                                                                            |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                            |
| Methods/PaymentTxTypes       | `SecureTradingDeposit`<br/> `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `GooglePayDeposit`<br/> `Refund`<br/> `Void`<br/> `PaysafecardWithdrawal` |
| PaymentIQ Configuration File | `SecureTradingConfig`                                                                                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
```xml
<com.devcode.paymentiq.integration.securetrading.SecureTradingConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <testMode>true</testMode>
    <defaultDescriptor>Test payment description</defaultDescriptor>
    <allowToCancelPtxOnRedirect>true</allowToCancelPtxOnRedirect>
    <accounts>
        <entry>
            <string>APM</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <profileId>default</profileId> <!--stprofile parameter-->
                <username>??</username>
                <password>??</password>
                <siteReference>??</siteReference> <!--sitereference parameter-->
                <serviceEndpoint>https://webservices.securetrading.net/json/</serviceEndpoint>
                <notificationPassword>??</notificationPassword><!--notification password that is configured at Secure Trading account-->
                <supportedCurrencies>??</supportedCurrencies>
                <forcePayment>??</forcePayment>
                <jwtUser>??</jwtUser>
                <jwtSecret>??</jwtSecret>
            </account>
        </entry>
        <entry>
            <string>cc_default_3DS</string>
            <account>
                <use3Dsecure>true</use3Dsecure>
                <siteId>??</siteId> <!--stprofile parameter-->
                <username>??</username>
                <password>??</password>
                <serviceEndpoint>https://webservices.securetrading.net:443/xml/</serviceEndpoint>
                <supportedCurrencies>EUR|GBP|USD</supportedCurrencies>
                <useTokenId>false</useTokenId>
            </account>
        </entry>
        <entry>
            <string>cc_default_N3DS</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <siteId>??</siteId> <!--stprofile parameter-->
                <username>??</username>
                <password>??</password>
                <serviceEndpoint>https://webservices.securetrading.net:443/xml/</serviceEndpoint>
                <supportedCurrencies>EUR|GBP|USD</supportedCurrencies>
                <useTokenId>true</useTokenId>
            </account>
        </entry>
    </accounts>

    <redirectUrl>${baseRedirectUrl}/api/securetrading/deposit/redirect/${ptx.txRefId}</redirectUrl>
    <redirectFailureUrl>${baseRedirectUrl}/api/securetrading/deposit/redirect/${ptx.txRefId}</redirectFailureUrl>
    <proceedUrl>${baseRedirectUrl}/api/securetrading/googlepay/proceed/${ptx.txRefId}</proceedUrl>
</com.devcode.paymentiq.integration.securetrading.SecureTradingConfig>

```

</details>

### Attributes

| Attribute                  | Description                                                                    |
|----------------------------|--------------------------------------------------------------------------------|
| profileId                  | stprofile (created in MyST)                                                    |
| username                   | WebService details (created in MyST)                                           |
| password                   | WebService details (created in MyST)                                           |
| siteReference              | sitereference parameter (provided by SecureTrading)                            |
| allowToCancelPtxOnRedirect | allow update transaction status immediately after user cancelled payment       |
| forcePayment               | specify default APM should be used in case no service available in the request |
| notificationPassword       | notification password that is configured at Secure Trading account             |
| defaultDescriptor          | defines the descriptor sent to the provider, will default to "Bambora payment" |
| jwtUser                    | JWT username (provided by SecureTrading)                                       |
| jwtSecret                  | JWT Secret Key (provided by SecureTrading)                                     |

### Notes

- For SafetyPay, QIWI and Paysera it's required to configure TxType specifying according service

### GooglePay

To configure GooglePay via SecureTrading, you need to request SiteReference and associated JwtUsername & Jwt Secret Key from SecureTrading Support team.

When you have these you need to add them to the account in SecureTradingConfig as follows -

```xml
<com.devcode.paymentiq.integration.securetrading.SecureTradingConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <testMode>true</testMode>
    <defaultDescriptor>Test payment description</defaultDescriptor>
    <allowToCancelPtxOnRedirect>true</allowToCancelPtxOnRedirect>
    <accounts>
        <entry>
            <string>GooglePay</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <profileId>default</profileId> <!--stprofile parameter-->
                <username>??</username>
                <password>??</password>
                <siteReference>??</siteReference> <!--sitereference parameter-->
                <serviceEndpoint>https://webservices.securetrading.net/json/</serviceEndpoint>
                <notificationPassword>??</notificationPassword><!--notification password that is configured at Secure Trading account-->
                <supportedCurrencies>??</supportedCurrencies>
                <forcePayment>??</forcePayment>
                <jwtUser>jwtUser_XXXX</jwtUser>
                <jwtSecret>jwtSecret_XXXX</jwtSecret>
            </account>
        </entry>
    </accounts>
    <redirectUrl>${baseRedirectUrl}/api/securetrading/deposit/redirect/${ptx.txRefId}</redirectUrl>
    <redirectFailureUrl>${baseRedirectUrl}/api/securetrading/deposit/redirect/${ptx.txRefId}</redirectFailureUrl>
    <proceedUrl>${baseRedirectUrl}/api/securetrading/googlepay/proceed/${ptx.txRefId}</proceedUrl>
</com.devcode.paymentiq.integration.securetrading.SecureTradingConfig>
``` 
Also, update the GooglePayConfig file and add the siteReference value as gatewayMerchantId -

```xml
<com.devcode.paymentiq.integration.googlepay.GooglePayConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <gateway>trustpayments</gateway>
  <gatewayMerchantId>SiteReference_XXXX</gatewayMerchantId>
  <merchantId>???</merchantId>
  <merchantName>???</merchantName>
</com.devcode.paymentiq.integration.googlepay.GooglePayConfig>
```

### ApplePay

:::note
Only works with Safari browser
:::

ApplePay via SecureTrading is supported as SecureTradingDeposit (not as ApplePayDeposit, as on some other providers).
To configure ApplePay via SecureTrading please follow the below steps:

1. First you need to update the default.css file to hide other payment options. This is needed as ApplePay is integrated as a Payment Page on Secure Trading. The easiest way to update the file is to copy below code and save it as default.css, then upload it to your SecureTrading account. You can do this under the file manager menu.
```css
#st-block-standardpaymentchoicesdiv,
span.st-wallet-hr,
#st-google-pay,
#st-block-standard-paymentchoice > p:nth-child(4),
#st-block-standard-paymentchoice > h2:nth-child(1){
  display:none
}
```
2. Then you need to reach out to the Secure Trading Support Team and ask them to enable SiteSecurity and to include this field combination currencyiso3a+mainamount+sitereference+sitesecuritytimestamp+notificationPassword

### PaySafeCard

From Secure-Trading PaySafeCard you need to request a MyST account where you will receive your own credentials (username/password) as well as your site reference (i.e. test_devcode66006). Then, you will configure your account as following:

1. At User Details:

![](/img/providers/securetrading01.png)

Add a new user with WebServices role and whitelist the IPs in [Provider IP Whitelisting](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist)

Then, use this new user credentials (username/password) to configure your PaymentIQ SecureTradingConfig xml as following.

```xml
<username>??</username>
<password>??</password>
<siteReference>??</siteReference>
```

2. Configure the Notification at your account as following:
* Go the notification page
  ![](/img/providers/securetrading02.png)

* Add filter
  ![](/img/providers/securetrading03.png)

* Add destination with following details. You can change the password as you want. Also, you need to make sure that only the following fields are checked: errorcode, orderreference, paymenttypedescription, requestreference, settlementstatus, sitereference and transactionreference

![](/img/providers/securetrading04.png)

* Then configure the following tags:
```xml
<!--notification password that is configured at Secure Trading account-->
<notificationPassword>??</notificationPassword>
```

3. Supported currencies at time being are: ARS, AUD, BGN, CAD, CHF, CZK, DKK, EUR, GBP, HRK, HUF, MXN, NOK, NZD, PEN, PLN, RON, SEK, TRY, USD, UYU

Therefore, you will need to make sure that you are using only those that are supported by Secure-Trading/PaySafecard. Configure as following:

```<supportedCurrencies>EUR|SEK</supportedCurrencies>```

### SafetyPay:
```<supportedCurrencies>EUR|USD</supportedCurrencies>```

Supported Billing countries addresses:
Austria (AT), Belgium (BE), Chile (CL), Colombia (CO), Costa Rica (CR), Ecuador(EC), Germany (DE), Mexico (MX), Netherlands (NL), Peru (PE), Puerto Rico (PR) and Spain (ES)

### QIWI:
```<supportedCurrencies>EUR|KZT|RUB|USD</supportedCurrencies>```

Supported Billing countries addresses:
Kazakhstan (KZ), Russia (RU) and Ukraine (UA)

### Paysera:
```<supportedCurrencies>EUR</supportedCurrencies>```

Supported Billing countries addresses:
Estonia (EE), Lithuania (LT) and Latvia (LV)

### Paypal:
```<supportedCurrencies>AUD|CAD|EUR|GBP|JPY|USD</supportedCurrencies>```

Supported Billing countries: No restrictions

### paysafecard:
```<supportedCurrencies>ARS|AUD|BGN|CAD|CHF|CZK|DKK|EUR|GBP|HRK|HUF|MXN|NOK|NZD|PEN|PLN|RON|SEK|TRY|USD|UYU</supportedCurrencies>```

Supported Billing countries addresses: No restrictions

### EPS:
```<supportedCurrencies>EUR</supportedCurrencies>```

Supported Billing countries addresses: Austria (AT)

### Bancontact:
```<supportedCurrencies>EUR</supportedCurrencies>```

Supported Billing countries addresses: Belgium (BE)

In Secure-Trading BO (Notification management - step 3), you will need to fix the callback url.

| Callback URLs |                                                                            |
|---------------|----------------------------------------------------------------------------|
| Test          | https://test-api.paymentiq.io/paymentiq/api/securetrading/deposit/callback |
| Production    | https://api.paymentiq.io/paymentiq/api/securetrading/deposit/callback      |

Here is a link on how to create the notifications/webhooks:
[https://help.trustpayments.com/hc/en-us/articles/4402689992593-Configure-webhooks?source=search](https://help.trustpayments.com/hc/en-us/articles/4402689992593-Configure-webhooks?source=search)


## Transaction Flow

The customer journey is the following:

1. The customer inserts as many 16 digits PINs as needed in order to cover the required deposit amount.
2. The customer clicks on the BUY button.
3. After successful purchase, the payment is completed and the client is redirected to the success/failure page.

### SafetyPay:
1. Input amount
2. Press Deposit button
3. Finish bank flow to be redirected to success/failure page

### QIWI:
1. Input amount and phone number
2. Press Deposit button
3. Finish QIWI flow to be redirected to success/failure page

### Paysera:
1. Input amount
2. Press Deposit button
3. Finish Paysera flow to be redirected to success/failure page

## Example Routing Rule
![](/img/providers/routing/securetrading.png)

## Test Information

16 digit PIN for testing
PIN: 0000009861101185
Currency: EUR
Max balanace: 100 EUR

### Safetypay
Any dummy data (even empty fields) will work for testing purposes

### paysafecard

PIN: 0000 0000 0990 0828

### QIWI, Paysera:
No special instructions required

### Creditcard

| Card Brand | Account          | CVV | Expiry date | Result/Info  |
|------------|------------------|-----|-------------|--------------|
| VISA       | 4111110000000211 | Any | Any         | 3DS enrolled |
| VISA       | 4111110000000021 | Any | Any         | 3DS enrolled |
| MASTERCARD | 5100000000000511 | Any | Any         | Enrolled     |
