--- 
id: "callpay" 
title: "CallPay EFTsecure"
hide_title: "true"
---
 
![](/img/providers/logos/callpay.png)
![](/img/providers/logos/eftsecure.png)

# CallPay EFTsecure

## About
CallPay is a payment provider offering different digital payment solutions in South Africa, including EFTsecure.
EFTsecure is directly connected to each South African bank and allows the customer to pay using their bank account.


| Provider Name                | CallPay                                                                        |
|------------------------------|--------------------------------------------------------------------------------|
| Product                      | EFTsecure.                                                                     |
| Link                         | [http://www.callpay.com/eftsecure.html](http://www.callpay.com/eftsecure.html) |
| Classification               | Bank                                                                           |
| Regions                      | `South Africa`                                                                 |
| Currencies                   | `ZAR`                                                                          |
| Methods/PaymentTxTypes       | `BankDeposit`, `BankLocalWithdrawal`                                           |
| PaymentIQ Configuration File | `CallpayConfig`                                                                |
| Supported countries          | `ZAF`                                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

### Example
```xml
<com.devcode.paymentiq.integration.callpay.CallpayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username>
        <password>???</password>
        <merchantName>???</merchantName>
        <supportedCurrencies>ZAR</supportedCurrencies>
        <!--Optional, if sending custom beneficiary bank details-->
  		<!--<method>eft</method>
  		<listedBeneficiaryAccount></listedBeneficiaryAccount>
  		<defaultBeneficiaryReference>test</defaultBeneficiaryReference>
  		<beneficiaryAccountNumber>1111222233333</beneficiaryAccountNumber>
  		<beneficiaryName>testName</beneficiaryName>
  		<beneficiaryAccountType>cheque</beneficiaryAccountType>
  		<beneficiaryBank>absa</beneficiaryBank>
  		<apiSalt>Il1ke5Alt0NMy5take</apiSalt>-->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.callpay.CallpayConfig>
```

</details>

### Attributes

| Attribute           | Description                                     |
|---------------------|-------------------------------------------------|
| username            | Provided by Callpay. "Username"                 |
| password            | Provided by Callpay. "Password"                 |
| merchantName        | Will be displayed at checkout                   |
| supportedCurrencies | ZAR is the only supported currency ATM          |
| service             | White label Callpay services.`PAYGURU`,`EFTPAY` |

## White labels

To use a white label from EFTSecure you can send in the `service` parameter in the `BankDeposit` front API request or set the `service` attribute on the account config and route to it.

| White label (service) |
|-----------------------|
| PAYGURU               |
| EFTPAY                |

## Banks

The supported banks are `absa, standard, capitec, fnb, nedbank, investec, bidvest, tyme, windhoek, afribank, oldmutual`.

| Bank      | BankDeposit bankName param value |
|-----------|----------------------------------|
| absa      | absa                             |
| standard  | standard                         |
| capitec   | capitec                          |
| fnb       | fnb                              |
| nedbank   | nedbank                          |
| investec  | investec                         |
| bidvest   | bidvest                          |
| tyme      | tyme                             |
| windhoek  | windhoek                         |
| afribank  | afribank                         |
| oldmutual | oldmutual                        |

## Example Routing Rules
![](/img/providers/routing/callpay.png)

## Test Information

The provider has a fully working test system where you can test each bank to do `successful`, `failed` or `cancelled` transactions. No specific test information needed.