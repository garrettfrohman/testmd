---
id: "integration_api_pf_parameters"
---

# Payment Facilitator

In order to connect the payment to the sub-merchant additional data will need to be provided in the attributes object in the answer from [Integration API authorize](authorize).

## Example Authorize response with Payment Facilitator Information

```json
{
	"userId": "User_123",
	"success": true,
	"attributes": {
        "merchantId": "66227919",
		"subMerchantName": "TestSubMerchant",
		"subMerchantId": "VTX1800",       	
		"subMerchantCountry": "SWE",
		"subMerchantCity": "Stockholm",
        "subMerchantPostalCode": "11120",
		"subMerchantAddress": "Vasagatan 16",
		"subMerchantURL": "https://www.example.com",
		"merchantMcc": "5812",
	}
}
```

## Response body parameters for the Merchant Object

| Attribute                       | Description                                                                                                                                                                                         | Info                          |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|
| paymentFacilitatorId            | The paymentFacilitator Id of the Merchant.                                                                                                                                                          | Not needed for BamboraGa      |
| merchantId                      | The acquirer merchantId of the Merchant.                                                                                                                                                            | Also known as "Proxy MID"     |
| merchantMcc                     | The sub-merchant Mcc code.                                                                                                                                                                          |                               |
| subMerchantId                   | The internal merchantId of the sub-merchant.                                                                                                                                                        | Also known as "PF Account ID" |
| subMerchantName                 | The name of the sub-merchant.                                                                                                                                                                       |                               |
| subMerchantAddress              | The address of the sub-merchant.                                                                                                                                                                    |                               |
| subMerchantPostalCode           | The postal code of the sub-merchant.                                                                                                                                                                |                               |
| subMerchantCity                 | The city of the sub-merchant                                                                                                                                                                        |                               |
| subMerchantCountry              | The three letter operational country of the sub-merchant.                                                                                                                                           |                               |
| subMerchantURL                  | The URL of the sub-merchant. Must be a full URL beginning with 'https'.                                                                                                                             |                               |
| subMerchantThreeDSRequestorId   | The ThreeDSRequestorId of the sub-merchant (see the 3DS2 documentation for additional details). If not provided, PaymentIQ will use the corresponding attribute from the Payment Facilitator MID.  |                               |
| subMerchantThreeDSRequestorName | The ThreeDSRequestorname of the sub-merchant (see the 3DS2 documentation for additional details) If not provided, PaymentIQ will use the corresponding attribute from the Payment Facilitator MID. |                               |
