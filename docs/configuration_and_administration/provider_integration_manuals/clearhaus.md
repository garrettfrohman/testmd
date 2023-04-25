--- 
id: "clearhaus" 
title: "Clearhaus"
hide_title: "true"
---
 
![](/img/providers/logos/clearhaus.png)

# Clearhaus

## About
Clearhaus is a credit card provider that offers deposits, refunds, voids, withdrawal.

| Provider Name                | Clearhaus                                                                                                    |
|------------------------------|--------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.clearhaus.com/](https://www.clearhaus.com/)                                                     |
| Classification               | Debit/Credit Card Processor                                                                                  |
| Regions                      | `International`                                                                                              |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `MobilePayDeposit`<br/> `ApplePayDeposit` |
| PaymentIQ Configuration File | `ClearhausConfig`                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.clearhaus.ClearhausConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>3DS2</string>
     <account>
       <serviceEndpoint>https://gateway.clearhaus.com</serviceEndpoint>
       <username>??</username>
       <password></password> <!-- SHOULD BE LEFT BLANK, NO ENTRY NEEDED -->
       <use3Dsecure>true</use3Dsecure>
       <authType>AUTH_CAPTURE</authType>
               <!--
        <authType>AUTH_CAPTURE</authType> Do an auth + capture in one step
        <authType>FINAL_AUTH</authType> Do a final authorization to later be manually or automatically captured/voided
        <authType>PRE_AUTH</authType> Do a pre-authorization to later be manually or automatically captured/voided
        -->
        <!-- 3DS2 parameters -->
        <acquirerMerchantId>XXXXXXXX</acquirerMerchantId> <!-- Value received from PSP  -->
        <mcc>7995</mcc> <!-- 7995 for gambling merchants change if this isn't applicable to you -->
        <merchantCountry>XXX</merchantCountry> <!-- Origin country of merchant 3 DIGIT ISO for eaxmple SWE or MLT -->
        <merchantUrl>http://www.example.com</merchantUrl> <!-- URL to your website -->
        <merchantName>XXX</merchantName> <!-- Name of your brand -->
        <!-- End of 3DS2 parameters -->
     </account>
    </entry>
    
    <entry>
     <string>Mobilepay</string>
     <account>
       <serviceEndpoint>https://gateway.clearhaus.com</serviceEndpoint>
       <username>??</username>
       <password></password> <!-- SHOULD BE LEFT BLANK, NO ENTRY NEEDED -->
       <use3Dsecure>true</use3Dsecure>
       <authType>AUTH_CAPTURE</authType>
       <mcc>XXXX</mcc> <!-- Merchant Category Code -->
               <!--
        <authType>AUTH_CAPTURE</authType> Do an auth + capture in one step
        <authType>FINAL_AUTH</authType> Do a final authorization to later be manually or automatically captured/voided
        <authType>PRE_AUTH</authType> Do a pre-authorization to later be manually or automatically captured/voided
        -->
     </account>
    </entry>
   </accounts>
  <!-- DO NOT uncomment the below two strings. Values are fetched from PaymentIQ master MID -->
  <!-- <signingApiKey></signingApiKey>
  <signingRsaPrivateKey></signingRsaPrivateKey> -->
</com.devcode.paymentiq.integration.clearhaus.ClearhausConfig>
```

</details>

### Attributes

| PaymentIQ Configuration                                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.username                                            | Is provided by Clearhaus (this is the http username)                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| accountConfig.password                                            | Should be left blank                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| accountConfig.useTokenId                                          | If set to `true` series transactions feature is enabled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| accountConfig.cardOnFileType or config.cardOnFileType             | Defines type of transaction series. Can be set to `INITIAL_RECURRING` if desired to initiate `recurring` transaction series. Can be set to `INITIAL_UCOF` if desired to initiate `unscheduled` transaction series. If desired to run subsequent in series transaction, can be set either to `UCOF_MIT` for unscheduled subsequent series or `RECURRING` for recurring subsequent series. If not set, `INITIAL_RECURRING` value will be used. For this parameter to work `accountConfig.useTokenId` should be set to `true`. |
| accountConfig.originalRecurringPsp or config.originalRecurringPsp | This parameter is taken into account If cardOnFileType is set either to `RECURRING` or `UCOF_MIT`. The PSP on which the initial (`INITIAL_RECURRING` or `INITIAL_UCOF`) transaction executed. If not assigned `BamboraGa` is used as default. If there is no information stored in the user account about the initial or subsequent transactions executed on Clearhaus, it will lookup for the initial transaction information in the PSP assigned in this parameter.                                                       |
| accountConfig.useFixedAmountExemption                             | If set to true, the exemption type for Mastercard series transaction is `fixed_amount_series`. If set to false, exemption type for Mastercard series transaction is `variable_amount_series` By default set to true. Can be also supplied in `CreditcardDepositInput` as attribute value: `useFixedAmountExemption: true`.                                                                                                                                                                                                  |
| accountConfig.version                                             | If set to `ApplePayUsingEncryptedToken`, PaymentIQ will share SymmetricKey & encrypted PaymentToken to the provider and decryption will be taken care of by the provider itself. By default, `version` is not set and PaymentIQ will decrypt the token and share the decrypted token details like PAN, expiry month, expiry year, eci, cryptogram, etc. to the provider.                                                                                                                                                    |

### Clearhaus MPI Config
This config should be on the master level of the merchant, and only holds one entry; merchantUrl. This value should be the merchant's site URL.

The rest of the MPI config is not visible to the merchant, and is in the top level of DevCode’s master merchant.

![](/img/providers/clearhaus01.png)

### Use Declined Tokenized Cards
When making deposits and withdrawals, Clearhaus performs an auth against the card issuer and then tokenizes the cards. In the case of withdrawals, Clearhaus perform a zero amount auth, which some issuers declines. However Clearhaus still creates the token for the cards, and it’s possible to still try and perform a withdrawal if you add the config entry: ```<useDeclinedTokenizedCards>true</useDeclinedTokenizedCards>```. If this is not used, PaymentIQ will consider the transaction failed from the first response.

![](/img/providers/clearhaus02.png)

It’s still possible that the transaction won’t go through, but it might for some issuers. This is used by merchant at own risk.

### 3DS2
For 3DS2 authorizations to work correct with Clearhaus the 3DS2 authentication must also be made through Clearhaus' 3DS Server. This needs to be configured in PaymentIQ by DevCode. See example below.

![](/img/providers/routing/clearhaus_3ds2.png)

### Travel data
Travel data can be supplied by adding to the `CreditcardDepositInput` attributes corresponding values.

<details>
<summary>Click to see the example of travel attributes</summary>
<br/>

```json
{
  "attributes": {
    "travel": {
      "mode": "lodging",
      "date": "2022-09-30"
    }
  }
}
```
</details>

Mandatory parameters for travel data are `mode` and `date`.

Possible values for `mode` parameter - `car`, `lodging`, `flight`.

`date` parameter should be set in the following format: `yyyy-MM-dd`.

When mode set to `car`, the `date` parameter has meaning of a pick up date.

When mode set to `lodging`, the `date` parameter has meaning of a check in date.

When mode set to `flight`, the `date` parameter has meaning of a departure date.

## Example Routing Rule
![](/img/providers/routing/clearhaus.png)

## Test Information

### Test Cards

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| VISA       | 4111111111111111 | Any | Any         | APPROVED    |
| VISA       | 4200000000000000 | Any | Any         | DECLINED    |
| MASTERCARD | 5500000000000004 | Any | Any         | APPROVED    |
| MASTERCARD | 5555555555554444 | Any | Any         | DECLINED    |
