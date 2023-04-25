--- 
id: "vload" 
title: "VLoad"
hide_title: "true"
---
 
![](/img/providers/logos/vload.png)

# VLoad

## About
Vload is prepaid payment method that consists of a 16 to 20 alphanumeric code representing a specific denomination and currency.  
The VLoad product is purchased directly at https://vload.expert (or one of the distributors). 

| Provider Name                | VLoad                                    |
|------------------------------|------------------------------------------|
| Link                         | [https://vload.com/](https://vload.com/) |
| Classification               | Voucher                                  |
| Regions                      | International                            |
| Currencies                   | `USD` `EUR` `JPY`                        |
| Methods/PaymentTxTypes       | `VLoadDeposit`  `VLoadWithdrawal`        |
| PaymentIQ Configuration File | `VLoadConfig`                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vload.VLoadConfig>
  <enabled>true</enabled>
<testMode>true</testMode>
  <accounts>
    <entry>
     <string>default</string>
     <account>
     <apiKey>???</apiKey>
     <secretKey>???</secretKey>
     <terminalId>???</terminalId>
     <supportedCurrencies>USD|EUR|JPY</supportedCurrencies>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.vload.VLoadConfig>

```
</details>

### Attributes

| Attribute  | Description                                                                                                  |
|------------|--------------------------------------------------------------------------------------------------------------|
| apiKey     | Api key provided by VLoad. It is a value that uniquely identifies the merchant company on the provider side. |
| secretKey  | Api secret provided by VLoad. It is the key used to hash the signature string to obtain the signature.       |
| terminalId | Terminal Id provided by VLoad. It indicates from where the transaction is instigated.                        |

## Example Routing Rules

![](/img/providers/routing/vload.png)
 
## Deposits
- The customer should have a vload account where he/she will purchase his/her voucher ( might be single or bundle voucher upon customer choice). 
- On merchant site, the user needs to enter the voucher pins that he/she previously purchased (16 to 20 alphanumeric code). 

## Notes
- The voucher value used on merchant site should be equal to the amount that the user need to pay on merchant site, otherwise the tx will be refused.
- The customer cannot use a partial amount of his single voucher.
- Bundlevoucher consists of several child vouchers(each has its own pin code). The user can use his child voucher separately, but he/she will no longer be able to use his/her bundle voucher pin.

## Test Information

VLOAD PINs are one time use only. Please contact VLOAD for your testing PINs.