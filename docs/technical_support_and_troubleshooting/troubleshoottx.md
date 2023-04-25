---
id: "troubleshoottx"
---

# Investigate Failed Transactions

## Problem Description

A transaction has ended up in state `FAILED` in PaymentIQ and you want to find out why and if there is a risk of this happening to future transactions.

![](/img/troubleshooting/failedtx.png)

## Troubleshooting Steps

### Is there any information in the Info column?

In PaymentIQs Transaction View there is a column called Info. This is usually the best starting point get information about why a transaction failed.

You will not usually get information specifically about where the transaction failed, but often you can figure it out from the information and your experience.

In the example from this image you can probably figure out that the customer used a currency which was not supported by the provider. 

![](/img/troubleshooting/infotx.png)

And from this you can consider f.ex either
- Contacting the provider about the currencies supported
- Updating your routing rules or payment method rules to make sure the users with this currency gets other options.

### Are the routing and credentials added correctly?

A common issue with failed transactions is that there is some type of configuration issue with the transaction routing. To make sure that the routing is correct please follow these steps:

#### 1 - Did the transaction match a rule?

Check the transaction id in the Tx-id colum in the Transaction View in PaymentIQ

![](/img/troubleshooting/txid.png)

Go to Rules > Routing > Routing to view the Routing rules. Click the small cogwheel and choose "Match transaction against rules, type in your Tx-id and press "Match"

![](/img/troubleshooting/match.png)

This will locate the routing rule used for that transaction. If no rule can be found, that will be why the transaction failed or tried to route with a fallback rule. This means you will need to check why the transaction did not meet the conditions of the rules available, or create a new routing rule with conditions that works for the transaction.

#### 2 - Are the PSP account and PSP set in the rule?

If the "Match" search did find a rule was used, please scroll and locate it. Make note of the "PSP account" and "PSP" set as action in the rule. If if either of them are not set or are blank, this will be the cause of the failed transaction.

![](/img/troubleshooting/routingtx.png)

#### 3 - Does the routing rule match the account name in the provider config?

With the note of "PSP account" and PSP available, go to Admin > Configuration in PaymentIQ (this will only be available as an option for Admin users). Click on the PSP Config that was used in the rule and make sure the "PSP Account" in the rule is listed under accounts. There needs to be an account matching the rule or the transaction will fail.

![](/img/troubleshooting/payontxexample.png)

In this example you can see that the routing is correct. (Please note that "default" in the routing will match anyway of there is only one account listed in the config).

#### 4 - Are there credentials added in the provider config?

The final step to check is to make sure the credentials for the provider are added in the provider config file under the account. Continuing on the example above it could for example look like this:

```xml
<account>
   <username>123456</username>
   <password>djkglsdkghlbhslgsdgisofids</password>
   <serviceEndpoint>https://test.oppwa.com/v1</serviceEndpoint>
   <merchantId>jkjfdjfdkjfdkjfk34343435</merchantId>
   <redirectUrl>${baseRedirectUrl}/api/payon/deposit/redirect/form/${ptx.txRefId}</redirectUrl>
   <use3Dsecure>false</use3Dsecure>
   <useTokenId>false</useTokenId>
   <version>form</version>
</account>
```

Here you can see the username and password is set and so the provider will know which merchant is doing the transaction. If the provider config had looked for example like this:

```xml
<account>
   <username>??</username>
   <password>??</password>
   <serviceEndpoint>https://test.oppwa.com/v1</serviceEndpoint>
   <merchantId>??</merchantId>
   <redirectUrl>${baseRedirectUrl}/api/payon/deposit/redirect/form/${ptx.txRefId}</redirectUrl>
   <use3Dsecure>false</use3Dsecure>
   <useTokenId>false</useTokenId>
   <version>form</version>
</account>
```

It would mean the credentials has not been added and so the transaction will fail. Please note that provider configs will look a bit different, but the general principle is that there needs to be credentials for the provider. 

### Can the issue be located in the transaction log?

If there is not enough information in the Info field and the routing seems to be correct advanced users can proceed with additional troubleshooting. 

A transaction can fail in a lot of different ways and so trying to methodically pin down the issue will usually be the quickest way to resolve it. The best starting point for this is to use the transaction log in PaymentIQ.

