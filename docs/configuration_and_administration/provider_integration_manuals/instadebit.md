--- 
id: "instadebit" 
title: "Instadebit"
hide_title: "true"
---
 
![](/img/providers/logos/instadebit.png)

# Instadebit

## About
Instadebit is a banking provider offering deposits and withdrawals.

| Provider Name                | Instadebit                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.instadebit.com/](https://www.instadebit.com/)                      |
| Classification               | Online Banking                                                                  |
| Regions                      | `Canada`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `InstadebitDeposit`<br/> `InstadebitWithdrawal`<br/> `Reversal`                 |
| PaymentIQ Configuration File | `InstadebitConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.instadebit.InstadebitConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <memberId>??</memberId>
        <password>??</password>
        <redirectUrl>${baseRedirectUrl}/api/instadebit/deposit/redirect?transId=${ptx.txRefId}</redirectUrl>
      </account>
    </entry>
  </accounts>
  <container>window</container> <!-- redirects to cashier success/failure URLs won't work with iFrame -->
  <notificationVerificationUrl>https://www.instadebit.com/service/servlet/ConfirmTrans</notificationVerificationUrl>
  <payoutsUrl>https://www.instadebit.com/service/servlet/MerchantPayout</payoutsUrl>
</com.devcode.paymentiq.integration.instadebit.InstadebitConfig>
```

</details>

### Attributes
| Attribute  | Description                            |
|------------|----------------------------------------|
| merchantId | Merchant ID provided by Instadebit     |
| memberId   | Merchant Sub ID provided by Instadebit |
| password   | Password provided by Instadebit        |



### Callback URLs:

#### TEST
https://test-api.paymentiq.io/paymentiq/api/instadebit/deposit/callback

#### PRODUCTION 
https://api.paymentiq.io/paymentiq/api/instadebit/deposit/callback

:::note
For optimal functionality on mobile browsers we recommend setting `allowMobilePopup=true`. For more information check the [Cashier parameter details](../../apis_and_integration/cashier/cashier_parameter_details#allowmobilepopup).
:::

## Example Routing Rule
![](/img/providers/routing/instadebit.png)

## Test Information

### Testing Instadebit outside of Canada
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

| Currency | Email                  | Password | Last 3 digits of SIN |
|----------|------------------------|----------|----------------------|
| USD/CAD  | demo_ca@instadebit.com | test4now | 333                  |

### Testing steps
1. After transaction is initiated with PIQ, authentication is required and a username/password prompt will pop up. Enter `guest` as username and `IntegratingTesting!` as password.
2. In the Log in page enter `demo_ca@instadebit.com` as Email Address and `test4now` as Password.
3. When asked for "last 3 digits of SIN", provide `333` and complete the transaction.