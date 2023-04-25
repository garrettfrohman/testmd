--- 
id: "trustly" 
title: "Trustly"
hide_title: "true"
---
 
![](/img/providers/logos/trustly.png)

# Trustly

## About
Trustly does online banking payments - enabling payments and transfers from consumer bank accounts across Europe. You can accept payments and transfers from bank accounts in 29 European countries and reach more customers at no additional cost.

| Provider Name                | Trustly                                                                                                                                                                                                                                     |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://trustly.com/en/](https://trustly.com/en/)                                                                                                                                                                                          |
| Classification               | Online Banking                                                                                                                                                                                                                              |
| Regions                      | `Austria`, `Germany`, `Belgium`, `Bulgaria`, `Estonia`, `Denmark`, `France`, `Czech Republic`, `Finland`, `Hungary`, `Ireland`, `Italy`, `Latvia`, `Lithuania`, `Slovakia`, `Romania`, `Spain`, `UK`, `Norway`, `Poland`, `Spain`, `Sweden` |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                             |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `BankLocalWithdrawal` <br/> `BankIBANWithdrawal` <br/> `BankIntIBANWithdrawal` <br/> `TrustlyDeposit` <br/> `TrustlyWithdrawal` <br/> `IdealDeposit` <br/> `Refund` <br/> `SignIn` <br/> `Reversal`                     |
| PaymentIQ Configuration File | `TrustlyConfig`                                                                                                                                                                                                                             |

