---
id: "kyc_overview"
---

# KYC - Overview

Know Your Customer (KYC) is a module in PaymentIQ system that allows you checking your customers ID and age status. This way, you can use the results in order to rule the transaction status accordingly by considering our rule engine. Consequently, you will make smarter, more informed decisions throughout the customer lifecycle.

Right now, we are integrated to CallCredit, GBGroup and DevCode Identity. CallCredit and GBGroup are configurable dynamically, at our back-office, according to your own profile score mapping.
Devcode Identity delivers a multi-channel platform for identification methods, regardless of market or technology. All the solutions from Devcode Identity can be orchestrated from the KYC rules engine in PIQ back-office.

The KYC tab, in PIQ back-office, allows you to search for KYC transactions, block transactions according to their KYC status, and manage the fallback between the KYC providers.

![](/img/fraudrisk/kyc01.png)

## Send KYC status details via Merchant Integration API

PaymentIQ can send KYC results as attributes via Merchant Integration API during the subsequent requests of verifyMerchantUser, such as authorize, cancel, and transfer. In order to activate this functionality, the following tag should be added into MerchantConfig:

```xml
<sendKycResultAsAttributes>true</sendKycResultAsAttributes>
```

The attributes that are going to be sent out are the following:

| Attribute           | Description                                                                                                                                                                                                                             |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kycIdStatus         | ID status, which can be: ERROR, UNDER_AGE, NOT_VERIFIED, VERIFIED, UNDER_VERIFICATION                                                                                                                                                   |
| kycAgeStatus        | Age state, which can be ERROR, UNDER_AGE, NOT_VERIFIED, VERIFIED, UNDER_VERIFICATION                                                                                                                                                    |
| kycAddressStatus    | Address status, which can be ERROR, UNKNOWN, NOT_VERIFIED, VERIFIED, UNDER_VERIFICATION                                                                                                                                                 |
| kycPepsAndSanctions | Peps & Sanciton status, which can be a string of multiple values, which are separated by comma such as PEP_WARNING,SANCTIONS_WARNING,SDN_WARNING                                                                                        |
| kycProvider         | KYC provider name at PaymentIQ side, for example DID_GDC                                                                                                                                                                                |
| kycStatus           | The overall KYC status at PIQ side, which can be: VERIFIED, VERIFICATION_IN_PROGRESS, VERIFICATION_FAILED, VERIFICATION_EXTERNAL_FAILURE, VERIFICATION_FAILED_INVALID_USER_DATA, NOT_VERIFIED, BLOCKED, UNDER_AGE, UNKNOWN, UNKNOWN_AGE |
| kycProviderScore    | Provider based score, which can be a number                                                                                                                                                                                             |

## KYC and Admin API

The Admin API also offers a Swagger UI view, where you can send real request towards either our production or test server. KYC Check function `POST /admin/v1/kyc/check` can be used to do server-to-server requests. This functinality can be used to trigger KYC check requests by evaluating pre-configured KYC Routing and Fallback rules at PaymentIQ.

Please find the Swagger UI [here](https://backoffice.paymentiq.io/paymentiq/swagger-ui.html)

| Environment | Endpoint                                                                |
|-------------|-------------------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/admin/v1/kyc/check?merchantId=1 |
| Production  | https://api.paymentiq.io/paymentiq/admin/v1/kyc/check?merchantId=1      |


### Request body

The merchant should get an access token through the Admin API, which will be used for the authorization header. A CURL request example follows: 

```
curl --location --request POST 'https://test-api.paymentiq.io/paymentiq/admin/v1/kyc/check?merchantId=1' \
--header 'Content-Type: application/json' \
--header 'authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9' \
--data-raw '{
  "userId": "123",
  "merchantKycStatus": "hi",
  "name": "Viktor Rydberg",
  "firstName": "Viktor",
  "lastName": "Rydberg",
  "sex": "MALE",
  "dob": "1971-02-01",
  "street": "SOMMARBO 207",
  "city": "JORDBRO",
  "state": "",
  "zip": "13767",
  "country": "SWE",
  "ip": "192.0.0.0",
  "email": "abdallah.salameh@bambora.com",
  "mobile": "24161472",
  "ssn":"",
  "attributes": {
    "success": "http://site.come/sucess",
    "pending": "http://site.come/pending",
    "failed": "http://site.come/failed"
  }
}'
```

### Response body

A JSON response will received as follows:

```json
{
    "userId": "123",
    "merchantId": 1,
    "ssn": "",
    "kycOverallStatus": "VERIFICATION_IN_PROGRESS",
    "kycAgeStatus": "UNDER_VERIFICATION",
    "kycIdStatus": "UNDER_VERIFICATION",
    "pepsAndSanctionStatus": "",
    "merchantKycStatus": "hi",
    "firstName": "Viktor",
    "lastName": "Rydberg",
    "sex": "MALE",
    "dob": "1971-02-01",
    "street": "SOMMARBO 207",
    "city": "JORDBRO",
    "zip": "13767",
    "country": "SWE",
    "email": "abdallah.salameh@bambora.com",
    "mobile": "24161472",
    "score": 0,
    "redirectOutput": {
        "html": null,
        "url": "https://demo-api.gii.cloud/api/oauth/auth_proxy?id=614504042416537606&uuid=bb437406-bd26-4cbf-b0dc-45e94edf159a",
        "method": "GET",
        "container": "window",
        "parameters": {},
        "height": null,
        "width": null,
        "sizeUnit": null
    },
    "attributes": {
        "success": "http://site.come/sucess",
        "pending": "http://site.come/pending",
        "failed": "http://site.come/failed"
    }
}
```

For some KYC providers, such as Sum&Sub, a `redirectOutput` param will be returned back in the response. The merchant can use it to redirect the end-user into the KYC provider side and upload the required documents. A callback notification will be received later to update the KYC data with the mapped status at PaymentIQ side.