Locate the transaction in the Transaction View then right click on it to get the context menu and choose "View Transaction". 

![](/img/troubleshooting/viewtx.png)

You will then get a new tab in PaymentIQ containing our XML log of the events for the transaction.

![](/img/troubleshooting/logtx.png)

The log is not complete but will contain most of the relevant information to find and resolve an issue.

Important to understand is that since the log lists the events of the transaction in order, it will correspond to the general flow for transactions shown [here](/docs/apis_and_integration/integration_overview/communication_flow)

There are typically four event types that are good to check in the log and which will most often be of help.

#### 1 - Is the Cashier/Front end input data and method correct?

The first log entry shows input and client information. For example it could look like this:

```xml
<com.devcode.paymentiq.integration.cryptocurrency.CryptoCurrencyDepositInput>
    <created>2020-08-18 06:48:38.259 UTC</created>
    <merchantId>1979</merchantId>
    <userId>test</userId>
    <sessionId>123</sessionId>
    <amount>1</amount>
    <attributes class="linked-hash-map">
        <entry>
            <string>initiatingClient</string>
            <string>piq-standardized-cashier-1.1.8</string>
        </entry>
        <entry>
            <string>channelId</string>
            <string>Windows</string>
        </entry>
        <entry>
            <string>channelDetails</string>
            <string>Windows | 10 | Chrome | 84.0.4147.125 | isMobile: false | 1280 x 720</string>
        </entry>
    </attributes>
    <storeAccount>true</storeAccount>
    <ipAddr></ipAddr>
    <acceptHeader>*/*</acceptHeader>
    <userAgentHeader>Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.125 Safari/537.36</userAgentHeader>
    <acceptLanguageHeader>en-US,en;q=0.9,sv;q=0.8</acceptLanguageHeader>
    <refererHeader>https://pay.paymentiq.io/cashier/develop/?environment=test&amp;merchantId=1979&amp;userId=test</refererHeader>
    <apiSource>FRONT_API</apiSource>
</com.devcode.paymentiq.integration.cryptocurrency.CryptoCurrencyDepositInput>
```

You should check the method used for the transaction here. So CryptoCurrencyDeposit in this case. Sometimes a merchant will be using the wrong method for the provider (all methods available for a provider are listed in the respective provider integration manual) and this may cause a transaction to fail.

Some providers will require additional parameters from the input and they will also be shown here. You can find the full list of additional parameters required [here](/docs/apis_and_integration/front_api/front_api_introduction) in the provider specific parameters section.

#### 2 - Is the verify user data correct?

After PaymentIQ receives the input it will do a verify user check (remember the transaction flow linked earlier). The response will be listed in the log and will look something like this:

```xml
<com.devcode.paymentiq.integration.merchant.MerchantVerifyUserRes>
    <created>2020-08-18 06:48:38.273 UTC</created>
    <userId>test</userId>
    <success>true</success>
    <attributes>
        <entry>
            <string>channelId</string>
            <string>I</string>
        </entry>
    </attributes>
    <updateState>true</updateState>
    <userCat>VIP</userCat>
    <firstName>Kalle</firstName>
    <lastName>Andersson</lastName>
    <street>Storgatan 1</street>
    <city>Storby</city>
    <zip>12345</zip>
    <country>SWE</country>
    <email>test@example.com</email>
    <dob>1981-01-01</dob>
    <mobile>+46-733805161</mobile>
    <balance>91.00</balance>
    <balanceCy>EUR</balanceCy>
    <locale>en</locale>
    <kycStatus>Accept</kycStatus>
    <sex>MALE</sex>
</com.devcode.paymentiq.integration.merchant.MerchantVerifyUserRes>
```

For a transaction to be successful it is important that the verify user response is correct and contains the parameters listed in the Integration API documentation. For example if `<sex>MALE</sex>` is submitted as `   <sex>Male</sex>` or if `<dob>1981-01-01</dob>` is submitted as `<dob>1981/01/01</dob>` or if the phone number is submitted without the `+`the transaction may fail. Also omitting parameters such as zip or email will often cause providers to decline the transaction. 

