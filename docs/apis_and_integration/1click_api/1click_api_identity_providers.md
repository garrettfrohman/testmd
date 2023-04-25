---
id: "1click_api_identity_providers"
---

# Identity Providers

These are currently supported identity providers by PaymentIQ. By default all identity providers can be used for both sign in and sign up.
Some providers support deposit, meaning the user can sign up and deposit in the same flow.

| Identity Provider     | Supports Deposit | Markets       | Website                          |
|-----------------------|------------------|---------------|----------------------------------|
| Trustly               | Yes              | SWE, FIN, GER | <https://trustly.com/se/>        |
| Zimpler               | Yes              | SWE, FIN      | <https://www.zimpler.com/>       |
| Brite                 | Yes              | SWE           | <https://britepaymentgroup.com/> |
| LuxonPay              | Yes              | SWE           | <https://luxon.com/>             |
| GII Swedish Bank-ID   | No               | SWE           | <https://www.bankid.com/en/>     |
| GII Norwegian Bank-ID | No               | NOR           | <https://www.bankid.no/bedrift>  |
| GII XID               | No               | NOR           | <https://www.bankid.no/bedrift>  |
| GII Nemid             | No               | DEN           | <https://www.nemid.nu/dk-da/>    |
| GII Yoti              | No               | Global        | <https://www.yoti.com/>          |
| GII Freja EID         | No               | SWE           | <https://frejaeid.com/>          |
| GII Eidas             | No               | SWE           | <https://www.eid.as/home/>       |
| GII Veriff            | No               | Global        | <https://veriff.me/>             |
| GII Sum & Substance   | No               | Global        | <https://sumsub.com/>            |
| GII Eutellerid        | No               | Fin           | <https://www.euteller.com/>      |
| GII Smart ID          | No               | EST, LTU, LVA |                                  |
| GII Verimi            | No               | GER           |                                  |

## Provider specific information

### Asynchronous verification

Yoti, Veriff, and Sum & Substance returns the result from the user verification later. Since this information is asynchronous we will push it to the merchant. 
We do this by sending an `/api/notification` call.

Example successful notification call:

```json
{
  "txTypeId":"970", 
  "txRefId":"1000A425", 
  "originTxId":"424", 
  "provider":"GlobalIdentityIntegrator", 
  "attributes":"{\"lastName\":\"Hansson\", \"personidType\":\"personnummer\", \"identityProvider\":\"gii-veriff\", \"firstName\":\"Arman\", \"dob\":\"1991-10-28\", \"personid\":\"199110284479}\", \"KYC_VERIFICATION\": \"done\"}",
  "notificationMsg":"KYC Verification successful", 
  "txName":"Notification"
 }
```

Example verification error notification call:

```json
{
  "txTypeId":"970",
  "txRefId":"1000A101",
  "originTxId":"100",
  "provider":"GlobalIdentityIntegrator",
  "attributes":"{\"identityProvider\":\"gii-veriff\", \"KYC_VERIFICATION\": \"failed\"}",
  "notificationMsg":"KYC Verification failed, error: double_callback",
  "txName":"Notification"
 }
```

### Yoti 

Yoti has multiple methods that can be used: application (default), DocScan, and list. In order to choose between these three options, the parameter `yoti-method` should used. This parameter has three different option values: `app`, `doc`, or `list`.

In case of using DocScan, then the parameter `enduser_id` is mandatory. You can also use the parameter `reauthenticate` to force signup scenario instead of the login scenario. Also, `reauthenticate` can have either `true` or `false` value.

Please note that Yoti DocScan does not have a test environment. You will need to take a photo of your real drivers licence or passport.
Yoti DocScan also have issues with Postman.

### GII Veriff

If you supply the parameter `enduser_id` Veriff will treat it as the same user.
The user is cached at Veriff in 5 days so if the user wants to verify themselves again in that time, they will not need to send in all the data again.

Please note that Veriff does not have a test environment. You will need to take a photo of your real drivers licence or passport.
Veriff also have issues with Postman.

### GII Sum & Substance

The parameter `enduser_id` is mandatory to provide functionality for caching the user.
Sum & Substance can also update the users verification status several days after that they have approved it. In this case we will send a new `/api/notification` call.
You should not have sensitive data in `enduser_id` we recommend to use a cryptographic hash function like for example SHA-256. 

### Euteller

You must enter your mobile number in the format +[country code][mobile number].
You will get a real SMS with a verification code.
