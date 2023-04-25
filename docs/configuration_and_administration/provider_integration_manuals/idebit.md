--- 
id: "idebit" 
title: "Idebit"
hide_title: "true"
---
 
![](/img/providers/logos/idebit.png)

# Idebit

## About
Idebit is a bank providers supporting Deposits and Withdrawals.

| Provider Name                | Idebit                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.idebitpayments.com/](https://www.idebitpayments.com/)              |
| Classification               | Online Banking                                                                  |
| Regions                      | `Canada`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `IDebitDeposit` <br/> `IDebitWithdrawal`                                        |
| PaymentIQ Configuration File | `IdebitConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.instadebit.IDebitConfig>
<enabled>true</enabled>
<accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>??</merchantId>
        <memberId>??</memberId>
        <password>??</password>
        <serviceEndpoint>https://www.idebitpayments.com/consumer/merGateway.do</serviceEndpoint>
        <redirectUrl>${baseRedirectUrl}/api/idebit/deposit/redirect?transId=${ptx.txRefId}</redirectUrl>
        <failureUrl>${failureUrl}</failureUrl>
        <successUrl>${successUrl}</successUrl>
     </account>
    </entry>
  </accounts>
  <container>window</container> <!-- redirects to cashier success/failure URLs won't work with iFrame -->
  <notificationVerificationUrl>https://www.idebitpayments.com/service/servlet/ConfirmTrans</notificationVerificationUrl>
  <payoutsUrl>https://www.idebitpayments.com/service/servlet/MerchantPayout</payoutsUrl>
</com.devcode.paymentiq.integration.instadebit.IDebitConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Description                      |
|-------------------------|----------------------------------|
| merchantId              | Merchant ID. Provided by Idebit. |
| memberId                | Member ID. Provided by Idebit.   |
| password                | Password. Provided by Idebit.    |

### Callback URLs:

### Test:
https://test-api.paymentiq.io/paymentiq/api/idebit/deposit/callback

### Prod: 
https://api.paymentiq.io/paymentiq/api/idebit/deposit/callback

:::note
For optimal functionality on mobile browsers we recommend setting `allowMobilePopup=true`. For more information check the [Cashier parameter details](../../apis_and_integration/cashier/cashier_parameter_details#allowmobilepopup).
:::

## Example Routing Rule
![](/img/providers/routing/idebit.png)

## Test Information

### Testing Idebit outside of Canada
If you are located outside of Canada and are accessing the staging environment to test customer transactions, please follow the steps below to configure a proxy server for redirection to the correct environment.

#### Configuring Mozilla Firefox
1. Open Mozilla Firefox
2. For Windows: Select "Options" | For Mac: Under "Firefox", select "Preferences"
3. Scroll down and find ”Networks Settings", click "Settings..."
4. Select "Automatic proxy configuration URL"
5. Enter: http://proxy.idsmanagement.com/proxy.pac

#### Configuring Internet Explorer & Chrome
1. Open Internet Explorer or Chrome
2. Under the “Tools” menu, select “Internet Options”
3. Click “Connections” Tab
4. Select "LAN Settings" box
5. Select “Use Automatic Configuration Script" box
6. Enter: http://proxy.idsmanagement.com/proxy.pac

#### Configuring Safari
1. Open Safari
2. Under the "Safari" tab, select "Preferences"
3. Select "Advanced" category
4. Next to "Proxies:", click "Change Settings" (Opens “System Network Preferences”)
5. Ensure the correct connection method is in the "Show" window (e.g. airport, built-in Ethernet)
6. Select "Web Proxy (HTTP)" box
7. Enter: http://proxy.idsmanagement.com/proxy.pac
8. Repeat for secure web proxy


The test user used need to have the following details. If not the account will be blocked:
- First Name: Demo
- Last Name: Customer

| Currency | Email                      | Password | Bank User ID | Bank Password |
|----------|----------------------------|----------|--------------|---------------|
| USD/CAD  | demo_ca@idebitpayments.com | test4now | 0102030405   | \*\*int\*\*   |

### Testing steps

1. After transaction is initiated with PIQ, authentication is required and a username/password prompt will pop up. Enter `guest` as username and `IntegratingTesting!` as password.
2. In the Log in page enter `demo_ca@idebitpayments.com` as Email Address and `test4now` as Password.
3. Select Test Bank in the select input and continue.
4. Provide `0102030405` as the "Bank User ID" and `**int**` as the "Bank Password".
5. Complete the transaction by selecting account and approving the payment.