### Additional Links
[Account payout](https://trustly.com/en/developer/api#/accountpayout)

[API](https://trustly.com/en/developer/api)

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.trustly.TrustlyConfig>
  <enabled>true</enabled>
  <notifyParent>false</notifyParent> <!-- Set to true to add the notifyParent parameter in redirect URL -->
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <quickDeposit>false</quickDeposit>
        <username>??</username>
        <password>??</password>
        <version>1.1</version>
        <secretKey>??</secretKey>
        <pspPublicKey>??????</pspPublicKey>
      </account>
    </entry>
    <entry>
      <string>FBB</string> <!-- Account for Finnish Bank Buttons -->
      <account>
        <container>window</container> <!--Finnish banks require window -->
        <quickDeposit>false</quickDeposit>
        <username>??</username>
        <password>??</password>
        <version>1.1</version>
        <secretKey>??</secretKey>
        <pspPublicKey>??????</pspPublicKey>
      </account>
    </entry>
  </accounts>  
  <depositCallbackUrl>${baseCallbackUrl}/api/trustly/callback/deposit</depositCallbackUrl>
  <withdrawalCallbackUrl>${baseCallbackUrl}/api/trustly/callback/withdrawal</withdrawalCallbackUrl>
  <APIVersion>1.1</APIVersion>
  <depositSuccessUrl>${successUrl}</depositSuccessUrl>
  <depositUrlTarget>_self</depositUrlTarget>
  <withdrawalSuccessUrl>${successUrl}</withdrawalSuccessUrl>
  <withdrawalUrlTarget>_self</withdrawalUrlTarget>
  <appendUserCountryForWithdrawal>true</appendUserCountryForWithdrawal>
  <alwaysManualApprove>true</alwaysManualApprove>
  <truncateCallback>false</truncateCallback>
  
  <!-- Enable if no authorize + cancel notification should be sent to merchant
  <skipAuthorizeOnWithdrawalCancel>true</skipAuthorizeOnWithdrawalCancel>-->
  
  <!-- Enable if we should wait for account notification before sending transfer -->
  <accountNotificationWaitTimeSeconds>5</accountNotificationWaitTimeSeconds> 
  
  <!-- Uncomment to disable sending SenderInformation in AccountPayout request
  <sendSenderInformation>false</sendSenderInformation>-->
  
  <!-- Uncomment to remove localisation parameters Locale, Country, and IP from the deposit requests
  <ignoreLocalisation>true</ignoreLocalisation>-->
  
  <bankMappings>
    <bankMapping><countryCode>IRL</countryCode><fromClearingHouse>IRELAND</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>DEU</countryCode><fromClearingHouse>GERMANY</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>FIN</countryCode><fromClearingHouse>FINLAND</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>AUT</countryCode><fromClearingHouse>AUSTRIA</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>SVK</countryCode><fromClearingHouse>SLOVAKIA</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>NOR</countryCode><fromClearingHouse>NORWAY</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>NLD</countryCode><fromClearingHouse>NETHERLANDS</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>SWE</countryCode><fromClearingHouse>SWEDEN</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>CZE</countryCode><fromClearingHouse>CZECH_REPUBLIC</fromClearingHouse></bankMapping>
    <bankMapping><countryCode>GBR</countryCode><fromClearingHouse>UNITED_KINGDOM</fromClearingHouse></bankMapping>
  </bankMappings>
</com.devcode.paymentiq.integration.trustly.TrustlyConfig>
```

</details>

### Credentials
Credentials needed for configuration in PaymentIQ
- API Username
- API Password
- Merchant private key
- Merchant public key

Detailed information on how to generate the merchant private and public key can be found by following this link. In short (xxxxx is the merchant name):

https://trustly.com/en/developer/api#/signature

- Open a terminal window and run following command to generate the merchant private key with openssl genrsa -out xxxxx.pem 2048
- Generate the merchant public key from the merchant private key with openssl rsa -pubout -in xxxxx.pem -out xxxxx_pub.pem -outform PEM
- Insert the private key in the secretkey tag in the TrustlyConfig
- Email the merchant public key ‘xxxxx_pub.pem’  to Trustly.

NOTE: The pspPublicCert should never be touched, since this is Trustly’s public key, which is the same for all merchants.

### Configure Trustly Pay&Play on withdrawal
Trustlys Pay&Play is an api to make deposits and withdrawals faster. On withdrawal they call it account payout.
The special thing with this is that we dont need to send an authorize to Trustly.

To configure this you need to add `<piqVersion>2</piqVersion> ` on the deposit account in `TrustlyConfig`.

This will also handle withdrawals without iframe.

#### Disabling authorize on cancelled withdrawal flow
In case of normal withdrawals with Trustly, a Trustly frame will pop-up for the end-user to complete the flow. The flow can be canceled by the user before finishing, and by default, PIQ will still send an authorize with a succeeding cancel notification to the merchant. To disable that the authorize and cancel occurs, the following TrustlyConfig entry can be added.

`<skipAuthorizeOnWithdrawalCancel>true</skipAuthorizeOnWithdrawalCancel>`

#### Enabling wait time for account notification before transfer
The account notification that Trustly send to PIQ with bank account information can come either before or after the transfer request is sent to the merchant, which means that the account information will not be present if the merchant requires it. To make sure that the account notification always comes before the transfer, one can add the following tag into the TrustlyConfig, with the wanted time in seconds that PIQ should wait:

`<accountNotificationWaitTimeSeconds>5</accountNotificationWaitTimeSeconds>`

#### Disabling 'SenderInformation' for AccountPayouts
SenderInformation is a parameter with end-user specific data such as address and name which is by default sent to Trustly in the AccountPayout request. This parameter is however optional and according to Trustly it should not be sent for gaming payments. To disable this parameter add the following entry into the TrustlyConfig:

`<sendSenderInformation>false</sendSenderInformation>`

### Trustly Express
Trustly Express displays the last-used bank account for returning customers, enabling them to skip steps in the Trustly checkout flow for a quicker, simpler payment experience.
In order to enable Trustly Express, the `accountConfig.expressCheckout` parameter should be set to `true`: `<expressCheckout>true</expressCheckout>`.

### Trustly QuickDeposit and direct debit
QuickDeposit is Trustlys version of Autogiro, Direct debit is used for recurring payments.

To be able to use QuickDeposit and direct debit the merchant needs to have direct debit enabled on their Trustly account. We also need to set `<quickDeposit>true</quickDeposit>` on the deposit accounts in `TrustlyConfig`.

To use recurring payments you need to set `<directDebitMandate>true</directDebitMandate>` in `TrustlyConfig`.

A quick deposit/direct debit works the same way as a normal deposit, with the exception that the end user will also be prompted to sign a direct debit mandate. If the attribute ChargeAccountID have been provided, the end user can be charged without any front end interaction. If the end user is not Swedish, the quick deposit will work just like any other deposit. It is up to the merchant to decide if they are ok with showing the quick deposit for other countries than Sweden, even though it will still be a regular deposit.

You invoke the quick deposit exactly the same way as a regular deposit, except that you also include the attribute QuickDeposit = 1 in the api call (DO NOT send RequestDirectDebitMandate = 1). This is handled by the PaymentIQ code.
You will then get a URL for the iFrame that should be shown to the end user. If the end user haven’t already registered a mandate the end user will be prompted to accept an agreement.
The steps will be the same as a regular deposit, the only difference is the step where the bank account is selected. The register mandate prompt will look like this:

![](/img/providers/trustly01.png)

PaymentIQ will receive an account notification straight away, see
https://trustly.com/en/developer/api#/account
The account notification will contain both the Trustly accountId and directDebitMandate flag. Both these flags are stored on the user psp account in PaymentIQ. The Trustly accountId is stored in the vault data.


If you use 1-click API you need to use the `enduser_id` attribute.
For example:

``
oauth/authorize?identity_provider=trustly&iframe=false&enduser_id=39f0dd7a-8da3-401f-b570-adac046abd8a
``

If you use the front API to enable direct debit mandate you need to send in the userId in the payload. This means that you can only use this for existing users in PaymentIQ, if you want to enable direct debit on non existing users you will need to use 1-click API.
```curl
curl -X POST -H 'Content-Type: application/json' -d '{"sessionId":"{sessionId}","userId":"39f0dd7a-8da3-401f-b570-adac046abd8a","merchantId":"{merchantId}","amount":"100","attributes": {}}' https://test-api.paymentiq.io/paymentiq/api/trustly/deposit/process
```

The value of the flag "directDebitMandate" is shown in the transaction view in Backoffice, check for `trustlyAccountNotification` or `trustlyAccountNotificationV2`.

#### Quick Deposit (when the mandate is in place)
When the the mandate has been successfully registered (usually one bank day later), you will include an AccountID and the attribute DirectDebitMandate = 1

The next time the end-user makes a quick deposit, you should provide both the attributes:
- QuickDeposit: 1
- ChargeAccountID: ```<the AccountID you have received from the account notification>```
(DO NOT send RequestDirectDebitMandate)

If you receive an URL, it should be displayed to the end user. Normally no Trustly iframe will appear, but if for example amount limit is reached the customer will be redirected to a regular Trustly deposit. No checkboxes and no mandates. As always for deposits, a credit notification will be sent when the account should be topped up.
From merchant’s cashier No changes needed from PaymentIQ's end. Trustly will enable the opportunity to register the mandate. The iframe will look like this:
![](/img/providers/trustly02.png)

Here is a link to demo, where you can test the flow for yourself:

http://bit.ly/2bAk4J3

If you use 1-click API you need to use the `enduser_id` attribute as usual.
For example:

``
oauth/authorize?identity_provider=trustly&iframe=false&enduser_id=39f0dd7a-8da3-401f-b570-adac046abd8a
``

If you use the front API to enable direct debit mandate you need to send in the userId  and the payment iq accountId in the payload.

To get the user psp account accountId:
```curl
curl 'https://test-api.paymentiq.io/paymentiq/api/user/transaction/{merchantId}/{userId}?sessionId={sessionId}&type=trustly'
```

Example response:
```json
{
  "merchantId": 1000,
  "userId": "39f0dd7a-8da3-401f-b570-adac046abd8a",
  "success": true,
  "accounts": [
    {
      "type": "trustly",
      "accountId": "b8793be5-31b8-412d-b01b-c965b591",
      "maskedAccount": "**39",
      "lastUsed": "2019-02-26 09:09:46",
      "lastSuccess": "2019-02-26 09:09:46",
      "visible": true,
      "description": null,
      "expired": false,
      "status": "ACTIVE",
      "directDebitMandate": "1"
    }
  ]
}
```

If you see "directDebitMandate" set to "1" then the direct debit is enabled.

Do deposit:

```curl
curl -X POST -H 'Content-Type: application/json' -d '{"sessionId":"{sessionId}","userId":"39f0dd7a-8da3-401f-b570-adac046abd8a","merchantId":"{merchantId}","amount":"1","accountId":"b8793be5-31b8-412d-b01b-c965b591","attributes": {}}' https://test-api.paymentiq.io/paymentiq/api/trustly/deposit/process
```

### Update of direct debit mandate

Trustly can update a users direct debit mandate. This means that even though they send us the users accountId the mandate is not finished. A mandate can also be cancelled.
This is handled by Trustly by sending us a new accountNotification with the attribute directDebitMandate set to "0" (disable) or "1" (enable). To get this to work when the merchant does deposits the merchant needs to send us our accountID from userPspAccount as the parameter "accountId".

Get it like this:
```curl
curl 'https://test-api.paymentiq.io/paymentiq/api/user/transaction/{merchantId}/{userId}?sessionId={sessionId}&type=trustly'
```

### Recurring payments

When setting up recurring payments we will send the flag RequestDirectDebitMandate = 1 to Trustly. Configure this by setting `<directDebitMandate>true</directDebitMandate>` in `TrustlyConfig`.

NOTE! you can't have `quickDeposit` and `directDebitMandate` both to true at the same time.

[More information about direct debit](https://trustly.com/en/developer/api#/directdebit)

---

### Remittance business
Remittance businesses are for merchants whose main business are sending money from person A to person B. Think of it like what Western union does.
To configure this you will need to add the flag `isRemittanceBusiness` in `TrustlyConfig`.

Remittance businesses are required to send details about the recipient with the deposit call to Trustly.
The information needs to be included as attributes in the Merchant API authorize response as in the example below.
```json
{
  "attributes": {
    "recipientInfoPartyType": "PERSON",
    "recipientInfoFirstName": "Satoshi",
    "recipientInfoLastName": "Nakamoto",
    "recipientInfoCountryCode": "SE",
    "recipientInfoCustomerID": "12345",
    "recipientInfoAddress": "Street 1",
    "recipientInfoDateOfBirth": "1990-01-01"
  }
}
```

### Pre-filled and unchangeable national identification number
For SignIn / PnP:
- The UnchangeableNationalIdentificationNumber flag is sent if account config variable `useUnchangeableId` is true.

For regular deposits and redirect withdrawals (not account payouts):
- NationalIdentificationNumber is sent if the account config variable `prepopulateId` is true and attribute "nationalIdentificationNumber" is included in the MerchantVerifyUserRes.
- UnchangeableNationalIdentificationNumber is sent if previous point is true and account config variable `useUnchangeableId` is true.

Example:
```xml
<accounts>
  <entry>
    <string>RegularDeposit</string>
    <account>
      <prepopulateId>true</prepopulateId>
      <useUnchangeableId>true</useUnchangeableId>
    </account>
  </entry>
</accounts>
```

### Send personid and account name on withdrawal authorize
This is a special case where you want to get personid(SSN) and account name from Trustly account notification sent to the integration api `/paymentiq/authorize` when doing withdrawals.

You need to do two configurations:

In `MerchantConfig`, add:
```xml
<entry>
  <string>ssn</string>
  <string>${ptx.latestTxCmdMap.TrustlyAccountNotification.attributes.personid}</string>
</entry>
```

under `<extraAttributes>`.

In `TrustlyConfig`, add:

`<sendAuthorizeAfterAccountNotification>true</sendAuthorizeAfterAccountNotification>`

### Check account number for user on withdrawals
If the country have restrictions that the user account number needs to controlled on withdrawals you can configure this.
This applies to Latvia (for now).

This means that the account number that PaymentIQ gets from Trustly in an AccountNotification will be controlled with the stored account number in PaymentIQ User psp account.

The user psp account is only checked if the user has made a `BankIBANDeposit`, if the user has not done that the withdrawal will fail.

If the account number is not the same the withdrawal will fail.

To configure this you will need to add:
```xml
<checkAccountNumberAgainstUserPspAccount>true</checkAccountNumberAgainstUserPspAccount>
```

### PersonID check for regular deposits
This check is done to verify that the person making the deposit is the same as the stored user psp account. By sending the variable "RequestKYC" to Trustly PIQ will receive a KYC notification right after the user has logged in to the bank and PIQ will be able to decide if the deposit is allowed to continue or not. The merchant must have this feature activated at Trustly for this to work.

The current implementation only checks that the person ID from the KYC notification is the same as the user psp account that is sent with the deposit. So this feature requires that an accountID is included in the /process front-API request. If the person ID doesn't match the deposit is cancelled and the user will not be able to continue in the Trustly iframe.

There are two configurations that should be added to activate this feature:
```xml
<requestKyc>true</requestKyc>
<matchPersonId>true</matchPersonId>
```

### Age verfication - Netherlands
This feature requires a separate processing account on Trustly's side.

In PIQ, all that's needed is to add this to the TrustlyConfig:
```xml
<requestKyc>true</requestKyc>
```

### Ignore Localisation Values
For some markets such as the Netherlands it's not allowed to have NLD pre-selected in the drop-down in the Trustly window. To achieve this it's possible to omit the localisation parameters `Locale`, `Country`, and `IP` from the request. This is enabled by adding the following entry to the provider account config:
```xml
<ignoreLocalisation>true</ignoreLocalisation>
```

### Delocalized checkout (DisableLocalisation)
`forceEnglishLanguage` adds a DisableLocalisation=1 parameter to the url and forces English as a language of the Trustly checkout page.
Should be added on an account level in the TrustlyConfig.
```xml
<forceEnglishLanguage>true</forceEnglishLanguage>
```

### Notify Parent
Requirements for a merchant to allow users to open an external app (e.g. Mobile BankID and
Swish) when the merchant has embedded Trustly’s payment flow within an iframe.

To add the necessary parameter to the redirect URL just add the `notifyParent` paramater on the top level in TrustlyConfig, example:
```xml
<notifyParent>true</notifyParent>
```

If not using PaymentIQ's cashier this has to be implemented in your cashier as well according to the section below.

#### Merchant cashier implementaion
The merchant has to set an event listener for the dispatched message from the embedded
iframe. See MDN documentation for window.postMessage for more information. Example in
javascript below:

```javascript
window.addEventListener(“message”, function (event) {
  if (event.origin !== “https://trustly.com”) { // Ensure that the origin of the message is Trustly
    return;
  }
  var data = JSON.parse(event.data);
  if (data.method === “OPEN_APP”) {
    location.assign(data.appURL); // Opens the app by assigning the URL
  }
}, false);
```

### Decline deposit if the account holder name doesn't match
PaymentIQ can decline the deposit before it is processed if the name returned from the provider doesn't match with the name PaymentIQ receives from the verifyUser response. The matching algorithm used is "Levenshtein Distance" and the similarity between the strings must be at least 90% by default. This value can be configured with setting nameMatchPercentageThreshold.

By default the matching will be case sensitive and all middle names will be considered. This can be configured with the settings nameMatchIgnoreMiddleNames and nameMatchIgnoreCase. For example, to ignore all middle names add the following configuration entry:

`<nameMatchIgnoreMiddleNames>true</nameMatchIgnoreMiddleNames>`

The name matching feature is activated by adding the following configuration entry:

`<matchAccountHolderName>true</matchAccountHolderName>`

In order for PIQ to receive the KYC notification from Trustly with the name, the merchant must have either **NameVerify** or **PnP(AgeVerify)** enabled on their Trustly account.

**NameVerify** - This option is recommended to use if the only intent is to verify the names, specifically meant for the German market (for the time being). Enabled in PIQ by adding `<nameVerify>true</nameVerify>` on the specific account in the TrustlyConfig.

**PnP(AgeVerify)** - It is also possible to use the name matching feature with a PnP (or AgeVerify) enabled account. The main focus with this enabled is to receive all KYC parameters, not just the names, but in most cases the names will be included and PIQ will be able to do the matching. Enabled in PIQ by adding `<requestKyc>true</requestKyc>` on the specific account in the TrustlyConfig.

### Deposit name matching using account notification
Name matching can also be done using Trustly's account notification instead of KYC notification (see section above). The transaction will be set to status code ERR_NAME_MISMATCH and state INCONSISTENT if the names don't match. The feature is activated by adding the following in TrustlyConfig, either on top or account level:

`<matchAccountHolderNameFromAccountNotification>true</matchAccountHolderNameFromAccountNotification>`

Also remember that PaymentIQ must have received the account notification for the verification to be possible, so it will be useful to use this feature together with `<accountNotificationWaitTimeSeconds>`, which sets how long PaymentIQ will wait for the account notification. If no account notification was received within that time the transaction will be put to state INCONSISTENT.

### Ignore pending notifications
For merchants that are experiencing issues with transactions that doesn't get successful in PaymentIQ but are success at Trustly it can be because the pending notifications is sent at the same time as other notifications. The pending notifications doesn't add any functionality to the transaction and can be ignored by adding one of the following examples in TrustlyConfig on root level:

```xml
<ignorePendingNotification>true</ignorePendingNotification>
<ignorePendingNotificationForDeposits>true</ignorePendingNotificationForDeposits>
<ignorePendingNotificationForWithdrawals>true</ignorePendingNotificationForWithdrawals>
```

This will ignore pending notifications either for all transactions, only deposits or only withdrawals.

## Example Routing Rule
![](/img/providers/routing/trustly.png)

## Test Information

Please check directly with the provider.