--- 
id: "upaycard" 
title: "UPayCard"
hide_title: "true"
---
 
![](/img/providers/logos/upaycard.png)

# UPayCard

## About
UPayCard is E-Wallet provider that offers deposit (transfer from any user on UPayCard), withdrawal (from merchant account to user UPayCard account), refund and status check. It also offers Bank deposit (receive money from customer to merchant’s account) and withdrawal (send money from merchant’s account to a customer) operations.

| Provider Name                | UPayCard                                                                                                                            |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://upaycard.com/](https://upaycard.com/)                                                                                      |
| Classification               | Wallet                                                                                                                              |
| Regions                      | `International`                                                                                                                     |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                     |
| Methods/PaymentTxTypes       | `UPayCardDeposit`<br/> `Refund`<br/> `UPayCardWithdrawal`<br/> `BankDeposit`<br/> `BankIBANWithdrawal`<br/> `BankIntIBANWithdrawal` |
| PaymentIQ Configuration File | `UPayCardConfig`                                                                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.upaycard.UPayCardConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>UPC_USD</string>
      <account>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey><!--SECRET-->
        <service>1</service>
        <pendingUrl>??</pendingUrl><!--backToMerchantUrl-->
        <apiKey>???</apiKey><!--KEY-->
        <sourceAccount>???</sourceAccount>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <container>iframe</container>
  <width>1000</width>
  <height>700</height>
  <liveServiceEndPoint>https://api.upaycard.com/api/merchant</liveServiceEndPoint>
  <redirectUrl>${baseRedirectUrl}/api/upaycard/deposit/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseCallbackUrl}/api/callback/upaycard/${ptx.txRefId}</callbackUrl>
  <bankMappings>
    <bankMapping>
      <!--TODO: use correct bank mapping here-->
      <countryCode>MLT</countryCode>
      <bankName>National Bank</bankName>
      <bankAddress>USA</bankAddress>
      <branchCity>Chicago</branchCity>
    </bankMapping>
  </bankMappings>
  <ewalletDepositConfirmationHtmlTemplateName>upaycard-confirm-ewallet-deposit-template</ewalletDepositConfirmationHtmlTemplateName>
  <bankDepositConfirmationHtmlTemplateName>upaycard-confirm-bank-deposit-template</bankDepositConfirmationHtmlTemplateName>
  <version>1.0</version>
</com.devcode.paymentiq.integration.upaycard.UPayCardConfig>

```
</details>

### Attributes

| Attribute     | Description          |
|---------------|----------------------|
| secretKey     | Provided by UPayCard |
| apiKey        | Provided by UPayCard |
| sourceAccount | Provided by UPayCard |

### UPayCard Confirm Payment HTML template

```html
<html>
   <head>
       <title>Confirm Payment</title>
       <script src="https://code.jquery.com/jquery-3.1.0.min.js"></script>
       <script type="text/javascript">
           $(document).ready(function () {
           $("#confirmation-form").submit(function (event) {
           //stop submit the form, we will post it manually.
           event.preventDefault();

           var redirectUrl = '${baseRedirectUrl}?keyCode=' + $('#keyCode').val();
           window.location = redirectUrl;
           });
           });
       </script>
   </head>
   <body>
       <form id="confirmation-form">
           <div>Enter Key Code for Token: ${tokenNumber}</div>
           <input type="text" id="keyCode" name="keyCode" value="" placeholder="Key Code">
           <input type="submit" id="bth_confirm" name="confirm" value="Confirm">
       </form>
   </body>
</html>
```


## Example Routing Rule
![](/img/providers/routing/upaycard.png)

## Test Information

### Test API Credentials
KEY	b53d6ae6e987d049
Secret	8f817edf7005d0f7

### Test URLs

| https://sandboxauser.upaycard.com | User front end         |
|-----------------------------------|------------------------|
| https://sandboxapi.upaycard.com   | Integration API (TEST) |
| https://api.upaycard.com          | Integration API (LIVE) |

### Test Users
One business user who would be you and 3 personal as your sponsored users and one additional BTC user for Bitcoin testing.

#### Business User: BusinessTest65686

Password: 4632342

Account USD: 1786046

Account BTC: 1786047


#### Sponsored User1: spTest656861

Password: 3764233

Account USD: 1786050

Account BTC: 1786051

#### Sponsored User2: spTest656862

Password: 8537439

Account USD: 1786052

Account BTC: 1786053

#### Sponsored User3: spTest656863

Password: 4637645

Account USD: 1786054

Account BTC: 1786055

#### PersonalUser: simpleTest65686

Password: 7234767

Account BTC: 1786056