The MerchantVerifyUserRes log will show you what is listed but usually the result of not responding properly to the verify user request will cause issues at the provider end, which is the next log section we will check.

#### 3 - Is the Merchant Response successful?

Next thing to check in the transaction log is the Authorize response from the merchant platform. At this stage the transaction has been received by PaymentIQ and the merchant has verified the user and now what is needed is a successful authorization from the merchant platform.

A successful response will look something like this:

```xml
<com.devcode.paymentiq.integration.merchant.MerchantAuthorizeTxRes>
    <created>2019-05-08 08:13:15.955 UTC</created>
    <statusCode>SUCCESS</statusCode>
    <userId>test</userId>
    <success>true</success>
    <attributes>
        <entry>
            <string>channelId</string>
            <string>I</string>
        </entry>
    </attributes>
    <updateState>true</updateState>
    <authCode>ea3cfd74-eb77-424f-895d-f5779b4d6d1e</authCode>
    <merchantTxId>1116834</merchantTxId>
</com.devcode.paymentiq.integration.merchant.MerchantAuthorizeTxRes>
```

And an unsuccessful response, causing a failed transaction will look like this:
```xml
<com.devcode.paymentiq.integration.merchant.MerchantAuthorizeTxRes>
    <created>2019-02-28 11:55:09.548 UTC</created>
    <statusCode>ERR_MERCHANT_RESPONSE_CODE_UNKNOWN</statusCode>
    <userId>test</userId>
    <success>false</success>
    <errCode>100</errCode>
    <errMsg>Internal Error</errMsg>
    <attributes>
        <entry>
            <string>channelId</string>
            <string>I</string>
        </entry>
    </attributes>
    <updateState>true</updateState>
</com.devcode.paymentiq.integration.merchant.MerchantAuthorizeTxRes>
```

The error `ERR_MERCHANT_RESPONSE_CODE_UNKNOWN` can also be seen in the Transaction View in the "Status Description" column. This provides a quick way to notice these types of error.

As this type of error happens at the merchant operator end PaymentIQ does not have any further information about what has gone wrong with the transaction. The issue will need to be escalated to your IT-team.

#### 4 - Did the provider respond successfully or with an error?

The most common issue causing failed transactions if PaymentIQ is configured correctly will be some problem or decline from the provider end. The responses from the provider are listed in the log and will look different depending on the provider.

In the example below we can see a response from IKajo regarding a creditcard deposit which was declined. The `pspStatusMsg` will usually contain the most information for figuring out the issue. Here it simply says "Account error" which does not give much more information other than that it likely is a merchant account setting or configuration issue on the provider side. 

```xml
 <com.devcode.paymentiq.integration.creditcard.deposit.CreditcardDepositTxRes>
        <created>2020-11-11 17:41:44.159 UTC</created>
        <provider>IKajo</provider>
        <statusCode>ERR_DECLINED_OTHER_REASON</statusCode>
        <responseCode>200</responseCode>
        <pspStatusCode>ERROR</pspStatusCode>
        <pspStatusMsg>Account error</pspStatusMsg>
        <pspResponseMsg>{&quot;result&quot;:&quot;ERROR&quot;,&quot;error_message&quot;:&quot;Account error&quot;}</pspResponseMsg>
</com.devcode.paymentiq.integration.creditcard.deposit.CreditcardDepositTxRes>
```

Transactions can fail in a lot of different ways on the provider end but if you familiarize yourself with the errors usually it will help making quick progress on resolving transaction issues. For example if you see something about "Invalid Credentials" in `pspStatusMsg` the issue will often be in the credentials added for the account in the provider config. Or for example if you see an error referring to some error code 05 for a credit card transaction it will likely be a decline on the issuer end with "Do Not Honour" and so on.

### Contacting PaymentIQ Technical Support or Onboarding Support

If you have checked as many of the above listed points you are comfortable with and have access to, but still can not find out why the transaction failed or need more information, please reach out to the Onboarding Team if you are currently Onboarding or the Technical Support Team if you are live.

It is helpful for us when troubleshooting to know the MID and transaction ID of the transaction you are having issues with and any other related information you have found in your troubleshooting.