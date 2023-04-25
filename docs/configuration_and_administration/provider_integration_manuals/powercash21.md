--- 
id: "powercash21" 
title: "Powercash21"
hide_title: "true"
---
 
![](/img/providers/logos/powercash21.png)

# Powercash21

## About
Powercash21 is a credit card and APM provider that offers deposit (and recurring), refund (and partial), withdrawal, void, status check.

| Provider Name                | Powercash21                                                                                          |
|------------------------------|------------------------------------------------------------------------------------------------------|
| Product                      | Please contact our technical support team for information.                                           |
| Link                         | [http://powercash21.com/](http://powercash21.com/)                                                   |
| Classification               | Debit/Credit Card Processor / Aggregator                                                             |
| API                          | Please contact our technical support team for information.                                           |
| Regions                      | `International`                                                                                      |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                      |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`, `Void`, `TrustlyDeposit`, `TrustlyWithdrawal` |
| PaymentIQ Configuration File | `Powerpay21Config`                                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.powerpay21.Powerpay21Config>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <!-- <dynamicDescriptor>Bambora/Stockholm</dynamicDescriptor> 'custom2' parameter used for Dynamic Descriptor, only enable once confirmed with Powercash21 -->
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <use3Dsecure>false</use3Dsecure>
         <merchantId>??</merchantId>
         <secretKey>??</secretKey>
      </account>
    </entry>
     <entry>
      <string>3DS</string>
      <account>
        <use3Dsecure>true</use3Dsecure>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <merchantUrl>https://bambora.com</merchantUrl> <!-- 'shop_url' parameter -->
        <redirectUrl>${baseRedirectUrl}/api/powerpay21/deposit/redirect/${ptx.txRefId}</redirectUrl>
      </account>
    </entry>    
  </accounts>
</com.devcode.paymentiq.integration.powerpay21.Powerpay21Config>
```
</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                         |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId        | Is provided by Powercash21 (This is the API username)                                                                                                                                               |
| secret Key        | Secret key that is provided by Powercash21.                                                                                                                                                         |
| use3Dsecure       | If `true`, it will activate the 3DS if the account is supported.                                                                                                                                    |
| useTokenId        | If `true`, it will enable recurring payment. Note - Only to be used with recurring transactions via the Front API. If doing recurring MIT transactions with the Admin API this entry is not needed. |
| dynamicDescriptor | Sends the 'custom2' parameter to Powercash21 which is used for the Dynamic Descriptor. Only enable once confirmed with Powercash21. See more info below.                                            |
| merchantUrl       | Sends the 'shop_url' parameter to Powercash21. Only needed if you use one merchant account for several URLs, in order to handle 3DS correctly.                                                      |
| withdrawalType    | Defaults to `CFT`. Only necessary to be added if you as a merchant wants to change to non-gambling withdrawals, which is done by adding the value `OCT`                                             |

### Dynamic Descriptor
You can use the Dynamic Descriptor if you as a merchant has one Powercash21 MID and different accounts/URLs.

The descriptor should be 38 characters long (if it's shorter, it can be filled by empty spaces). The DBA (doing business as) should contain maximum of 25 characters with only letters and numbers. The city field should contain a maximum of 13 characters.

Example: My Company Name/Phone Number/City.

**Note: Please contact the operations team (operations@powercash.de) to get updates/information on whether you can use the Dynamic Descriptor.**

### Credit Card Withdrawals

Powercash21 supports two different credit card withdrawal flows:
 1. With credit card info (Restricted to non-gambling merchants only).
 2. Extracting credit card info from an existing transaction.

Option 2. is the flow that is enabled by default in PIQ, and this means that a user has to have made a successfully captured deposit transaction before being able to make a withdrawal to the same card.

If PIQ can't find a previous deposit it will decline the transaction with the status `ERR_NO_REFERRAL_TX_FOUND` and info message ***\"Could not find a previous successful Powercash21 deposit transaction between the interval {interval}\"*** - where the {interval} is between the configured amount of days back that PIQ looks in history (default 150 days) and the current date at midnight.

**Note that the reason the interval is up to the current date at midnight because a deposit is captured at Powercash21 over night, meaning if the user's first deposit was made today it won't be possible to use as a reference for a withdrawal until Powercash21 has captured it.**

If you are not a gambling merchant and want to use option 1, the following configuration entry has to be added to the account level in the Powerpay21Config: `<withdrawalType>OCT</withdrawalType>`

### APMs

#### Trustly
To do Trustly payments via Powercash21 you need to use the specific transaction types TrustlyDeposit and TrustlyWithdrawal. More information on the endpoint of these can be found in the front api bank section.

##### Deposits
When initiated, the end user will be redirected to the Trustly page where they choose bank and continues by following the instructions.

##### Withdrawals
In order to do a successful withdrawal, a successful Trustly deposit has to have been done previously. This is so that PIQ can use this transaction as a reference in the request to Powercash21.

Withdrawal transactions can be "reversed", i.e the amount is transferred back to the user's account. This can happen if Powerpay21/Trustly is later on notified that the money transfer failed with the bank. In PIQ, this will create a new transaction of type "Reversal" which has the positive amount of the withdrawal and notifies the merchant with a transfer request.

## Example Routing Rule
![](/img/providers/routing/powerpay21.png)

## Test Information
Additional details can be found [here](https://docs.payabl.com/docs).

### Credit Cards

#### N3DS
| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| MASTERCARD | 5232050000010003 | 003 | Any         |
| VISA       | 4149011500000147 | 147 | Any         |

#### 3DS
| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4242424242424242 | 123 | Any         |

### APMs

#### Trustly
- Amount: 10 EUR
- Bank: Swedbank
- Personal number: 400920-6094
