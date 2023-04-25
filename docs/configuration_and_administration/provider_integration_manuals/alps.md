--- 
id: "alps"
title: "Alps"
hide_title: "true"
---

![](/img/providers/logos/alps.png)

# Alps

## About
Alps is one unique integration to have access to the main payment methods in each country of LATAM region including debit / credit cards, bank transfer and cash payment solutions.

| Provider Name                | Alps                                                                                                                              |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.alps.cl/](https://www.alps.cl/)                                                                                      |
| Classification               | Aggregator                                                                                                                        |
| Regions                      | `LATAM`                                                                                                                           |
| Currencies                   | `BRL`, `CLP`, `PEN`, `USD`                                                                                                        |
| Methods/PaymentTxTypes       | `WalletLatamDeposit` <br/> `CashLatamDeposit` <br/> `BankLatamDeposit`  <br/> `WebRedirectDeposit` <br/> `BankDomesticWithdrawal` |
| PaymentIQ Configuration File | `AlpsConfig`                                                                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.alps.AlpsConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>CL_PAYMENT</string>
            <account>
                <supportedCurrencies>CLP</supportedCurrencies>
                <publicKey>??</publicKey>
                <secretKey>??</secretKey>
                <channelId>1</channelId>
                <merchantId>153</merchantId>
            </account>
        </entry>
        <entry>
            <string>CL_PAYOUT</string>
            <account>
                <supportedCurrencies>CLP</supportedCurrencies>
                <username>??</username>
                <password>??</password>
                <forceCountry>CL</forceCountry>
            </account>
        </entry>
    </accounts>
    <defaultDescriptor>PaymentIQ Withdrawal</defaultDescriptor>
</com.devcode.paymentiq.integration.alps.AlpsConfig>
```

</details>

### Attributes

| Attribute                      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.publicKey        | Public key given by the provider for creating signatures for deposits requests.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| accountConfig.secretKey        | Secret key given by the provider for creating signatures for deposits requests.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| accountConfig.channelId        | Optional. The Payment channel value. Value of `1` is for using Online Payment channel. `2` is for using Cash payments. `3` (Chile CLP), `6` (Ecuador USD), `8` (Brazil BRL), `9` (Peru PEN) are for Debit & Credit Card payments. `5` is for Bank payment channel. If not set, the channel will be chosen according to the used txType (`WebRedirectDeposit` - Debit & Credit Card payments, `CashLatamDeposit` - Cash payments, `WalletLatamDeposit` - Online payments, `BankLatamDeposit` - Bank payments) |
| accountConfig.merchantId       | Merchant ID in Alps system (required to be configured for deposits)                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| accountConfig.username         | Username given by provider for requesting the access tokens for making withdrawal requests                                                                                                                                                                                                                                                                                                                                                                                                                   |
| accountConfig.password         | Password given by provider for requesting the access tokens for making withdrawal requests                                                                                                                                                                                                                                                                                                                                                                                                                   |
| accountConfig.forceCountry     | Country of banks which are going to be shown on bank selection dropdown when making withdrawal. For example, if the `forceCountry` is set to `CL`, only Chilean banks will be shown on bank dropdown list. If not set, the country value will be taken from user data.                                                                                                                                                                                                                                       |
| accountConfig.bankDetails      | Optional. The information about bank withdrawal which is sent in the withdrawal request.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| accountConfig.shortDescription | Optional. Subject of bank withdrawal which is sent in the withdrawal request. If not set, the value of `accountConfig.defaultDescriptor` or `config.defaultDescriptor` will be used.                                                                                                                                                                                                                                                                                                                         |

NOTE: the merchant should have the account in the `AlpsConfig` named `DEFAULT`, where all the required payouts config parameters should be assigned. The default config is needed for bank details retrieval, if it is not specified, no banks will be shown in the dropdown list when making withdrawal. It is not required, if there is only one accountConfig entry created.   

## Example Routing Rule
![](/img/providers/routing/alps.png)

## Withdrawal Banks List
The list of the banks is shown for user in the PaymentIQ Cashier when making `BankDomesticWithdrawal`. The list is received from specific provider's endpoint. 
In case of using custom cashier, the merchant will need to implement the banks list retrieval logic.
The PaymentIQ endpoint should be called to retrieve the banks list. 

The endpoint for stage environment: [https://test-api.paymentiq.io/paymentiq/api/alps/banks/{country}?merchantId={merchantId}](https://test-api.paymentiq.io/paymentiq/api/alps/banks/{country}?merchantId={merchantId})

The endpoint for production environment: [https://api.paymentiq.io/paymentiq/api/alps/banks/{country}?merchantId={merchantId}](https://api.paymentiq.io/paymentiq/api/alps/banks/{country}?merchantId={merchantId})

Where `country` is a two-letter country code retrieved from the user data (example `CL`) or from the `DEFAULT` account if `forceCountry` is defined. `merchantId` is the ID of the merchant in PaymentIQ.

<details>
<summary>Click to view example of the endpoint response</summary>
<br/>

```json
[
  {
    "id": 27,
    "name": "Banco del desarrollo",
    "code": "507",
    "codes": [
      "507"
    ],
    "alias": [
      "Banco del desarrollo",
      "Banco desarrollo"
    ],
    "country": "CL"
  }
]
```

</details>

The `id` response field of chosen by user bank should be sent as `bankCode` string json request parameter to `paymentiq/api/bankdomestic/withdrawal/validate` and `paymentiq/api/bankdomestic/withdrawal/process` when user submits transaction.

## Test Information
Information about deposit transactions testing can be found [here](https://developers.alps.cl/#9fb1cb92-3a39-4fc2-80f7-da8a3ab944ac) in the Test Transactions section.