--- 
id: "hexopay" 
title: "Hexopay"
hide_title: "true"
---
 
![](/img/providers/logos/hexopay.png)

# Hexopay

## About
Hexopay is an aggregator provider offering Credit Card and several Alternative Payment Methods. Credit Card payments supports Deposit, Withdrawal, Refund, Void, Auth and Capture. For Alternatvie Payment Methods it depends on the specific method, where all supports Deposit and some also Withdrawal and Refund. Please check with the provider for more details.

| Provider Name                | Hexopay                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://hexopay.com/](https://hexopay.com/)                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Classification               | Aggregator provider                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Void`<br/> `Refund`<br/> `Capture`<br/> `NetellerDeposit`<br/> `NetellerWithdrawal`<br/> `MuchBetterDeposit`<br/> `MuchBetterWithdrawal`<br/> `QiwiDeposit`<br/> `QiwiWithdrawal`<br/> `SkrillDeposit`<br/> `SkrillWithdrawal`<br/> `FunangaDeposit`<br/> `WebRedirectDeposit`<br/> `BankDeposit`<br/> `BankIBANWithdrawal`<br/> `BankLocalWithdrawal`<br/> `NeosurfVoucherWithdrawal`<br/> `InteracWithdrawal`<br/> `InteracDirectWithdrawal` |
| PaymentIQ Configuration File | `HexopayConfig`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.hexopay.HexopayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>apm</string>
      <account>
        <merchantId>????</merchantId>
        <secretKey>???????</secretKey>
        <supportedCurrencies>INR|USD|EUR|SEK</supportedCurrencies>
        <serviceEndpoint>https://api.hexopay.com</serviceEndpoint>
      </account>
    </entry>
    <entry>
      <string>n3ds</string>
      <account>
        <merchantId>????</merchantId>
        <secretKey>???????</secretKey>
        <authType>AUTH_CAPTURE</authType>
        <use3Dsecure>false</use3Dsecure>
        <supportedCurrencies>USD|EUR|SEK</supportedCurrencies>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <string>3ds</string>
      <account>
        <merchantId>????</merchantId>
        <secretKey>???????</secretKey>
        <authType>AUTH_CAPTURE</authType>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>USD|EUR|SEK</supportedCurrencies>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.hexopay.HexopayConfig>

```
</details>

### Attributes

| Attribute                  | Description                                                                                             |
|----------------------------|---------------------------------------------------------------------------------------------------------|
| merchantId                 | Shop ID. Provided by Hexopay                                                                            |
| secretKey                  | Provided by Hexopay                                                                                     |
| serviceEndpoint            | Endpoint differs between Credit Cards and APMs so needs to be set here for non Credit Cards             |
| useTokenId                 | Send request using stored token instead of credit card details. Required to skip 3ds for enrolled cards |
| replacePostRedirectWithGet | Defaults to false. See details below.                                                                   |
| brandId                    | Mandatory for CashtoCode/Funanga. Should be set to the registered CashtoCode web-app name               |

### Supported APMs
The table below shows the supported payment methods and the corresponding TxTypes that should be used. The service parameter should be included in the front API request only for the generic WebRedirect\* and Bank\* types.

| Name                          | TxType                                                  | Service parameter                          |
|-------------------------------|---------------------------------------------------------|--------------------------------------------|
| Skrill                        | SkrillDeposit, SkrillWithdrawal                         | -                                          |
| Neteller                      | NetellerDeposit, NetellerWithdrawal                     | -                                          |
| MuchBetter                    | MuchBetterDeposit, MuchBetterWithdrawal                 | -                                          |
| Funanga                       | FunangaDeposit                                          | -                                          |
| UPaySafe                      | WebRedirectDeposit                                      | UPAYSAFE                                   |
| Neosurf                       | WebRedirectDeposit, NeosurfVoucherWithdrawal            | NEOSURF                                    |
| Interac                       | BankDeposit, InteracWithdrawal, InteracDirectWithdrawal | INTERAC, INTERAC_ONLINE, INTERAC_ETRANSFER |
| Online_Banking (NexusPayment) | WebRedirectDeposit                                      | ONLINE_BANKING                             |
| Transact World Net Banking    | WebRedirectDeposit                                      | NET_BANKING                                |
| Transact World UPI            | WebRedirectDeposit                                      | UPI                                        |
| Transact World Cards          | WebRedirectDeposit                                      | TW_CARD                                    |
| RupeePayments                 | WebRedirectDeposit                                      | RUPEEPAYMENTS                              |

#### Interac
Interac deposits can be done in three different modes (channels on Hexopay):
1. Online. Use service parameter INTERAC_ONLINE.
2. ETI (E-Transfer). Use service parameter INTERAC_ETRANSFER.
3. CPI (Combined flow). User get to choose between Online or E-transfer in Interacs redirect page. Use service parameter INTERAC.

Interac withdrawals can either use txType InteracWithdrawal (ETO) or InteracDirectWithdrawal (ACH). No service parameter is necessary.

#### Transact World & RupeePayments
Transact World Net Banking, Transact World UPI and RupeePayments only works for Indian customers, and requires the state to be provided in abbreviated form (e.g. MH) in the Integration API.

### Replace POST redirect with GET
If the APM's redirect is method POST and doesn't allow iframes (e.g. NexusPayment) there have been issues with the redirect using Safari on iOS devices. A workaround have been made that will replace the POST redirect with a GET redirect. Instead of making the POST directly to the provider service this will make a GET request back to PaymentIQ which will respond with a simple HTML page that automatically makes the initial provider POST. To activate this feature add this to the configs account or top level:

`<replacePostRedirectWithGet>true</replacePostRedirectWithGet>`

## Example Routing Rule
![](/img/providers/routing/hexopay.png)
![](/img/providers/routing/hexopay-muchbetter.png)

## Test Information

### Credit Card

Please check [https://techdocuments.hexopay.com/en/test-integration#test-card-number](https://techdocuments.hexopay.com/en/test-integration#test-card-number) for up to date test cards.

### Skrill
To receive test credentials go to the Skrill techsupport.

### Neteller
| E-mail                        | Account ID   | Secure ID |
|-------------------------------|--------------|-----------|
| netellertest_USD@neteller.com | 454651018446 | 270955    |

### Much Better
| Phone Number | Pass Code | One Time Code |
|--------------|-----------|---------------|
| 447624111111 | 1122      | 000000        |
| 447624222222 | 1122      | 000000        |
| 447624333333 | 1122      | 000000        |

### UPaySafe
Any valid Visa card details can be used in the test environment.

Please be aware that when a merchant is approved by uPaySafe that they initially only get set up with test credentials on the providers test system, the provider doesn't issue live credentials until they have been able to review some successful test transactions

### Neosurf
Use voucher PIN: 26WN IIC A09

### Interac
Use user country CAD

### Transact World Cards

Use INR currency

| Card Number      | Exp. date       | CVV |
|------------------|-----------------|-----|
| 4242424242424242 | Any future date | 123 |

