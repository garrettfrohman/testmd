---
id: "request"
---


# API Request

## Query Parameters

| Query params | M/O | Description                                                                                                                                                                                                                                                                                                                                                                                       | Example |
|--------------|-----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| locale       | O   | Query parameter locale defines the user's language and region, default is ```en``` if nothing is provided. Parameter locale connects to what language translations you will receive in response messages, given that there are translations for the specified locale. If a certain provider has support for locales at their end it will be used here as well. | en_GB   |

Example:
```
/paymentiq/api/creditcard/deposit/process?locale=en_GB
```

## Payload Parameters

The following payload parameters apply for almost all requests performed as a merchant.

| JSON params      | Type   | M/O | Description                                                                                                                                                                                                                                                                                                                                                                  |
|------------------|--------|-----|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sessionId        | String | M   | User's session-id. Used by PaymentIQ to verify if user is authenticated. It is is present in every request and is created by the merchant. The PaymentIQ Integration API will later return this in the ```verifyuser``` request to merchant's platform, in order to validate the user.                                                                                       |
| userId           | String | M   | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time.                                                                                                                                                                                                                                                                |
| amount           | String | M   | The amount of the transaction.                                                                                                                                                                                                                                                                                                                                               |
| merchantId       | String | M   | PaymentIQ merchant identifier which will process the payment. ID is assigned to merchant in the on-boarding process.                                                                                                                                                                                                                                                         |
| attributes       | Object | O   | A map of optional parameters which are merchant specific and are not related to the payment request, e.g.bonus code, channel, and request specific success and failure URLs. These will be reflected back to merchant in the authorize and transfer/cancel requests in the Integration API. **Note: Some properties are reserved for certain uses by PaymentIQ, see below.** |
| orderInformation | Object | O   | Optional parameter to collect certain billing and shipping information which is useful for certain E-Commerce focused providers such as Qliro and Klarna. See below for an extended example.                                                                                                                                                                                 |

Minimal example:

```json
{
  "amount": "10",
  "merchantId": "1",
  "sessionId": "2864e062-c65d-4060-7db3-890b028c6983",
  "userId": "123456",
  "attributes": {
    "bonusCode": "A123",
    "channelId": "mobile"
  }
}
```
#### The following properties are reserved in `attributes`

| JSON params   | Type   | M/O | Description                                                                               |
|---------------|--------|-----|-------------------------------------------------------------------------------------------|
| bonusCode     | String | O   | Bonus code entered or selected by user in merchant's system. Max length is 50 characters. |
| successUrl \* | String | O   | Request specific landing page for successful redirect payments.                           |
| failureUrl \* | String | O   | Request specific landing page for failed redirect payments.                               |
| pendingUrl \* | String | O   | Request specific landing page for pending redirect payments.                              |
| cancelUrl \*  | String | O   | Request specific landing page for canceled redirect payments.                             |
| channelId     | String | O   | User's channel, e.g. mobile, tablet, or browser.Max length is 100 characters.             |
| type          | String | O   | Type of payment, e.g. normal or quick. Max length is 100 characters.                      |

\* If these are sent as attributes they will override the potentially configured values in the `MerchantConfig`

#### Extended example with `orderInformation`

```json
{
  "amount": "10",
  "merchantId": "1",
  "sessionId": "2864e062-c65d-4060-7db3-890b028c6983",
  "userId": "123456",
  "attributes": {
    "bonusCode": "A123",
    "channelId": "mobile"
  },
  "orderInformation": {
        "shippingAddressSameAsBillingAddress": true,
        "deliveryDate": "2021-06-05",
        "deliveryTimeFrame": "20",
        "billingAddress": {
            "firstName": "Jane",
            "lastName": "Doe",
            "title": "title",
            "email": "email@provider.com",
            "organizationName": "organizationName",
            "careOf": "careOf",
            "street1": "street1",
            "street2": "street2",
            "street3": "street3",
            "zip": "zip",
            "city": "city",
            "region": "region",
            "phoneNumber": "+46723179791",
            "country": "SWE",
            "reference": "reference",
            "attention": "attention"
        },
        "shippingAddress": {
            "firstName": "Jane",
            "lastName": "Doe",
            "organizationName": "organizationName",
            "careOf": "careOf",
            "street1": "street1",
            "street2": "street2",
            "zip": "zip",
            "city": "city",
            "country": "SWE"
        },
        "items": [
            {
                "itemId": "123",
                "itemName": "item1",
                "unitPrice": "10",
                "description": "description for item1",
                "totalPrice": "5",
                "taxCategory": "SE12"
            },
            {
                "itemId": "1234",
                "itemName": "item2",
                "description": "description for item2",
                "type": "type",
                "quantity": "1",
                "quantityUnit": "qu",
                "currency": "EUR",
                "unitPrice": "1",
                "totalPrice": "1",
                "totalDiscountAmount": "1",
                "totalTaxAmount": "1",
                "taxCategory": "SE12",
                "taxPercentage": "1",
                "merchantData": "md",
                "productUrl": "http://www.google.com",
                "imageUrl": "http://www.google.com",
                "productIdentifier": {
                    "categoryPath": "categoryPath",
                    "globalTradeItemNumber": "globalTradeItemNumber",
                    "manufacturerPartNumber": "manufacturerPartNumber",
                    "brand": "brand"
                },
                "itemExtraAttributes": {
                    "a": "a",
                    "b": "bb"
                }
            },
            {
                "itemId": "12345",
                "itemName": "item3",
                "quantity": "4",
                "unitPrice": "5",
                "totalPrice": "5",
                "taxCategory": "SE12",
                "taxRate": "SE10"
            }
        ]
    }
  }
```
