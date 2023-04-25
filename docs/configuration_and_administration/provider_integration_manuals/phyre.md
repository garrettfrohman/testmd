--- 
id: "phyre" 
title: "Phyre"
hide_title: "true"
---
 
![](/img/providers/logos/phyre.png)

# Phyre

## About
Phyre is an e-wallet payment provider offering deposit, withdrawal and refund.

| Provider Name                | Phyre                                             |
|------------------------------|---------------------------------------------------|
| Link                         | [https://phyreapp.com/](https://phyreapp.com/)    |
| Classification               | Wallet                                            |
| Regions                      | Europe                                            |
| Currencies                   | `BGN`, `EUR`                                      |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `PhyreWithdrawal`, `Refund` |
| PaymentIQ Configuration File | `PhyreConfig`                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.phyre.PhyreConfig>
  <enabled>true</enabled>
  <width>400</width>
  <height>300</height>
  <container>window</container>
  <testMode>true</testMode>
  <expiresAfter>5</expiresAfter>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
        <apiKey>???</apiKey>
        <!-- bank statements for deposit refund and credit -->
        <defaultDescriptor>Deposit</defaultDescriptor> <!-- bank statements for deposit -->
        <shortDescription>refund</shortDescription><!-- bank statements for refund -->
        <longDescription>credit</longDescription><!-- bank statements for credit -->
        <httpClientConfigEntry>
          <urlPattern>.*web-pay.phyreapp.com*</urlPattern>
          <viqProxy>false</viqProxy>
          <useClientCert>true</useClientCert>
          <clientCertPem>
          </clientCertPem>
          <clientCertKey>
          </clientCertKey>
        </httpClientConfigEntry>
        <!-- optional-->
        <!--<supportedCurrencies>BGN|EUR</supportedCurrencies>-->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.phyre.PhyreConfig>
```
</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                                 |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId        | Corresponds to `Merchant id` from Phyre.                                                                                                                                                                    |
| apiKey            | Corresponds to `API Keyt` from Phyre .                                                                                                                                                                      |
| expiresAfter      | The time for QR code to expire in minutes. Should take a value between 1 and 1440 (from 1 minute to 1 day).                                                                                                 |
| defaultDescriptor | The text that will appear on customer bank statement for deposit. It should be a string with length between 1 and 2048 characters                                                                           |
| shortDescription  | The text that will appear on customer bank statement for refund, along with paymentIq txId. It should be a string with length between 1 and 2048 characters                                                 |
| longDescription   | The text that will appear on customer bank statement for withdrawal.It should be a string with length between 1 and 2048 characters                                                                         |
| doDefaultRedirect | Has boolean value.The default value is false. If set to true, the user will be returned a URI directly from the bank. It should take the value false for UK payments account and true for European payments |
| useClientCert     | It should always be sett to true,it indicates if a cert should be used for withdrawal.                                                                                                                      |
| clientCertPem     | The certificate needed for withdrawal. Paste the content of the fullCerificate.pem file that the merchant recieved from Phyre team                                                                          |
| clientCertKey     | The certificate needed for withdrawal. Paste the content of the privateKey.pem file that the merchant recieved from Phyre team                                                                              |

## Example Routing Rules
![](/img/providers/routing/phyre.png)

### Callback URL
Please ask Phyre to configure "callback" URL:

#### TEST
https://test-api.paymentiq.io/paymentiq/api/phyre/callback

#### PRODUCTION
https://api.paymentiq.io/paymentiq/api/phyre/callback

## Test Information  

NOTE: Phyre doesn't have a TEST or SANDBOX environment and due to this testing should be done with PROD account settings and real wallet account on one of following wallets.
- Phyre
- A1 Wallet
- Pay by VIVACOM
- B@CB Pay

### Deposit
- The customer initiate a payment by entering the amount on cashier then ,In case the customer uses your web site or web app on a device that hasn't got phyre support, e.g. a Desktop PC, laptop, or tablet, the customer will be redierected to a page to scan qr code using his/her smart phone.
  In case the customer is on a smartphone, he/she will be redirected to the relevant phyre screen, if phyre is installed or to the respective app store for phyre to be installed.

### Withdrawal
 NOTE: TLS certificat is needed for withdrawal.The merchant need to ask Phyre team to provide it.
- To make a withdrawal the customer need to enter the following 1. the amount he/she want to withdraw 2. the wallet he want to use for withdrawal 3. the phone number registered on his/her wallet account including the country code.


