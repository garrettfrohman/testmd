--- 
id: "paramountinterac" 
title: "Paramount Interac"
hide_title: "true"
---
 
![](/img/providers/logos/paramountinteraclogo.png)

# Paramount Interac

## About
The Paramount Commerce Interac® payment service is a secure transaction platform using
cutting-edge risk management technology.

| Provider Name                | Paramount Interac                                                |
|------------------------------|------------------------------------------------------------------|
| Link                         | [https://paramountcommerce.com/](https://paramountcommerce.com/) |
| Classification               | Online Banking                                                   |
| Regions                      | `Canada`                                                         |
| Currencies                   | `CAD`                                                            |
| Methods/PaymentTxTypes       | `BankDeposit`, `ParamountWithdrawal`                             |
| PaymentIQ Configuration File | `ParamountConfig`                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paramountinterac.ParamountConfig>
  <enabled>true</enabled>
<accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>???</merchantId>
        <memberId>???</memberId>
        <password>???</password>
        <secretKey>???</secretKey>
        <supportedCurrencies>CAD</supportedCurrencies>
     </account>
    </entry>
  </accounts>  
  <testMode>true</testMode>
  <waitForWithdrawalNotification>false</waitForWithdrawalNotification>
</com.devcode.paymentiq.integration.paramountinterac.ParamountConfig>
```
</details>

### Attributes

| Attribute           | Description                                         |
|---------------------|-----------------------------------------------------|
| merchantId          | Merchant account ID assigned by Paramount.          |
| memberId            | Merchant sub ID configured and issued by Paramount. |
| password            | Merchant Password issued by Paramount.              |
| secretKey           | Merchant encryption key issued by Paramount.        |
| supportedCurrencies | CAD.                                                |


### Wait For Withdrawal Notifications
The normal scenario is that PaymentIQ sets the withdrawal to success after it has been successfully received by Paramount and waiting for it to be processed. If anything goes wrong during processing a reversal is created. To instead wait with setting success until a notification that the money has reached the user's account can be done by adding this to ParamountConfig:

`<waitForWithdrawalNotification>true</waitForWithdrawalNotification>`

Note that there is always a risk invovled with using this configuration that the merchant needs to be aware of. If anything goes wrong with the transaction (e.g. misconfiguration, human error, connection issues etc) while it is waiting to be processed at the provider that causes PaymentIQ to set it to FAILED means that a cancel will be sent to the merchant. At the same time it is possible that the provider successfully executed it and the user received the money on their end. So be very careful using this setting.


### Callback configuration 

You need to send PIQ callback URLS to Paramount.

Test callback Url : https://test-api.paymentiq.io/paymentiq/api/paramount/callback/

Live callback Url : https://api.paymentiq.io/paymentiq/api/paramount/callback/



## Example Routing Rule
![](/img/providers/routing/paramountinterac2.png)

## Test Information

### Testing Paramount interac outside of Canada
If you are accessing the staging environment from outside Canada, you must use a proxy server for redirection. Details about configuring a proxy server in common web browsers are below.

### Table 1: Proxy server settings

| Setting          | Value                                    |
|------------------|------------------------------------------|
| Username         | guest                                    |
| Password         | IntegratingTesting!                      |
| Proxy server URL | http://proxy.idsmanagement.com/proxy.pac |


#### Configuring Mozilla Firefox

1. Click the menu button and select Options on Windows, or Preferences on a Mac.
2. In the General panel, scroll down to the Network Proxy section and click Settings.
3. Select Automatic proxy configuration URL and enter the proxy server URL.
4. Click OK.

#### Configuring Chrome

1. Click the menu button and select Settings.
2. Scroll to the bottom of the Settings page and expand the Advanced section
3. Scroll down to the System section and click Open proxy settings.
4. Select Connections and click LAN Settings.
5. Do one of the following:
    a. On Windows, select Use automatic configuration script and enter the proxy server URL in Address.
    b. On a Mac, select Automatic Proxy Configuration and enter th eproxy server URL in URL.
6. Click OK.

#### Configuring Safari

1. On the Safari menu, select Preferences.
2. Select the Advanced tab.
3. In the Proxies section, click Change Settings.
4. Select Automatic Proxy Configuration and enter the proxy server URL in URL.
5. Click OK

#### Configuring Explorer

1. Click the configuration button and select Internet options.
2. Select the Connections tab and click LAN settings.
3. Select Use automatic configuration script and enter the proxy server URL in Address.
4. Click OK.

---

### PayIn Testing steps

To initiate a Paramount Interac® test transaction:
1. After transaction is initiated with PIQ, Paramount displays a page that contains five fields of important information.
2. Copy the reference number under Message.
3. Open Email Simulator:
     https://staging.paydirectnow.com/service/interacEmailSimulator.jsp
4. Paste the reference number and click Search to automatically populate the transaction details.
5. Click Send Email.

Paramount Interac® sends a notification to PIQ transaction notification URL to complete the transaction.

### PayOut Testing steps

To initiate a Paramount Interac® Payout test transaction, you need to enter the amount, select a security question and enter a security answer from the cahier.

You will need also to use a real email in the request, where you will be receiving an email from Paydirect billing Demo.

From that email, please go to the email headers and extract the value of the parameter `<X-PaymentKey>`
Then please send to Paramount the value of `<X-PaymentKey>` so that they can simulate the payout processing on their side, which will trigger the event notification being sent to PIQ.
