--- 
id: "acapture" 
title: "Acapture (via Payon)"
hide_title: "true"
---

![](/img/providers/logos/acapture.png)

# Acapture (via Payon)

## About

Acapture is a credit card provider that offers deposits with 3D secure, refunds (full and partial), recurring, withdrawal. 

| Provider Name                | Acapture (via Payon)                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.acapture.com/](https://www.acapture.com/)                          |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`                           |
| PaymentIQ Configuration File | `PayonConfig`                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payon.PayonConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>ACAPTURE_N3DS</string>
      <account>
        <username>???</username>
        <password>???</password>
        <serviceEndpoint>https://test.oppwa.com/v1</serviceEndpoint>
        <merchantId>???</merchantId>
        <redirectUrl>${baseRedirectUrl}/api/payon/deposit/redirect/form/${ptx.txRefId}</redirectUrl>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
        <version>form</version>
        <accessToken>???</accessToken>
      </account>
    </entry>
    <entry>
      <string>ACAPTURE_3DS</string>
      <account>
        <username>???</username>
        <password>???</password>
        <serviceEndpoint>https://test.oppwa.com/v1</serviceEndpoint>
        <merchantId>???</merchantId>
        <redirectUrl>${baseRedirectUrl}/api/payon/deposit/redirect/form/${ptx.txRefId}</redirectUrl>
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId>
        <version>form</version>
        <accessToken>???</accessToken>
      </account>
    </entry>
  </accounts>
  
  <userPWD>???</userPWD>
  <userID>???</userID>
  <securitySender>???</securitySender>
  <transactionChannel>???</transactionChannel>
  <transactionMode>CONNECTOR_TEST</transactionMode>
  <paymentCode>CC.DB</paymentCode>
  <paymentUsageAttributeKey>brand</paymentUsageAttributeKey>
  
</com.devcode.paymentiq.integration.payon.PayonConfig>
```
</details>

### Attributes

| Attribute   | Description                                                                        |
|-------------|------------------------------------------------------------------------------------|
| username    | Username provided by Acapture                                                      |
| password    | Password provided by Acapture                                                      |
| merchantId  | Merchant id provided by Acapture                                                   |
| accessToken | Access token generated from Acapture BO or requests from Acapture customer support |

#### Authentication
All customers are required to upgrade prior to March 31, 2020 to use the acccessToken as the authentication mechanism.
This can be generated from Acapture Backoffice (BIP) or send a email to technicalsupport@acapture.com

### 3D secure deposit
Acapture doesn't offer API to check if card is enrolled or not.
When you make the /payment, if the card is not enrolled for 3DS, Acapture just does an authorization and you will get the response synchronously. Else you will get the redirection details with enrollment result to /payment call. 

#### 3D secure flow
1. Payment request using card “4711100000000000”. There are few more 3D test cards listed below.
2. Redirect the user using the response parameters and the HTTP method returned in the response
3. After user finishes the authentication, we will redirect him back to the shopperResultUrl
4. Get Payment Status using the payment id to render the status of final payment

### Result Codes
A result code has the format ddd.ddd.ddd, i.e. 3 groups of 3-digit numbers.

Example: 800.100.153 means: 
800 -> Bank declined, 
100 -> it declined the authorization, 
153 -> it declined authorization because the CVV is wrong

#### Result codes for successfully processed transactions
![](/img/providers/acapture01.png)

#### Result codes for pending transactions
![](/img/providers/acapture02.png)

## Example Routing Rule
![](/img/providers/routing/acapture.png)
## Test Information

- Mock user: PAYON

| Card Brand | Account          | CVV | Expiry date | Result/Info     |
|------------|------------------|-----|-------------|-----------------|
| VISA       | 4200000000000000 | Any | Any         | not enrolled    |
| VISA       | 4711100000000000 | Any | Any         | 3DS enrolled ci |
| MASTER     | 5454545454545454 | Any | Any         | not enrolled    |
| MASTER     | 5212345678901234 | Any | Any         | 3DS enrolled ci |
| AMEX       | 377777777777770  | Any | Any         | not enrolled    |
| AMEX       | 375987000000005  | Any | Any         | 3DS enrolled ci |