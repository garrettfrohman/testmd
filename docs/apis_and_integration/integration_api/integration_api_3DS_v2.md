---
id: "integration_api_3DS_v2"
---

# 3DS v2

The required information that is needed for compliance with 3DS 2 will depend on the Merchant type. All changes for the Integration API are regarding additional Verify User parameters.

- [**Online Services:**](integration_api_3DS_v2_online_services) These are the parameters we recommend you to submit to minimize friction and be compliant with 3DS 2 if you are a PaymentIQ Online Services Merchant. This includes Gaming Merchants.
- [**E-commerce:**](integration_api_3DS_v2_ecommerce) These are the parameters we recommend you to submit to minimize friction and be compliant with 3DS 2 if you are a PaymentIQ E-commerce Merchant.
- [**Full set:**](integration_api_3DS_v2_full_set) In addition to the two Merchant specific sections we have also included a section with the full parameter set. This is included for reference and shows all available parameters. Many of these are provided by PaymentIQ, they can however be overridden. This is not recommended.

## Fields used for 3DS 2 from the Verify User Response

In order to minimize the required information for merchants to submit PaymentIQ will use the following fields from the [verify user response](verifyuser):

| Parameter | Required                                                                                                                   |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| street    | Required                                                                                                                   |
| city      | Required                                                                                                                   |
| zip       | Required                                                                                                                   |
| country   | Required                                                                                                                   |
| email     | Required                                                                                                                   |
| mobile    | Required                                                                                                                   |
| state     | Required unless market or regional mandate restricts sending this information, or State is not applicable for this country |

