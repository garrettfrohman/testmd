--- 
id: "payu" 
title: "PayU"
hide_title: "true"
---
 
![](/img/providers/logos/payu.png)

# PayU

## About
PayU is a payment aggregator offering various payment solutions globally.

| Provider Name                | PayU                                                                                     |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | [https://www.payu.in](https://www.payu.in)                                               |
| Classification               | Aggregator                                                                               |
| Regions                      | `Poland`, `Czech Republic`, `Slovakia`, `Brazil`                                         |
| Currencies                   | `PLN`, `CZK`, `EUR`, `USD`, `BRL`                                                        |
| Methods/PaymentTxTypes       | `BankDeposit`, `BoletoBancarioDeposit`, `CreditcardDeposit`, `Void`, `Capture`, `Refund` |
| PaymentIQ Configuration File | `PayUConfig`                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payu.PayUConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>POLAND</string>
      <account>
        <secretKey>********-****-****-****-************</secretKey>
        <pspPublicKey>********-****-****-****-************</pspPublicKey>
        <productId>123</productId>
        <productName>product name 123</productName>
        <supportedCurrencies>PLN|CZK|EUR</supportedCurrencies>
        <profileId>******</profileId>
      </account>
    </entry>
    <entry>
      <string>BRAZIL</string>
      <account>
        <secretKey>********-****-****-****-************</secretKey>
        <pspPublicKey>********-****-****-****-************</pspPublicKey>
        <productId>456</productId>
        <productName>product name 456</productName>
        <supportedCurrencies>BRL|USD</supportedCurrencies>
        <profileId>******</profileId>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <apiVersion>1.3.0</apiVersion>
  <defaultDescriptor>???</defaultDescriptor>
</com.devcode.paymentiq.integration.payu.PayUConfig>
```
</details>


### Attributes
| Attribute         | Description                                                                                                                                                                           |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| secretKey         | Corresponds to the Private API Key from PayU that is used as 'private-key' request header.                                                                                            |
| pspPublicKey      | Corresponds to the Public API Key from PayU that is used as 'public-key' request header                                                                                               |
| profileId         | Corresponds to the App ID from PayU that is used as 'app-id' request header                                                                                                           |
| productId         | Corresponds to the product id request parameter                                                                                                                                       |
| productName       | Corresponds to the product name request parameter                                                                                                                                     |
| defaultDescriptor | Used to set the 'statement_soft_descriptor' parameter in the credit card request to PayU                                                                                              |
| authType          | Set to `FINAL_AUTH` if you want to do a separate card authorization and capture request for credit card transactions. The default is doing a regular charge request (`AUTH_CAPTURE`). |

### Note

'Private API Key', 'Public API Key' and 'App ID' can be found at [PaymentsOS](https://control.paymentsos.com) and navigating to Account > Business Units.


### Webhook / Callback URL

A callback URL has to be configured at the [PaymentsOS](https://control.paymentsos.com) and navigating to Accounts > Webhooks and "Create a Webhook Endpoint".

| environment | URL                                                       |
|-------------|-----------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/payu/callback |
| Prod        | https://api.paymentiq.io/paymentiq/api/payu/callback      |

It is also important to enable the "Payment Event Alerts" when adding the callback URL, please enable it as the picture below suggests.

![](/img/providers/payu02.png)

### Get available methods
PaymentIQ has exposed an endpoint where it's possible for you as a merchant to fetch the available PayU payment methods and populate them as options in the cashier. This can be used for those PayU services that have several payment options, e.g the PayU Poland service, where the user picks the method to be used and is sent to PIQ as the `service` value.

##### Request
`GET https://api.paymentiq.io/paymentiq/api/payu/available-methods/{MerchantId}?account={PSP account}`

Replace `{MerchantId}` with your MID in PaymentIQ, and `{PSP account}` with the name of the PSP account that you want to use inside the PayUConfig.

##### Example request (test environment)
`curl --location --request GET 'https://test-api.paymentiq.io/paymentiq/api/payu/available-methods/1000?account=POLAND'`

##### Example response

```json
{
    "success": true,
    "availableMethods": [
        {
            "displayName": "BLIK",
            "vendor": "blik",
            "sourceType": "bank_transfer",
            "status": "available",
            "logoUrl": "https://static.payu.com/images/mobile/logos/pbl_blik.png",
            "minAmount": 100,
            "maxAmount": 99999999
        },
        {
            "displayName": "Płacę z iPKO",
            "vendor": "p",
            "sourceType": "bank_transfer",
            "status": "available",
            "logoUrl": "https://static.payu.com/images/mobile/logos/pbl_p.png",
            "minAmount": 50,
            "maxAmount": 99999999
        },
        {
            "displayName": "mTransfer",
            "vendor": "m",
            "sourceType": "bank_transfer",
            "status": "available",
            "logoUrl": "https://static.payu.com/images/mobile/logos/pbl_m.png",
            "minAmount": 50,
            "maxAmount": 99999999
        },
        {
            "displayName": "Płatność online kartą płatniczą",
            "vendor": "c",
            "sourceType": "credit_card",
            "status": "available",
            "logoUrl": "https://static.payu.com/images/mobile/logos/pbl_c.png",
            "minAmount": 5,
            "maxAmount": 99999999
        }
    ]
}
```

| parameter   | description                                                           |
|-------------|-----------------------------------------------------------------------|
| displayName | Name of the method                                                    |
| vendor      | Value that needs to be sent to PIQ as the `service` value             |
| sourceType  | Type of method, e.g `credit_card` or `bank_transfer`                  |
| status      | If the method it available. By default we only show available methods |
| logoUrl     | URL to the payment methods logo if it is to be displayed              |
| minAmount   | The minimum amount to be used with the method                         |
| maxAmount   | The maximum amount to be used with the method                         |

If you are using the PaymentIQ standardized cashier there is already a prepared HTML template to be used which is called `payu-available-methods`. Please contact the technical support if this is not already available on your MID. The below is an example is how it looks in the cashier.

![](/img/providers/payu03.gif)

## Example Routing Rule
![](/img/providers/routing/payu.png)

## Test Information

Please visit [Testing](https://developers.paymentsos.com/docs/providers/payu-singleplatform.html#testing) section in the provider's API documentation for more info.

### Bank

To make a bank transfer the user has to specify the amount and select bank a bank name to provide as the service parameter for the BankDeposit method. Please see above how to fetch the available methods. Once the payment is initiated the user will be redirected to the bank page to complete payment.

![](/img/providers/payu01.png)

After payment is completed the user will receive a corresponding email (email address is configured during company/shop registration at [https://merch-prod.snd.payu.com/cp/company_data](https://merch-prod.snd.payu.com/cp/company_data) in case of Sandbox account: Account configuration > Company data).

### Boleto Bancario

To test "Cash" payments for Boleto, first make sure that the user address is a correct Brazilian address e.g. `country=BRA`, `city=São Paulo`, `street=Alameda Santos, 122`, `zip=09171-640` and you have to use the BoletoBancarioDeposit transaction type. This type requires the specific input `nationalId` which is the users national identification number (CNPJ). A valid CNPJ for use in test is `32593371000110`. Once the transaction is initiated the user will be redirected to a page where they can see and print out their receipt (which if it would be live the user has to take to a relevant Payment Office and pay for their purchase).

To complete the full flow and get a successful transaction in test, PayU has to be contacted and provided with the external id of the transaction so that they can approve the pending transaction, which in turn pushes a notification to PIQ in order to put the transaction to a successful state. If this is not done the transaction will remain in state WAITING_INPUT.

### Credit Card

When testing credit card deposits you initiate the transaction with the regular CreditcardDeposit type.

### Brazil

| Card number      | Expiry              | CVV |
|------------------|---------------------|-----|
| 4705980330050322 | 11/2023             | 777 |
| 4422120000000008 | Any (in the future) | Any |
| 4984460000000008 | Any (in the future) | Any |
| 5123740000000002 | Any (in the future) | Any |

Use card holder name `APPROVED` for successful transactions, and `REJECTED` for failed transactions.
