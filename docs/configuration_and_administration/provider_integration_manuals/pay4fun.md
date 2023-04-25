--- 
id: "pay4fun" 
title: "Pay4Fun"
hide_title: "true"
---
 
![](/img/providers/logos/p4fLogo.png)

# Pay4Fun

## About
Pay4Fun is a wallet provider offering solutions to pay and receive money with your Pay4Fun account. 

| Provider Name                | Pay4Fun                                                             |
|------------------------------|---------------------------------------------------------------------|
| Link                         | [https://p4f.com/](https://p4f.com/)                                |
| Classification               | E-Wallet                                                            |
| Regions                      | `Brazil`                                                            |
| Currencies                   | `BRL`, `EUR`, `USD`                                                 |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/> `Pay4FunWithdrawal`<br/> `Pay4FunDeposit` |
| PaymentIQ Configuration File | `Pay4FunConfig`                                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pay4fun.Pay4FunConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>???</merchantId>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <supportedCurrencies>EUR|USD|BRL</supportedCurrencies>
        <beneficiaryLogoUrl>https://www.example.com/image</beneficiaryLogoUrl>
        <language>en-US</language>
        <width>600</width>
        <height>600</height>
        <container>window</container>  
     </account>
    </entry>
  </accounts>
  <layoutColor></layoutColor>
  <labelId>???</labelId>
</com.devcode.paymentiq.integration.pay4fun.Pay4FunConfig>
```

</details>

### Attributes

| Attribute          | Description                                                                     |
|--------------------|---------------------------------------------------------------------------------|
| merchantId         | Provided by Pay4Fun. "Merchant ID"                                              |
| apiKey             | Provided by Pay4Fun. "Merchant Secret"                                          |
| secretKey          | Provided by Pay4Fun. "Merchant Key"                                             |
| beneficiaryLogoUrl | URL to logo that will be displayed in checkout                                  |
| language           | Customer’s desired language (pt-BR, en-US etc.) (default: pt-BR)                |
| layoutColor        | Hexadecimal color code that will be displayed in checkout                       |
| labelId            | Label id set in the Pay4Fun backoffice to be sent for all transactions on a MID |

### Note

Account credentials are available in your Pay4Fun backoffice for both staging and production environment.

## Example Routing Rules

![](/img/providers/routing/p4fRouting.png)


## Test Information

| email                 | Password  |
|-----------------------|-----------|
| test_customer@p4f.com | @testp4F! |
