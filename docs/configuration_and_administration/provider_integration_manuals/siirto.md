--- 
id: "siirto" 
title: "Siirto (via Euteller)"
hide_title: "true"
---
 
![](/img/providers/logos/siirto.png)

# Siirto (via Euteller)

## About
Siirto is the first real-time mobile payment platform in Finland that works without a credit or debit card. The end-users only need a mobile phone number for sending or receiving money. All transfers will occur in real time on the user’s bank accounts similar to the successful Swedish payment solution Swish.

Siirto is also the first mobile payment platform to follow the new rules for open payment interfaces (PSD2) two years ahead of the actual implementation date in Europe. This makes it possible for any EU licensed payment service provider to offer payments to the banks regardless of which Siirto member bank the account is opened.

| Provider Name                | Siirto (via Euteller)                                                           |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://siirto.fi/](https://siirto.fi/)                                        |
| Classification               | Online Banking                                                                  |
| Regions                      | `Finland`                                                                       |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `SiirtoDeposit`<br/> `SiirtoWithdrawal`                                         |
| PaymentIQ Configuration File | `-`                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.euteller.EutellerConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DP</string>
      <account>
        <customerId>??</customerId>
        <secretKey>??</secretKey>
        <key1>??</key1><!--Merchant API secret = password-->
        <deviceCategoryMapping>I->0,M->1,*->0</deviceCategoryMapping>
      </account>
    </entry>
    <entry>
      <string>WD</string>
      <account>
        <customerId>??</customerId>
        <secretKey>??</secretKey>
        <key1>??</key1><!--Merchant API secret = password-->
        <deviceCategoryMapping>I->0,M->1,*->0</deviceCategoryMapping>
      </account>
    </entry>
  </accounts>
  <!--<container>iframe</container> default is window, force iframe is necessary for merchant (certain banks don't support iframe so if it's used a new window will opened for those banks) --> 
  <height>715</height>
  <width>805</width>
  <!--
  <extraFields>
    <entry>
      <string>TxRefId</string>
      <string>${ptx.txRefId}</string>
    </entry>
    
    /// one can add
    <entry>
      <string>routing</string>
      <string>siirto</string>
    </entry>
    give permission to Euteller to use Siirto for withdrwal.
    If Siirto withdrawal is not available for the user it will fall back to Bank withdrawal.
    ///
    
  </extraFields>
  -->
</com.devcode.paymentiq.integration.euteller.EutellerConfig>
```

</details>

### Attributes

| Attribute  | Description |
|------------|-------------|
| customerId |             |
| secretKey  |             |
| key1       |             |

## Example Routing Rule
![](/img/providers/routing/siirto.png)

## Test Information

- +358509999991 mobile phone number for SUCCESSFUL transaction 
- +358509999992 mobile phone number for CANCELLED transaction
