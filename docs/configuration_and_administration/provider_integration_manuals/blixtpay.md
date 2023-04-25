--- 
id: "blixtpay"
title: "BlixtPay"
hide_title: "true"
---

![](/img/providers/logos/blixtpay.png)

# BlixtPay

## About
BlixtPay is a payment provider offering deposits and withdrawals in EUR currency only.

| Provider Name                | BlixtPay                                           |
|------------------------------|----------------------------------------------------|
| Link                         | N/A                                                |
| Classification               | Banking                                            |
| Currencies                   | `EUR`                                              |
| Methods/PaymentTxTypes       | `BlixtPayBankWithdrawal`<br/> `WebRedirectDeposit` |
| PaymentIQ Configuration File | `BlixtPayConfig`                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.blixtpay.BlixtPayConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <password>{account.password}</password>
                <brandId>{account.brandId}</brandId>
                <merchantId>{account.merchantId}</merchantId>
                <supportedCurrencies>EUR</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.blixtpay.BlixtPayConfig>
```
</details>

| Attribute                | Description                                                                                                                                                                                                                                             |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.password         | Corresponds to the "API key" provided by BlixtPay                                                                                                                                                                                                       |
| account.brandId          | Corresponds to the "Brand" value provided by BlixtPay.                                                                                                                                                                                                  |
| account.merchantId       | Corresponds to "account reference" provided by BlixtPay.                                                                                                                                                                                                |
| statusPollAttemptsCount  | Sometimes it takes some time to received a final tx status from the provider and in order to wait on that final status you can configure `statusPollAttemptsCount` to perform several status check attempts (3 times by default).                       |
| statusPollIntervalInSec  | It is used to specify a timeout between status check attempts (2 sec. by default).                                                                                                                                                                      |
| validCallbackIpAddresses | The list of BlixtPay IP addresses from which the callbacks are expected separated by '&#124;' (pipe character) - f.ex. \<validCallbackIpAddresses>127.0.0.1&#124;127.0.0.2\</validCallbackIpAddresses>. The list of IPs should be provided by BlixtPay. |

## Example Routing Rule
![](/img/providers/routing/blixtpay.png)

## User notifications
PIQ Backoffice is receiving all needed information about transaction on StatusCheck, so don't need to configure Webhook for callback.

## Additonal notes
Please make sure to send the "merchantTxId" parameter in the Integration API's authorize response, <br/>
as the "request_id" parameter sent to them is dependent on it: [Integration API - Authorize](/../docs/apis_and_integration/integration_api/authorize#example-response)

## Test Information
For start testing process requires to have all credentials from BlixtPay.
Required credentials:
-API key
-Brand
-account reference
-account_id.

Every customer needs to have BlixtPay account_id (blixtpay_id) and set it to field "userAccountId". Ask BlixtPay to provide instruction how to generate account_id.
For testing Failed transaction use wrong "userAccountId".

## Deposit Testing Flow

For testing Deposit method merchant needs to configure following attribute.

### Attributes

| Attribute | Description                                                        |
|-----------|--------------------------------------------------------------------|
| isMobile  | Device user is using.  <br/> Possible values are `true` or `false` |

BlixtPay provides two different ways for deposits. Merchant need to ask BlixtPay to provide test application for the mobile phone with active account credentials.

Flow 1: User pays with web browser. After clicking Deposit in the Cashier the user will be redirected to a page with QR code. 
   Scan QR code with application provided by BlixtPay and finish the payment.
   
Flow 2: User pays with the mobile phone. After the user clicks Deposit in Cashier they will be redirected to a page with two buttons "Pay on Site" and "Pay in App". 
   Based on decision user will be redirected to web browser or in BlixtPay application.
