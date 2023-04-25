--- 
id: "payvision" 
title: "Payvision"
hide_title: "true"
---
 
![](/img/providers/logos/payvision.png)

# Payvision

## About
Payvision is a creditcard provider with support for Deposits, Withdrawals, Refunds, Voids and ApplePay.

| Provider Name                | Payvision                                                                                                                 |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.payvision.com/](https://www.payvision.com/)                                                                  |
| Classification               | Debit/Credit Card Processor                                                                                               |
| Regions                      | `International`                                                                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                           |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/>`Void`<br/> `ApplePayDeposit`<br/> `ApplePayWithdrawal` |
| PaymentIQ Configuration File | `PayvisionConfig`                                                                                                         |

## Configuration Information
<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payvision.PayvisionConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <height>600</height>
  <width>1000</width>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <memberId>????</memberId>
        <memberGuid>????</memberGuid>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
    <entry>
      <string>N3DS_AUTH</string>
      <account>
        <authType>FINAL_AUTH</authType>
        <memberId>???</memberId>
        <memberGuid>???</memberGuid>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>  
    <entry>
      <string>3DS</string>
      <account>
        <memberId>???</memberId>
        <memberGuid>???</memberGuid>
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
    <entry>
      <string>3DS_AUTH</string>
      <account>
        <authType>FINAL_AUTH</authType>
        <memberId>???</memberId>
        <memberGuid>???</memberGuid>
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>  
    <entry>
      <string>OCT</string>
      <account>
        <memberId>????</memberId>
        <memberGuid>????</memberGuid>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
    <entry>
      <string>APPLEPAY</string>
      <account>
        <memberId>????</memberId>
        <memberGuid>????</memberGuid>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>       
  </accounts>
  <defaultDescriptor>Company|City</defaultDescriptor> <!-- DBA name and DBA city deparated with a | -->
</com.devcode.paymentiq.integration.payvision.PayvisionConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                                                                                      |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| pspRefId                | Will pick different data for the psp ref id field. if true then TransactionId is used, if false then TransactionGuid is used                     |
| defaultDescriptor       | A description of the merchant. Company and City separated with a \|                                                                              |
| memberId                | Member id provided by Payvision                                                                                                                  |
| memberGuid              | member guid provided by Payvision                                                                                                                |
| authType                | Possible values are FINAL_AUTH or AUTH_CAPTURE. FINAL_AUTH will only do a authorize of the transaction and AUTH_CAPTURE will capture it directly |
| previousDepositRequired | Set to true if withdrawals should not be allowed unless a previous deposit with Payvision has been done with the card                            |

### Condition to check if successful deposit was made
For example if you only want to route withdrawals to Payvision if a previous successful deposit has been made, the condition "User with vault data" should be used with the value `Payvision_Successful_Deposit`. See example:

![](/img/providers/routing/payvision2.png)

## Example Routing Rule
![](/img/providers/routing/payvision.png)

## Test Information

- Currency: EUR (3DS)
- Amount: 12 (3DS)
- To simulate declines, use amounts from 100 through 500.

### 3DS

| Card Brand | Account                         | CVV | Expiry date |
|------------|---------------------------------|-----|-------------|
| VISA       | 4000000000000002 (enrolled)     | Any | Any         |
| VISA       | 4000000000000051 (not enrolled) | Any | Any         |
| VISA       | 4000000000000028 **             | Any | Any         |
| MASTERCARD | 5200000000000106 * (enrolled)   | Any | Any         |
| MASTERCARD | 5200000000000056 (not enrolled) | Any | Any         |
| MASTERCARD | 5200000000000023 **             | Any | Any         |

- \* Choose "Do not activate now"
- ** Expected: Business rule (Error 6000)

### N3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4907639999990022 | Any | Any         |
| VISA       | 4775889400000171 | Any | Any         |
| VISA       | 4917484589897107 | Any | Any         |
| VISA       | 4012000033330026 | Any | Any         |
| MASTERCARD | 5432673003275469 | Any | Any         |
| MASTERCARD | 5546989999990033 | Any | Any         |

### OCT

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4907639999990022 | Any | Any         |
| MASTERCARD | 5546989999990033 | Any | Any         |
