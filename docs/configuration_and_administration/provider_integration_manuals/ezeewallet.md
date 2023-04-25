--- 
id: "ezeewallet" 
title: "eZeeWallet (eMerchantPay)"
hide_title: "true"
---
 
![](/img/providers/logos/ezeewallet.png)

# eZeeWallet (eMerchantPay)

## About
eZeeWallet is a payment provider offering different payment solutions globally.
With eZeeWallet the merchant can receive and send money from/to the consumers e-wallet account.<br/>
<!---Using the eZeePayout method the merchant can also transfer money from merchant account to consumer's credit card.
**For gambling merchants, to ensure a closed loop, a deposit should be made with the credit card before it's used for EzeePayoutWithdrawal.**--->

| Provider Name                | eZeeWallet                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://staging.ezeewallet.com](https://staging.ezeewallet.com)                |
| Classification               | Wallet                                                                          |
| Currencies                   | `EUR`                                                                           |
| Methods/PaymentTxTypes       | `EzeeWalletDeposit`<br/> `EzeeWalletWithdrawal`, <!---`EzeePayoutWithdrawal`--> |
| PaymentIQ Configuration File | `EzeeWalletConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.ezeewallet.EzeeWalletConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username>
        <password>???</password>
        <supportedCurrencies>EUR</supportedCurrencies>
        <merchantName>???</merchantName>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ezeewallet.EzeeWalletConfig>
```

</details>

### Attributes

| Attribute    | Description                            |
|--------------|----------------------------------------|
| username     | Provided by eZeeWallet. "API username" |
| password     | Provided by eZeeWallet. "API password" |
| merchantName | Will be displayed at checkout          |


### Additional attributes for V2

| Attribute   | Description                                                                                                                                                                       |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantUrl | Merchant's website.                                                                                                                                                               |
| version     | Version of the provider API to be used. "v2" is the latest API version. If the value is other then "v2" or none - older version of the provider API will be attempted to be used. |

<details>
<summary>Click to view example configuration for V2</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.ezeewallet.EzeeWalletConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <version>v2</version>
    <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>???</username>
        <password>???</password>
        <supportedCurrencies>EUR</supportedCurrencies>
        <merchantName>???</merchantName>
        <merchantUrl>???</merchantUrl>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ezeewallet.EzeeWalletConfig>
```

</details>

## Payment Flow

#### EzeeWalletDeposit
1. Select Ezeewallet payment option in PaymentIQ Cashier and enter wallet-id, password and amount like shown below.

![](/img/providers/ezeewallet03.png)

2a. If the user has sufficient funds in the eZeeWallet account the deposit will be processed.

2b. If the user has insufficient funds in his account he will be redirected to a page to top up the account

![](/img/providers/ezeewallet04.png)

<br/>

![](/img/providers/ezeewallet05.png)


<!--#### EzeePayoutWithdrawal
Select Ezeepayout payment option in PaymentIQ Cashier and enter some amount like shown below.

![](/img/providers/ezeewallet01.png)

Fill in the credit card information and submit.

![](/img/providers/ezeewallet02.png)-->

## Example Routing Rules
![](/img/providers/routing/ezeewallet.png)


## Test Information

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4711100000000000 | Any | Any         |
| MASTERCARD | 5420923878724339 | Any | Any         |

Test Wallet : testezeewallet+devtest@gmail.com
Password : Repi4kitepak13#
- For staging only `EUR` is suspported
