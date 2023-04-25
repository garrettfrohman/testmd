---
id: "commercegate"
title: "CommerceGate"
hide_title: "true"
---

![](/img/providers/logos/commercegate.png)

# CommerceGate

## About
CommerceGate is a payment provider offering:<br/>
- credit card operations (in Brazil as well): 3DS and N3DS deposit, recurring, refund, withdrawal (CFT, OCT), reversal (for withdrawal and refund);
- PIX deposits and withdrawals;
- Boleto deposits in Brazil;
- status check (via polling job as well).

| Provider Name                | CommerceGate                                                                                                            |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.commercegate.com/](https://www.commercegate.com/)                                                          |
| Classification               | Debit/Credit Card Processor                                                                                             |
| Regions                      | `International`                                                                                                         |
| Currencies                   | `EUR`, `GBP`, `USD`, `BRL`                                                                                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`Reversal`<br/>`PixDeposit`<br/>`BoletoBancarioDeposit` |
| PaymentIQ Configuration File | `CommerceGateConfig`                                                                                                    |

## Configuration Information

### Attributes
| Attribute                | Description                                        |
|--------------------------|----------------------------------------------------|
| accountConfig.merchantId | Corresponds to the *Merchant ID* from CommerceGate |
| accountConfig.siteId     | Corresponds to the *Website ID* from CommerceGate  |

### Example

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.commercegate.CommerceGateConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <siteId>??</siteId>
        <useTokenId>false</useTokenId><!--true: enable recurring-->
        <previousAuth>false</previousAuth><!--true: enable OCT withdrawal-->
        <templateName>commercegate-loading-template</templateName>
        <supportedCurrencies>EUR|USD|GBP|BRL</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.commercegate.CommerceGateConfig>
```
</details>

## Example Routing Rules
![](/img/providers/routing/commercegate.png)

## Configuration at provider side

All configuration at provider side will be done by the provider.
Merchant can just specify (but it is optional) callback type as **JSON** and callback method as **POST**.<br/>
Callback URL is dynamic for each payment tx and cannot be specified at provider side.

![](/img/providers/commercegate01.png)

## Test Information

### Payments in Brazil

#### Credit Card

In order to initiate credit card payment you will need to provide `nationalId` parameter (CPF or CNPJ) along with credit card details.<br/>
It can be done either by sending `nationalId` parameter in payment request (e.g. `CreditcardDepositInput.nationalId`) or by sending `nationalIdentificationNumber` attribute in the `verifyuser` response of the Integration API (see example below):
```json
{
  "success": true,
  "userId": "user_123",
  "firstName": "John",
  "lastName": "Doe",
  ...
  "attributes": {
    "nationalIdentificationNumber": "86758181650",
    "district": "Queens"
  },
  ...
}
```
#### Parameters information for APM's

For APM operations `upstreamDestination` is a parameter which must be provided by Merchant, it is not unique for each payment. It is an account or wallet from which the payout id is procсessed.

#### PIX

In order to initiate PIX deposit you will need to use `PixDeposit` transaction type and provide `nationalId` in the payment request.

In order to initiate PIX withdrawals you will need to use `BankDomesticWithdrawal` transaction type and provide `nationalId`in the payment request.
The `nationalId` field can be of type EVP, CPF, CNPJ, EMAIL or PHONE.

#### Boleto

In order to initiate Boleto deposit you will need to use `BoletoBancarioDeposit` transaction type and provide `nationalId` in the payment request.

For Boleto, the customer details like country, state, district, city, street, address and zip code are mandatory.
The "district" attribute can be added in the `verifyuser` response of the Integration API (see example above).
The "street" means "address line 1" ( the street name).
The "address" means "address line 2" ( the number of apartments , house etc). 

## Test Data

### Test Credit Cards

| Card Brand | Card Number         | Exp. Date | CVV | 3D Password | Email                                                | Result                     |
|------------|---------------------|-----------|-----|-------------|------------------------------------------------------|----------------------------|
| Visa       | 4012000300001003    | 01/2023   | 003 | wirecard    | user1@cgtest.com, user2@cgtest.com, user3@cgtest.com | 3DS OK                     |
| MasterCard | 5413330300001006    | 01/2023   | 006 | wirecard    | user1@cgtest.com, user2@cgtest.com, user3@cgtest.com | OK                         |
| Maestro    | 6799860300001000003 | 01/2023   | 003 | wirecard    | user1@cgtest.com                                     | OK                         |
| Visa       | 4012000300003009    | 01/2023   | 009 | wirecard    | user1@cgtest.com                                     | Enrolled + PIN Failed      |
| MasterCard | 5413330300004000    | 01/2023   | 999 | wirecard    | user1@cgtest.com                                     | Enrolled + Unable to Auth  |
| Visa       | 4012000300006002    | 01/2023   | 002 | wirecard    | user1@cgtest.com                                     | Not Enrolled               |
| Maestro    | 6799860300006000008 | 01/2023   | 008 | wirecard    | user1@cgtest.com                                     | Not Enrolled               |
| MasterCard | 5413330300008001    | 01/2023   | 001 | wirecard    | user1@cgtest.com                                     | System Error at Enrollment |

### Test CPF for PIX and Boleto

| CPF         | Payment Method | Status  |
|-------------|----------------|---------|
| 06957410600 | PIX            | Success |
| 52507570800 | Boleto         | Success |

All other CPFs will lead to failed operation results.
