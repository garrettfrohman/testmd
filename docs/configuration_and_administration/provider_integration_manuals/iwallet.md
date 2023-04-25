--- 
id: "iwallet" 
title: "iWallet"
hide_title: "true"
---
 
![](/img/providers/logos/iwallet.png)

# iWallet

## About
To create a transaction, customer can click the "iWallet" link on the merchant's website and they will be advised to login to their iWallet account. Customer needs to choose the currency and click Confirm. Then the amount with the designated value will be automatically paid to the correspondent iWallet account of the Merchant. The payments will be completed immediately and redirected a real-time callback URL.

| Provider Name                | iWallet                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://iwl.hk/](https://iwl.hk/)                                              |
| Classification               | Online Banking                                                                  |
| Regions                      | `Japan`, `Malaysia`, `Singapore`                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `IWalletDeposit` <br/> `IWalletWithdrawal`                                      |
| PaymentIQ Configuration File | `iWalletConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.iwallet.IWalletConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
     <string>DEPOSIT</string>
     <account>
       <merchantId>??</merchantId>
       <secretKey>??</secretKey>
       <username>??</username>
       <password>??</password>
        <supportedCurrencies>USD|EUR|GBP|HKD|SGD|JPY|CNY</supportedCurrencies>
        <container>window</container>
     </account>
    </entry>
    <entry>
      <string>WITHDRAW</string>
      <account>
        <password>??</password>
        <merchantId>??</merchantId>
        <sourceAccount>??</sourceAccount>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
        <supportedCurrencies>USD|EUR|GBP|HKD|SGD|JPY|CNY</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>window</container>
 <!-- <width>600</width>
  <height>600</height>-->
  <!-- <liveServiceEndPoint>https://iwallet.paymentiq.io/</liveServiceEndPoint>
  actual endpoint is https://secure.iwl.world/ but iwallet.paymentiq.io is poiting towards that but through proxy which is needed for iWallet to work
  Note: We're deprecating this one since it doesn't seem to work, use the real URL below, and it is the merchants referrer URL IPs that has to be whitelisted with iWallet -->
  <liveServiceEndPoint>https://secure.iwl.world/</liveServiceEndPoint>
  <redirectUrl>${baseRedirectUrl}/api/iwallet/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseCallbackUrl}/api/iwallet/callback/${ptx.txRefId}</callbackUrl>
  <defaultDescriptor>??</defaultDescriptor>
  <settlementExtUrlEng>en/settlement.php</settlementExtUrlEng>
  <settlementExtUrlJap>ja/settlement.php</settlementExtUrlJap>
  <remittanceUrl>https://api.iwl.world/MoneyRequest</remittanceUrl>
</com.devcode.paymentiq.integration.iwallet.IWalletConfig>
```
</details>

### Attributes

| PaymentIQ Backoffice | Description                                                               |
|----------------------|---------------------------------------------------------------------------|
| merchantId           | Provided by the IWallet                                                   |
| secretKey            | Provided by the DevCode/Bambora to secure request that is sent to IWallet |
| username             | Provided by the IWallet to create request signature                       |
| password             | Provided by the IWallet to create request signature                       |

### IP whitelisting
iWallet uses a specific way of whitelisting IP's that is not common for other providers. They are whitelisting the referrer URL's IP's, and this means it's the merchants' referrer URL and not PIQ's URL's that have to be whitelisted. For this, communication with iWallet together with the merchant has to be initiated where the merchant let's iWallet know which URL IP's are used client-side to redirect to the iWallet window. If the merchant is unsure of these, iWallet should be able to investigate on their end what the referrer URL is and from there do a lookup on the IP's.

## Example Routing Rule
![](/img/providers/routing/iwallet.png)

## Test Information
### Deposits

| Username               | Password |
|------------------------|----------|
| RPLtest-user@iwl.world | 9xjanyTX |

### Withdrawals

- Test account: 60148766
