--- 
id: "computop" 
title: "Computop"
hide_title: "true"
---
 
![](/img/providers/logos/computop.png)

# Computop

## About
Computop is a Creditcard processor with support for Deposits and Withdrawals.

| Provider Name                | Computop                                                                            |
|------------------------------|-------------------------------------------------------------------------------------|
| Link                         | [https://www.computop.com/us/](https://www.computop.com/us/)                        |
| Classification               | Debit/Credit Card Processor                                                         |
| Regions                      | `International`                                                                     |
| Currencies                   | Please check directly with the provider regarding what currencies are supported     |
| Methods/PaymentTxTypes       | `CreditcardDeposit` `CreditcardWithdrawal` `Refund` `Void` `Capture` `IdealDeposit` |
| PaymentIQ Configuration File | `ComputopConfig`                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.computop.ComputopConfig>
<enabled>true</enabled>
<useViqProxy>true</useViqProxy>
<accounts>
    <entry>
      <string>3DS</string>
      <account>
        <use3Dsecure>false</use3Dsecure>
        <merchantId>???</merchantId>
        <blowFishKey>???</blowFishKey> <!-- Key for blowfish encoding of data sent for initial deposit -->
        <secretKey>???</secretKey> <!-- Used to encrypt the MAC.. (HASH) -->
        <redirectUrl>${baseRedirectUrl}/api/computop/deposit/callback</redirectUrl>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <string>Ideal</string>
      <account>
        <paymentCode>test</paymentCode>
        <merchantId>???</merchantId>
        <blowFishKey>???</blowFishKey> <!-- Key for blowfish encoding of data sent for initial deposit -->
        <secretKey>???</secretKey> <!-- Used to encrypt the MAC.. (HASH) -->
        <successUrl>${baseRedirectUrl}/api/computop/deposit/redirect</successUrl>
        <failureUrl>${baseRedirectUrl}/api/computop/deposit/redirect</failureUrl>
        <useTokenId>true</useTokenId>
       </account>
    </entry>
</accounts>
<defaultDescriptor>My test order</defaultDescriptor>
<mode>Live</mode> <!-- Live eller Test -->
<testModeCode>0000</testModeCode> <!-- Status code to simulate.. 0000 is success -->
<directUrl>https://www.computop-paygate.com/direct.aspx</directUrl>
<direct3DSUrl>https://www.computop-paygate.com/direct3d.aspx</direct3DSUrl>
<payoutUrl>https://www.computop-paygate.com/creditex.aspx</payoutUrl>
<idealUrl>https://www.computop-paygate.com/ideal.aspx</idealUrl>
<notifyUrl>${baseCallbackUrl}/api/computop/deposit/notify/${txRefId}</notifyUrl>
</com.devcode.paymentiq.integration.computop.ComputopConfig>
```

</details>

### Attributes

| Attribute       | Description                                                                                                                                      |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| blowFishKey     | Key for blowfish encoding of data sent for initial deposit                                                                                       |
| secretKey       | Used to encrypt the MAC.. (HASH)                                                                                                                 |
| merchantAddress | Optional parameter used if the merchant wants to re-use the same blockchain account address instead of generating a new one for each transaction |

To use CreditcardWithdrawal the merchant must contact Computop since credit without reference is used and that requires additional configuration. 

## Example Routing Rule
![](/img/providers/routing/computop.png)

## Test Information
For testing, please refer to this [Test guide provided by Computop](https://developer.computop.com/display/EN/Test+Guide).
