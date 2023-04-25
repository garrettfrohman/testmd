--- 
id: "neteller" 
title: "Neteller"
hide_title: "true"
---
 
![](/img/providers/logos/neteller.png)

# Neteller

## About
Neteller is a wallet solution offering Deposits and Withdrawals.

| Provider Name                | Neteller                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.neteller.com/en/](https://www.neteller.com/en/)                    |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `NetellerDeposit`<br/> `NetellerWithdrawal`                                     |
| PaymentIQ Configuration File | `NetellerConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example account configuration</summary>
<br/>

If you are not using Customer Verification Tool
```xml
<accounts>
    <entry>
        <string>PaysafeApi</string>
        <account>
            <username>?????</username>
            <password>?????</password>
            <serviceEndpoint>https://api.test.paysafe.com/paymenthub</serviceEndpoint>
            <version>paysafe_rest_api</version>
            <container>window</container>
        </account>
    </entry>
</accounts>
```
If you are using Customer Verification Tool
```xml
<accounts>
    <entry>
        <string>PaysafeApi</string>
        <account>
            <username>?????</username>
            <password>?????</password>
            <serviceEndpoint>https://api.test.paysafe.com/paymenthub</serviceEndpoint>
            <version>paysafe_rest_api</version>
            <container>window</container>
            <customerCheck>true</customerCheck>
            <customerCheckWithdrawal>ture</customerCheckWithdrawal>
            <accountID>?????</accountID>
            <merchantId>?????</merchantId>
            <merchantKeyId>?????</merchantKeyId>
        </account>
    </entry>
</accounts>
```
</details>

### Attributes

| Attribute        | Description                                                                       |
|------------------|-----------------------------------------------------------------------------------|
| username*        | Username - From Paysafe Payments API private Key                                  |
| password*        | Password - From Paysafe Payments API private Key                                  |
| version*         | Set to paysafe_rest_api to use new API                                            |
| serviceEndpoint* | Set to Paysafe Payments API URL to use new API                                    |
|                  |                                                                                   |
| accountID**      | AccountID - Provided by Neteller                                                  |
| merchantId**     | MerchantID - Provided by Neteller                                                 |
| merchantKeyId**  | API Key - Provided by Neteller                                                    |
| externalTestMode | Set to true to be able to test via NETELLER gateway instead of Paysafe simulation |

\* Must be set to use the new Paysafe Payments API (see info below)   
\** After the migration to the new Paysafe Payments API (15 May 2020) these parameter will only be needed if the Customer verification tool is used. 

### Information regarding migration to new API before 15 May 2020
The Deposit and Withdrawal functions via the ***NETELLER REST API will be disabled on 15 May 2020***. In order to continue transaction processing via the NETELLER service, merchants need to use the Paysafe Payments API instead.  
The customer verification service will continue to use the old API after the migration.   
The new API have separate credentials which are available in the same section where the client ID and client secret are.  
***Note that after the migration the account holders 12 digit NETELLER account ID can not be used when processing NETELLER via PIQ, instead only the account holders email address should be used as the parameter 'account'. The parameter 'secureId' is also no longer required***
#### Migration Guide for merchants using NETELLER via PaymentIQ 
1. Contact NETELLER support to configure the callback(webhook) URL to https://api.paymentiq.io/paymentiq/api/neteller/callback (Note, the base URL will be different for non-hosted environment). This has to be done manually by the NETELLER support team.
2. Get the new Paysafe Payments API credentials from NETELLER Merchant Dashboard and add it to a new account entry in NetellerRestConfig in PIQ (see example below).  
**To get your Username/Password, sign in to the NETELLER Merchant Dashboard and click Developer -> Apps. You will find a new section that displays the Paysafe Payments API keys, use the Username/Password for the PRIVATE Key.**  
 ![](/img/providers/neteller01.png)
3. In PIQ NetellerRestConfig, set serviceEndpoint to 'https://api.paysafe.com/paymenthub' in the new account entry (see example below).
4. Also set the version to "paysafe_rest_api" in the same account entry.
5. Change the routing rule to use the new account entry you created in previous steps.

### Note on 2FA

If 2FA is enabled Neteller will ask for the users 2FA code. IF it is not enabled secure ID is required. If a user enters an incorrect 2FA code the transaction log will show this in the response as follows:

```xml
<statusCode>ERR_DECLINED_OTHER_REASON</statusCode>
<pspStatusCode>20008</pspStatusCode>
<pspStatusMsg>"Invalid verification code"</pspStatusMsg>
<pspResponseMsg>{
"error": {
"code": "20008",
"message": "Invalid verification code"
</pspResponseMsg>
```

### Customer Verification Tool
The customer verification service is used to check if one of your customers, identified by the Neteller customerId, is registered with Neteller (i.e. the customer already has an active Neteller Digital Wallet account). You can also verify information that you hold about the customer against Neteller's registration records. This feature needs to be activated for the merchant’s Neteller account, as well as in PaymentIQ.

The information that can be checked is as follows:
- First Name
- Last Name
- Date of Birth
- Country
- Post Code

If the customer has an active Neteller Wallet account, then the verification service returns a MATCH or NO_MATCH response for each parameter provided in the request. Match information is not shown by default for the customerId.

The customer verification service call also returns a verification level for an account which shows:
- Whether the customer has been verified
- Whether the customer has a verified payment instrument e.g. Debit / Credit card or Bank Account registered with their Neteller account.

This code will be shown in the Info column of the transaction view in back office, as well as added to the PSP fraud score column.

#### Enable Neteller Customer Verification in PaymentIQ
Add tag `<customerCheck>true</customerCheck>` to the NetellerConfig to enable it for Neteller deposits. Add `<customerCheckWithdrawal>true</customerCheckWithdrawal>` to enable the check for Neteller withdrawals.

Then to decide which user values that has to match with the user’s Neteller account, add tag customerVerificationMatchingValues with one or several of the following values:
- firstName
- lastName
- dateOfBirth
- country
- postCode

Example where the firstname and lastname of the user has to match with the Neteller account.
```<customerVerificationMatchingValues>firstName|lastName</customerVerificationMatchingValues>```

#### Deciding status code
You can also decide which PaymentIQ specific status code the transaction should end up in in case of a declined transaction due to a mismatch. The default code is ```ERR_DECLINED_FRAUD``` but can be freely chosen with the tag ```pspCodeToStatusCode```
Example of choosing a different status code

```xml
<pspCodeToStatusCode>
  <entry>
    <string>VERIFICATION_MATCHING_FAIL</string>
    <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_OTHER_REASON</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
  </entry>
</pspCodeToStatusCode>
```

## Example Routing Rule
![](/img/providers/routing/neteller.png)
## Test Information

- Please test with either DKK, SEK, GBP, EUR, NOK, CHF, USD, BGN, INR, PLN or CAD. If you want to test with any other currency it needs to be done with currency conversion (using a Forex rule).

| Region | Account                   | Password       |
|--------|---------------------------|----------------|
| EEA    | netellertest1@bambora.com | netellertest1@ |
| ROW    | netellertest2@bambora.com | netellertest2@ |
