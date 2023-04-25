--- 
id: "ozan" 
title: "Ozan"
hide_title: "true"
---
 
![](/img/providers/logos/ozan.png)

# Ozan

## About
Ozan is E-Wallet provider that offers deposit, refund, withdrawal and status check.

| Provider Name                | Ozan                                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.ozan.com/](https://www.ozan.com/)                                  |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/> `OzanWithdrawal`<br/> `Refund`                        |
| PaymentIQ Configuration File | `OzanConfig`                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ozan.OzanConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>??</username>
        <password>??</password>
        <secretKey>??</secretKey><!--private key-->
        <supportedCurrencies>EUR|USD|GBP</supportedCurrencies>
        <apiKey>??</apiKey><!--public key-->
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <height>670</height>
  <!--<liveServiceEndPoint>https://ozan.com/api</liveServiceEndPoint>
  <testServiceEndPoint>https://sandbox.ozan.com/api</testServiceEndPoint>-->
  <refundRequestTimeout>600</refundRequestTimeout>
  <checkoutHtmlTemplateName>ozan-checkout-template</checkoutHtmlTemplateName>
</com.devcode.paymentiq.integration.ozan.OzanConfig>
```

</details>

### Attributes

| Attribute | Description                                                       |
|-----------|-------------------------------------------------------------------|
| apikey    | Provided by Ozan Technical Team to secure payment initialization. |
| secret    | Provided by Ozan Technical Team to secure payment initialization. |

### Limits
Our limits depend on KYC verification, single transaction upper limit is 10,000 euros (or equivalent in other currency)

## Example Routing Rule
![](/img/providers/routing/ozan.png)

## Test Information

In order to do deposit with Ozan user should specify phone number but without country code (country code will be selected from drop-down) e.g. in case of 447447884021 user should specify 7447884021.
In order to do withdrawal with Ozan user should specify phone number with country code e.g. 447447884021.

### End User Accounts
End user account is used to make purchases, you can use the below end user to perform payments.

| Phone Number | 447447884021 | 447447884121 | 44 7447884028 |
|--------------|--------------|--------------|---------------|
| Password     | ozan123+     | P@ssw0rd     | ozan123$      |