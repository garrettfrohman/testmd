--- 
id: "Mbankomat" 
title: "Mbankomat"
hide_title: "true"
---
 
![](/img/providers/logos/mbankomat.png)

# Mbankomat

## About
Mbankomat is a mobile payments solution supporting Deposits.

| Provider Name                | Mbankomat                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | -                                                                               |
| Classification               | Mobile                                                                          |
| Regions                      | Czech Republic, Slovakia                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `MbankomatDeposit`                                                              |
| PaymentIQ Configuration File | `MbankomatConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.mbankomat.MbankomatConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <key1>??</key1>
        <key2>??</key2>
      </account>
    </entry>
  </accounts>
  <height>600</height>
  <width>800</width>
  <description>??</description>
  <debug>true</debug>
  <ignoreVerify>true</ignoreVerify>
</com.devcode.paymentiq.integration.mbankomat.MbankomatConfig>

```

</details>

### Attributes

| Attribute  | Description                         |
|------------|-------------------------------------|
| merchantId | Merchant ID. Provided by Mbankomat. |
| key1       | Provided by Mbankomat.              |
| key1       | Provided by Mbankomat.              |

## Example Routing Rule

-

## Test Information

### For Czech Republic users

| Operator  | Phone Number  |
|-----------|---------------|
| Vodaphone | +420774695596 |
| O2        | +420721978704 |
| T-Mobile  | +420739984547 |

- Use a user with country czech republic (e.g mock user: CZK)
- Amount: 1 CZK
- Phone number: See above.

### For Slovakia users

| Operator          | Phone Number  |
|-------------------|---------------|
| O2 Slovakia       | +421944306428 |
| T-Mobile Slovakia | +421902814328 |
| Orange Slovakia   | +421907566964 |

- Use a user with country Slovakia (e.g mock user: SLK)
- Amount: 0.1 EUR
- Phone Number: See above, together with SK Provider(the only option).
