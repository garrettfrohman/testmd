--- 
id: "ecopayz" 
title: "EcoPayz"
hide_title: "true"
---
 
![](/img/providers/logos/ecopayz.png)

# EcoPayz

## About
The ecoPayz Merchant Account gives you access to a globally renowned payment option, the ecoAccount, whilst at the time offering you an instant and cost effective means of taking payments from customers worldwide - even in countries that can be difficult to reach. ecoPayz is a e-wallet where your customers can both do a deposit and withdrawal.

| Provider Name                | EcoPayz                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.ecopayz.com/en/](https://www.ecopayz.com/en/)                      |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `EcoPayzDeposit`<br/> `EcoPayzWithdrawal`                                       |
| PaymentIQ Configuration File | `EcoPayzConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.ecopayz.EcoPayzConfig>
  <enabled>true</enabled>
 <accounts>
    <entry>
      <string>EUR</string>
      <account>
      <merchantId>??</merchantId>
        <accountID>??</accountID>
        <password>??</password>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
    <entry>
      <string>CAD</string>
      <account>
      <merchantId>??</merchantId>
        <accountID>??</accountID>
        <password>??</password>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
    <entry>
      <string>SEK</string>
      <account>
      <merchantId>??</merchantId>
        <accountID>??</accountID>
        <password>??</password>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
  </accounts> 
  <payoutUrl>https://secure.ecopayz.com/services/MerchantAPI/MerchantAPIService.asmx</payoutUrl>
  <liveServiceEndPoint>https://secure.ecopayz.com/PrivateArea/WithdrawOnlineTransfer.aspx?</liveServiceEndPoint>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.ecopayz.EcoPayzConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential |
|-------------------------|---------------------|
| merchantId              | Id                  |
| accountID               | Account Id          |
| password                | Merchant password   |


### Callback URLs

**For TEST**

URL success:

`https://test-api.paymentiq.io/paymentiq/api/ecopayz/deposit/redirect/success?TxID={CustomerOriginatedTxID}`

URL failure:

`https://test-api.paymentiq.io/paymentiq/api/ecopayz/deposit/redirect/failure?TxID={CustomerOriginatedTxID}`

Transfer and callback URL:

`https://test-api.paymentiq.io/paymentiq/api/ecopayz/deposit/callback`

**For PRODUCTION**

URL success:

`https://api.paymentiq.io/paymentiq/api/ecopayz/deposit/redirect/success?TxID={CustomerOriginatedTxID}`

URL failure:

`https://api.paymentiq.io/paymentiq/api/ecopayz/deposit/redirect/failure?TxID={CustomerOriginatedTxID}`

Transfer and callback URL:

`https://api.paymentiq.io/paymentiq/api/ecopayz/deposit/callback`

### Logo in ecoPayz payment window

You can send your logo to ecoPayz and they will uploaded it in the payment window. It will shown  when the player is going to do a deposit or a withdrawal.

![](/img/providers/ecopayz01.png)

### EcoVoucher
To use ecoVoucher, include a `service` parameter in the process request with value `VOUCHER`.

## Example Routing Rule
![](/img/providers/routing/ecopayz.png)

## Test Information
### Wallet accounts

| Currency | Username          | Password    |
|----------|-------------------|-------------|
| EUR      | devcode_user1     | October2022 |
| EUR      | devcode_user2     | October2022 |
| EUR      | devcode_user_test | October2022 |

### Vouchers

| Amount | Currency | Voucher            |
|--------|----------|--------------------|
| 10.00  | GBP      | 116639598104742383 |
| 10.00  | GBP      | 162454826489025290 |
| 10.00  | GBP      | 180588030537233279 |
| 10.00  | GBP      | 176073488995417681 |
| 10.00  | GBP      | 145638469636981324 |
| 10.00  | EUR      | 177160763095357050 |
| 10.00  | EUR      | 182251245258968844 |
| 10.00  | EUR      | 176491878733505789 |
| 10.00  | EUR      | 141054832141315399 |
| 10.00  | EUR      | 132065237031719451 |
| 10.00  | CAD      | 180437779884523505 |
| 10.00  | CAD      | 183766859288045891 |
| 10.00  | CAD      | 163581201798152266 |
| 10.00  | CAD      | 162605864135335782 |
| 10.00  | CAD      | 177223292575925905 |
| 10.00  | USD      | 147315926197801770 |
| 10.00  | USD      | 165747351829277577 |
| 10.00  | USD      | 173853593231594424 |
| 10.00  | USD      | 113792733151505337 |
| 10.00  | USD      | 113764495315313386 |
