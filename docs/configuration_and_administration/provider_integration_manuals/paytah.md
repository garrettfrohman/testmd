--- 
id: "paytah" 
title: "Paytah"
hide_title: "true"
---
 
![](/img/providers/logos/paytah.png)

# Paytah

## About
Paytah is a payment provider offering internal and external bank withdrawal (SEPA payment) operation.

- INTERNAL (BankLocalWithdrawal) payment - from merchant's Paytah account (`sourceAccount` specified in the PaytahConfig) to the user's Paytah account specified in the cashier UI.
- EXTERNAL (BankIBANWithdrawal) payment - from merchant's Paytah account (`sourceAccount` specified in the PaytahConfig) to the user's bank account (IBAN) specified in the cashier UI.

So, if user has a Paytah account -- INTERNAL payment must be used, if not (only IBAN) - EXTERNAL payment must be used.

| Provider Name                | Paytah                                                                                                                                                                                                                                                                                                                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://paytah.com/](https://paytah.com/)                                                                                                                                                                                                                                                                                                                          |
| Classification               | Online/Manual Banking                                                                                                                                                                                                                                                                                                                                               |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                     |
| Availability                 | SEPA Countries: Austria, Belgium, Britain, Bulgaria, Cyprus, Croatia, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Republic of Ireland, Italy, Latvia, Lithuania, Luxembourg, Malta, Netherlands, Poland, Portugal, Romania, Slovenia, Slovakia, Spain and Sweden. Norway, Liechtenstein, Iceland, and also Switzerland and Monaco. |
| Currencies                   | `EUR`                                                                                                                                                                                                                                                                                                                                                               |
| Methods/PaymentTxTypes       | `BankLocalWithdrawal`, `BankIBANWithdrawal`                                                                                                                                                                                                                                                                                                                         |
| PaymentIQ Configuration File | `PaytahConfig`                                                                                                                                                                                                                                                                                                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paytah.PaytahConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <apiKey>??</apiKey>
        <sourceAccount>??</sourceAccount>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <!--There is no request field to specify PIQ tx-ref-id, so it is specified in comment-->
  <defaultDescriptor>Payment: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.paytah.PaytahConfig>
```
</details>


### Attributes

| Attribute     | Description                                                                                                                                                                                               |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey        | Corresponds to *API Key* from Paytah. It is used to authenticate requests. You can find your API Key at https://developer.paytah.com/dashboard. Before Api Key can be used it must be activated by Paytah |
| sourceAccount | Merchant's account where money will be taken from. That is an account in the Paytah system that consisting of digits only e.g. `410011002255`                                                             |

## Example Routing Rule
![](/img/providers/routing/paytah.png)

## Test Information

### Internal payment (withdrawal)

Please use `BankLocalWithdrawal` or choose `Banklocal` in PIQ cashier to initiate internal bank withdrawal.

### External payment (withdrawal)

Please use `BankIBANWithdrawal` or choose `Bankiban` in PIQ cashier to initiate external bank withdrawal.

#### Test data

To make internal/external bank withdrawal on SANDBOX env. you can use any valid test data (see example below):
Paytah SANDBOX env. organized in such a way so the same successful response will be received (it is not possible to simulate failed case).

| Attribute           | Value                                             |
|---------------------|---------------------------------------------------|
| Bank Account Number | 410028645794                                      |
| Swift/BIC           | QHVBFR99                                          |
| IBAN                | FR7630006000011234567890189                       |
| Bank Name           | U.S. Bancorp                                      |
| Bank Address        | Delta, 999 Boulevard Jourdan, 75014 Paris, France |
